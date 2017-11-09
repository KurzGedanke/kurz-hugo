---
title: "How to Encrypt Files with AES"
date: 2017-09-13T11:49:24+02:00
draft: false
tags: ["encryption", "aes", "tutorial"]
---
In times of mass surveillance, public Wi-Fis and a lot of bad people trying to steal your data you want to encrypt your data before you send them over the internet. 

<!--more-->

This is possible with something called _OpenSLL_ and _AES_. _AES_ is a cryptological cipher to encrypt your data, _OpenSSL_ is a suite with cryptological stuff in it for you to use. _OpenSSL_ should be preinstalled on all _\*nix_ operation system.

### Let's start:

On Mac open your terminal with the spotlight search and entering `terminal`. Hit enter to start it up.

![Terminal on a Mac](/img/encrypt_with_aes/terminal.png)

You need to navigate to the folder where the file, you want to encrypt, is located. In my case this is the Desktop.
If you want to know more about navigating the terminal, [here is a link to a tutorial.](https://computers.tutsplus.com/tutorials/navigating-the-terminal-a-gentle-introduction--mac-3855)

> Of course, you can just copy the commands, but without the `$`. This indicates just a line you can enter in the terminal.

```bash
$ cd Desktop/
```

To show what files you have on your desktop you can use the `ls` command.

```bash
$ ls
very_important_file.txt
```

You can see, I have a `very_important_file.txt`on my desktop, which I want to encrypt before I send it to my friend. To encrypt this file you can use the following command:

```bash
$ openssl aes-256-cbc -a -salt -in very_important_file.txt -out someRandomName.enc

enter aes-256-cbc encryption password:
Verifying - enter aes-256-cbc encryption password:
```

It asks you now for a password. You should use a real strength and long password and communicate it to a safe channel. And if you ask, the internet, even with a super fancy encrypted messenger, is not a safe channel. Let's shortly break up the command.

- `openssl` is the cipher suite I mentioned earlier.
- `aes-256-cbc` is the encryption cipher. An aes with 256 key in cbc mode.
- `-a` is optional and is used for a base64 encoding which enables you to look at the file in a text editor.
- `-salt` adds a nonce to the encryption and makes it even stronger
- `-in` tells _OpenSSL_ which file it should encrypt
- `-out` tells _OpenSSL_ what the name of the output file should be. You should use a random name without an extension so no one can guess the underlying file type.

If your friend wants to decrypt the file he/she can use the following command:

```bash
$ openssl aes-256-cbc -d -a -in someRandomName.enc -out very_important_file.txt

enter aes-256-cbc decryption password:
```

Your friend is of course asked for the password to decrypt the file. But let's break down this command as well.

- `openssl` is the cipher suite I mentioned earlier.
- `aes-256-cbc` is the encryption cipher. An aes with 256 key in cbc mode.
- `-d` tells _OpenSSL_ to use decryption, not encryptipn.
- `-a` tells _OpenSSL_ that the file was base 64 encoded. If you left the `-a` out by the encryption, you have to leave if from the decryption out aswell. 
- `-in` tells _OpenSSL_ which file it should decrypt.
- `-out` tells _OpenSSL_ the output name of the decrypted file.

Please keep in mind that this is just an encryption. The file could be altered on its way through the internet by an attacker.
