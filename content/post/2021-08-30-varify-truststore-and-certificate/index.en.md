---
title: Varify truststore and certificate
author: ''
date: '2021-08-30'
slug: []
categories: []
tags:
  - certificate
  - ssl
  - openssl
Description: ''
Tags: []
Categories: []
DisableComments: no
---

Recently, I have faced new issue. My friends want me to apply own singed certificates to communicate with each other. 

I have struggled a lot about this because I didn't have any background. 

To remind myself, I'd like to leave the history here. 

Basically, I need to understand trusted root certificate chain. There are many official and public organiztion to manage these chain, but here we don't need to know them at all.

Think it like there are family. you are the youngest guy in that family. Your family will assure you are a member of your family. The highest authority will have parents and next will have your older siblings. 


```
<Parents Certificate>  --(sign)--> <your elder siblings certificate> --(sign)--> <next elder siblings certificate> --(..<skip>..) --> <your certificate>
```

That is it. Unfortunately, I cannot believe in you are stable (good person). I need your family higharchy chain of trust. 


In the cyber world, 'openssl' can verify these kinds of chain.


``` bash
$ openssl verify -CAfile RootCA.pem -untrusted SubCA.pem your-cert.pem

```

- RootCA: parents
- SubCA: older sibling
- your-cert: you


In the java world, you need truststore and keystore. 
- truststore : all chain of trust
- keystore : your private keys and signed certificates. 

Your service will refer `truststore` to verify each certificate.

To covert these CA into your truststore, follow this : 

1.
```
openssl pkcs12 -export -chain -in dev-cert.pem -inkey dev-key.pem -out ssl_keystore.p12 -CAfile maprCA.pem -name '<your cluster name>'
```

2.
```
keytool --importkeystore -noprompt -deststorepass mapr123 -destkeystore ssl_keystore -srckeystore maprCA.pk12 -srcstoretype PKCS12 -srcstorepass mapr123

```

3.
```
openssl pkcs12 -in ssl_keystore.p12 -out ssl_keystore.pem
```

4.
```
keytool -importcert -trustcacerts -file RootCA.pem -keystore ssl_truststore -alias 'demo.mapr.com'
```

5.
```
keytool -importkeystore -srckeystore ssl_truststore -destkeystore ssl_truststore.p12 -srcstoretype JKS -deststoretype PKCS12 -deststorepass mapr123 -srcstorepass mapr123 -alias 'demo.mapr.com'
```

6.
```
openssl pkcs12 -in ssl_truststore.p12 -out ssl_truststore.pem
```

to verify keystore and truststore, 

- server:
```
openssl s_server -key dev-key.pem -cert dev-cert.pem -CAfile inter.pem -accept 2009
```

- client:
```
openssl s_client  -connect localhost:2009 -CAfile ssl_truststore.pem
```






