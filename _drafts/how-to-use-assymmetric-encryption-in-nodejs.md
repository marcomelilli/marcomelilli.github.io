---
layout: ''
title: How to use assymmetric encryption in Nodejs
subtitle: ''
gh-repo: ''
gh-badge: []
tags: []
comments: false
date: 
published: false

---
* To **generate** private and public key in nodejs:

      const { writeFileSync } = require('fs')
      const { generateKeyPairSync } = require('crypto')
      
      function generateKeys() {
        const { privateKey, publicKey } = generateKeyPairSync('rsa', {
          modulusLength: 4096,
          publicKeyEncoding: {
            type: 'pkcs1',
            format: 'pem',
          },
          privateKeyEncoding: {
            type: 'pkcs1',
            format: 'pem',
            cipher: 'aes-256-cbc',
            passphrase: '',
          },
        })
      
        writeFileSync('private.pem', privateKey)
        writeFileSync('public.pem', publicKey)}
* To **generate** private and public key using **openssl** (this method works with JsEncrypt):
  * Within your terminal (Unix based OS) type the following:

        openssl genrsa -out rsa_4096_priv.pem 4096
  * This generates a private key, which you can see by doing the following

        cat rsa_4096_priv.pem
  * Next, you can then get the public key by executing the following command.

        openssl rsa -pubout -in rsa_4096_priv.pem -out rsa_4096_pub.pem
  * You can see the public key by typing...

        cat rsa_4096_pub.pem
* To encrypt and decrypt in **nodejs**:

      const crypto = require('crypto')
      const path = require('path')
      const fs = require('fs')
      
      function encrypt(toEncrypt, relativeOrAbsolutePathToPublicKey) {
        const absolutePath = path.resolve(relativeOrAbsolutePathToPublicKey)
        const publicKey = fs.readFileSync(absolutePath, 'utf8')
        const buffer = Buffer.from(toEncrypt, 'utf8')
        const encrypted = crypto.publicEncrypt(publicKey, buffer)
        return encrypted.toString('base64')}
      
      function decrypt(toDecrypt, relativeOrAbsolutePathtoPrivateKey) {
        const absolutePath = path.resolve(relativeOrAbsolutePathtoPrivateKey)
        const privateKey = fs.readFileSync(absolutePath, 'utf8')
        const buffer = Buffer.from(toDecrypt, 'base64')
        const decrypted = crypto.privateDecrypt(
          {
            key: privateKey.toString(),
            passphrase: '',
          },
          buffer,
        )
        return decrypted.toString('utf8')}
      
      const enc = encrypt('hello', `public.pem`)
      console.log('enc', enc)
      
      const dec = decrypt(enc, `private.pem`)
      console.log('dec', dec)
* To encrypt public key in **javascript**

      var crypt = new JSEncrypt();
      crypt.setKey(__YOUR_OPENSSL_PRIVATE_OR_PUBLIC_KEY__); //You can use also setPrivateKey and setPublicKey, they are both alias to setKey
      
      var text = 'test';
      var enc = crypt.encrypt(text);


* references::
  * [Asymmetric Encryption using Nodejs Crypto module](https://stackoverflow.com/questions/54087514/asymmetric-encryption-using-nodejs-crypto-module)
  * [https://github.com/travist/jsencrypt](https://github.com/travist/jsencrypt "https://github.com/travist/jsencrypt")