---
title: "Decoding JWT"
date: 2023-05-06T17:25:53Z
draft: false
tags: ['owasp', 'security', 'jwt']
categories : ['Development']
---

## Introduction

JSON Web Token (JWT) is a compact, URL-safe means of representing
claims to be transferred between two parties. The claims in a JWT
are encoded as a JSON object that is used as the payload of a JSON
Web Signature (JWS) structure or as the plaintext of a JSON Web
Encryption (JWE) structure, enabling the claims to be digitally
signed or integrity protected with a Message Authentication Code
(MAC) and/or encrypted

## Online tools

If you work with JWT tokens, you might have used http://jwt.io, a website that lets you decode and verify them online. It's a valuable tool, but it has some limitations. There is another website that I think is better: http://jwt.ms.

http://jwt.ms is a website created by Microsoft for their Azure Active Directory documentation. It has several advantages over http://jwt.io:

- It has a more elegant and intuitive design that makes it easy to use and understand.
- It shows more details about the token, such as the issuer, audience, expiration time, signature algorithm, and key ID.
- It validates the token against some common criteria, such as expiration, signature, issuer, audience, and required claims. It also warns you if the token uses a weak algorithm or contains sensitive data in the payload.
- It lets you edit the token and see how it changes the decoded output and the validation results. You can also copy the token or download it as a file.
- It supports both JWT and JWE (JSON Web Encryption) tokens, which are encrypted JWT tokens that provide more security.

As you can see, http://jwt.ms is a more comprehensive and user-friendly tool to decode JWT tokens than http://jwt.io. Try it out and see how much you can learn from your tokens and how you can improve your web security practices.

:warning: However, be careful when decoding tokens online. Tokens are credentials that grant access to your system's resources, and revealing them using online tools can expose them to privacy and security risks. Always use trusted websites, and never share your tokens with anyone.

## A safer local option

Online token decoding can compromise security. Tokens are the keys to your system's resources, and using online tools to decode them can expose them to privacy and security threats. If unsure, you can always use a local easy method to view the token contents.

```sh
 jq -R 'split(".") | .[1] | @base64d | fromjson' <<< "${TOKEN}
```
