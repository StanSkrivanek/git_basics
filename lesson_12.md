# SSH Communication

---

## What is SSH

In short SSH (Secure Shell) use both `SYMMETRIC` and `ASYMMETRIC` encryption. In simple way an `Asymmetric` key is used with help of `DHEx` to generate secure private `Symmetric` key for encrypted communication and `HMAC` to make sure that message wasn't modified durning transmission.

[Understanding the SSH Encryption and Connection Process](https://www.digitalocean.com/community/tutorials/understanding-the-ssh-encryption-and-connection-process)
[How does SSH Work](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work)

---

## Three secure communication principles

Encryption is the specific way how to hide data content durning communication between two computers. Usually is communication between `client` (your computer) and `Host` (server/other computer).

Encryption is used to prevent access these data for unauthorized suspects durning communication. In SSH are used tree basic encryption algorithms `Symmetric`, `Asymmetric`, and `Hash`

### Symmetric

Symmetric encryption use **one** secret key for encryption and decryption on both communication sides (client/host).

On send request from `client` are data encrypted with key. Encrypted data are send over internet and when data arrive on other computer they can be decrypted with identical key.

When someone else see this data he would not understand these data because he doesn't have right key to decrypt it.

**pure data:** `"How are you?"`
**encrypted by key 1:** `12r=69ehYC*Lu7`
**data arrive:** `12r=69ehYC*Lu7`
**decrypted by key 1:** `"How are you?"`

This is how SSH works (partially) in its core but this type of encrypted communication has on major security problem. **Anyone who has the key can decrypt the message**.

Thats why we have to some way hide this key that other suspects (people) can't find what key is used. This is done with **Key exchange algorithm**. What make this algorithm secure is that key is never transmitted between `client` and `host`, mean it's not part of transmitted data.

These computers share some public piece of data and then independently calculate this secret key. Even if someone else get these public data would not be able calculate key thanks to **Key exchange algorithm**

Secret key is specific for each SSH session and is generated prior to something called **client authentication**. With use of **Symmetrical** encryption between `client` and `host` all communication will be encrypted and private. But we need use `key exchange algorithm`.

[Symmetric - video](https://www.dropbox.com/s/v8oxrhzj0jveq6r/SymmetricEncryption.m4v?raw=1)

### Asymmetric

Asymmetric encryption use two mathematically related keys `public` and `private`.

#### How this works:

`Host` and `client` will exchange `public` key. When keys are exchanges and communication request is send an `Difiie Helman key exchange` function is activated and it will create a `private` Symmetric key. This key is based on partial information's of `private` and `public` keys from both sides (client/host).

Data send from `client` are encrypted with **host** `public key`. These data are transmitted to `host` and decrypted by its own `private` key.

**Difiie Helman key exchange is used everywhere** so we need as developers know how thing works

[DHEx explained - video](https://www.youtube.com/watch?v=NmM9HA2MQGI)

But that's not all there may happen situation that some way will unauthorized entity ("man in middle") break this encrypted communication and pretend to be `HOST` and `CLIENT`. If this happened "man in middle" can read and/or modified these data and send them over this "secure" communication pipe.

Don't worry there is a way how to make this possible vulnerability more secure by using Hash function.

[Asymmetric - video](https://www.dropbox.com/s/n9esnfdjn2af0ig/AsymmetricEncryption.m4v?raw=1)

### Hash

Hashing is another type of cryptography. Hash algorithm is different from both algorithms above as is used to ensure that the received message is **intact** and **unmodified**.

We have come across Hash function in early lessons about Git when we create a hash with use of SHA-1. Do you remember? Just keep in mind that SHA-1 is not used in any secure communication nor in SSH.

In secure communication is Hash function used to generate 40 digits number that is unique to data. Remember, one small change in data will generate completely different Hash number. Hashing is very useful as is for unauthorized entities almost impossible to reverse hash to get and change data.

#### How it works?

Once secure communication pipe is established using `asymmetric` and `symmetric` keys, than data run thru Hash function before are transmitted.

As part of the symmetrical encryption negotiation outlined above, a message authentication code (MAC) algorithm is selected. The algorithm is chosen by working through the client's list of acceptable MAC choices. The first one out of this list that the server supports will be used.

Each message that is sent after the encryption is negotiated must contain a MAC so that the other party can verify the packet integrity. The MAC is calculated from the symmetrical shared secret, the packet sequence number of the message, and the actual message content.

The MAC itself is sent outside of the symmetrically encrypted area as the final part of the packet. Researchers generally recommend this method of encrypting the data first, and then calculating the MAC.

Hash is generated with `HMAC` (_Hash-based Message Authentication Code_) from 3 types of data 1. generated symmetric key, 2. Packet sequence number, 3 data it self. Then generated Hash is send to `Host`.

As Host have identical data 1. generated symmetric key, 2. Packet sequence number and because data were send thru SSH Host have also data it self. Host will now run these data thru identical Hash function to generate Hash.

Then Host will check is received Hash from client match Hash generated on its side. If they match this mean that message wasn't modified

**_A Host/client should not be able to produce the original message from a given hash, but they should be able to tell if a given message produced a given hash._**

[Hash - video](https://www.dropbox.com/s/k1irvsdrd4u4knc/Hashing.m4v?raw=1)

---

## Why SSH for Github

Github give us two secure **encrypted** protocols **HTTPS** and **SSH** to communicate with their server. When we use HTTPS, the server will **always** verified by **Certificate Authorities**.

Main disadvantage is that you always need to provide a password confirm who you are every time you connect to github and try to do some actions as pull, push, merge etc. When you do daily many operations as pull requests, commits etc. Github will always ask for password and this became in no time a bit annoying.

With **SSH** we use more secure communication than just passwords, we **use keys**.

## Create SSH Key

1. **Switch to user account** - home directory (tilde)\
   `$ cd ~`

2. **Create a new directory if doesn't exist**
   `$ mkdir -p ~/.ssh`
   `-p` check if file folder exist
   `ls -a` - show list ( `-a` > include hidden files)

3. **Generate key (pair)**
   `$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
   `-t` type (rsa)
   `-b` base (4096 Bit)
   `-C` comment (email)
   _Provided email has to be identical with email you are assigned to Github_

[Github SSH](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[passphrase](https://security.stackexchange.com/questions/183636/ssh-keygen-what-is-the-passphrase-for)

4. **Check keys**
   `$ ls | grep your_keyname`
   `$ cat your_keyname.pub`

5. **Copy key to clipboard**

```bash
~/.ssh pbcopy < ~/.ssh/id_rsa.pub
```

6. **add SSH Public key to Github**

Go to your github profile, click on your profile image and from open menu choose `Setting`

Next from left sidebar choose `SSH and GPG keys` where you will add `New SSH key`.

In open form choose any descriptive name eg.`Home Desktop` and in large text area paste your key from clipboard. Then confirm with `Add SSH key`

Done ;)

## Create specific SSH key

how to create custom name for `id_rsa`
to know what the key is for eg. `id_rsa_heroku`

1. Once you are inside `.ssh` folder run `ssh-keygen` command in terminal. It will generate keys and than open dialogue
   `Enter file in which to save the key (/Users/stan/.ssh/id_rsa):`

2. copy path `/Users/stan/.ssh/id_rsa` Paste it on end after `:` add custom extension to key `/Users/stan/.ssh/id_rsa_test_01` and confirm with `enter`

3. You can add `passphrase` for extra security but its not essential

<!-- Create authorized_keys file and paste PUBLIC key
`\$ vi ~/.ssh/authorized_keys -->
