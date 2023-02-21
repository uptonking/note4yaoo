---
title: watarble-feat-encryption-security
tags: [encryption, security, watarble]
created: 2022-11-24T11:35:13.876Z
modified: 2022-11-24T11:36:36.445Z
---

# watarble-feat-encryption-security

# guide

- encrypt
  - [end-to-end-encryption · GitHub Topics](https://github.com/topics/end-to-end-encryption?l=javascript&o=desc&s=)

- https://github.com/robinmoisson/staticrypt
  - StatiCrypt uses AES-256 to encrypt your HTML file with your passphrase and return a static page including a password prompt and the javascript decryption logic that you can safely upload anywhere
  - 静态网页加密，基于 crypto.js ，可以不使用任何后端，运行命令就可以将原网页生成一个密码保护提示页。可以非常方便的部署到任何静态文件服务中- Netlify,Cloudflare,Github pages。
# blogs

## [Excalidraw: End-to-End Encryption in the Browser_202003](https://blog.excalidraw.com/end-to-end-encryption/)

- Web Cryptography APIs are now widely available to all the browsers that let us implement this. 
- That said, the APIs to deal with encryption, keys and binary data are not the most straightforward

## [How to encrypt files in react using Web Crypto API.](https://abhijeet-nandvikar.hashnode.dev/how-to-encrypt-files-in-react-using-web-crypto-api)

- [React App](https://frontend-file-encryption-demo.abhijeetnandvik.repl.co/)
  - https://replit.com/@AbhijeetNandvik/frontend-file-encryption-demo

## [End-to-End Encrypted Chat with JS & Web Crypto API](https://getstream.io/blog/web-crypto-api-chat/)

# encryption-examples

# encryption-utils
- https://github.com/seald/sscrypto
  - a wrapper around other cryptography libraries, intended to be simple to use, provide a consistent interface for multiple encryption backends (for now, forge, nodeJS crypto, and WebCrypto.subtle), and well-chosen parameters.
  - https://github.com/digitalbazaar/forge
    - A native implementation of TLS in Javascript and tools to write crypto-based and network-heavy webapps


# more

- https://twitter.com/xiazhaoyang/status/1620653699344523266
  - 尝试理解一下，目前iCloud数据和升级高级数据加密后的区别，所谓的“端到端”加密是否指的是在“客户端”做加密和解密这两件事？
- 我理解之前的数据也是加密存储在server的，只是密钥被apple托管。而升级后，密钥归属用户，apple拿不到。
  - 『密钥拥有者』跟『服务器所有者』可以是两个角色。服务器可以用谷歌的或者微软的。
- 目前也是加密存储的，密钥apple管理。高级端侧加密，密钥有基于锁屏密码等派生的，密钥在用户手中

