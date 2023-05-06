---
title: "Decoding JWT"
date: 2023-05-06T17:25:53Z
draft: false
tags: ['owasp', 'security', 'jwt']
categories : ['Development']
---

## Online decoders: JWT.IO and JWT.MS

If you work with JWT tokens, you might have used http://jwt.io, a website that lets you decode and verify them online. It's a useful tool, but it has some limitations. There is another website that I think is better: http://jwt.ms.

http://jwt.ms is a website created by Microsoft for their Azure Active Directory documentation. It has several advantages over http://jwt.io:

- It has a more elegant and intuitive design that makes it easy to use and understand.
- It shows more details about the token, such as the issuer, audience, expiration time, signature algorithm, and key ID.
- It validates the token against some common criteria, such as expiration, signature, issuer, audience, and required claims. It also warns you if the token uses a weak algorithm or contains sensitive data in the payload.
- It lets you edit the token and see how it changes the decoded output and the validation results. You can also copy the token or download it as a file.
- It supports both JWT and JWE (JSON Web Encryption) tokens, which are encrypted JWT tokens that provide more security.

As you can see, http://jwt.ms is a more comprehensive and user-friendly tool to decode JWT tokens than http://jwt.io. I suggest you to try it out and see how much you can learn from your tokens and how you can improve your web security practices.

However, be careful when decoding tokens online. Tokens are credentials that grant access to your system's resources, and decoding them using online tools can expose them to privacy and security risks. Always use trusted websites and never share your tokens with anyone.

## A simpler but more secure alternative

Decoding tokens online can impose security risk. Tokens are credentials that allow access to resources of your syste, and decoding them using online toools can lead to privacy and security issues. If you have any doubts you can always use a local simple workaround to dump the token contents

```sh
 jq -R 'split(".") | .[1] | @base64d | fromjson' <<< "${TOKEN}
```

That's all for today. I hope you enjoyed this blog post and found it useful. If you have any questions or feedback, feel free to leave a comment below. And don't forget to subscribe to my blog for more tips and tricks on web development. Happy coding!