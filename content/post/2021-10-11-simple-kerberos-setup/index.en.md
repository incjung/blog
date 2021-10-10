---
title: simple kerberos setup
author: ''
date: '2021-10-11'
slug: []
categories: []
tags:
  - kerberos
Description: ''
Tags: []
Categories: []
DisableComments: no
---

I have been facing some Kerberos requests from many customers. It's good for authentication. But if you are working on EDF, a.k.a MapR, it's not any benefict. even thought that, many users want that. Basically, it is only for generationg `MapR Ticket` throught kerberos.

Anyway, sometimes you want to deploy Kerberose server. You can easily do that yourself if you have test machine in linux. 

You will need two parts. one is for kererose sErver. The other is for kereros client. 


# Client Side
Mostly big organization would have the kereros server already. In this case, you will only need to install clients. Simple. ask to make a principal and make keytab file. 

```
kadmin
        : addprinc -randkey mapr/my.cluster.com
        : ktadd -k /opt/mapr/conf/mapr.keytab mapr/my.cluster.com
```

The mapr.keytab file must be owned and readable only by the mapr user. You can specify the location of the mapr.keytab file in the conf/mapr.login.conf file. The default location for mapr.keytab is /opt/mapr/conf.


For more information, https://docs.datafabric.hpe.com/62/SecurityGuide/Configuring-Kerberos-User-Authentication.html


# Server side

Install server
```
yum install krb5-server krb5-libs krb5-auth-dialog
```

Modify `/etc/krb5.conf`. You may need to change kerberos_realm name with your hostname. 

```
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 default_realm = MYREALM.COM
 dns_lookup_realm = false
 dns_lookup_kdc = false
 ticket_lifetime = 24h
 renew_lifetime = 7d
 forwardable = true

[realms]
 MYREALM.COM = {
  kdc = elserver1.example.com
  admin_server = elserver1.example.com
 }

[domain_realm]
 .myrealm.com =CTCCDH1.COM
myrealm.com =CTCCDH1.COM
```

Modify the `/var/kerberos/krb5kdc/kdc.conf` KDC.conf file. But Basically, you don't need to do it. default.

And change `ACL`. /var/kerberos/krb5kdc/kadm5.acl


Create a princial which you want to use 
Create the principal using the command addprinc. For example, create a principal with the user name “root”.
```
$ kadmin.local -q "addprinc root/admin"
Authenticating as principal root/admin@MYREALM.COM with password.
WARNING: no policy specified for root/admin@MYREALM.COM; defaulting to no policy
Enter password for principal "root/admin@MYREALM.COM":
Re-enter password for principal "root/admin@MYREALM.COM":
Principal "root/admin@MYREALM.COM" created.
```


Create the database.

```
kdb5_util create -r $realm -s
```

Start services 
```
# service krb5kdc start
Starting Kerberos 5 KDC:               [  OK  ]

# service kadmin start
Starting Kerberos 5 Admin Server:      [  OK  ]
```

I refered this link. 
- https://www2.microstrategy.com/producthelp/Current/InstallConfig/en-us/Content/installing_kerberos_authentication_service.htm
