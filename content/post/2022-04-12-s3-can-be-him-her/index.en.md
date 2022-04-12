---
title: S3 can be him/her
author: ''
date: '2022-04-12'
slug: []
categories: []
tags:
  - s3
Description: ''
Tags: []
Categories: []
DisableComments: no
---

DataFabric a.k.a MapR 7.0 was released. Surely, there are many bug fixes and version upgrades. 
 - https://docs.datafabric.hpe.com/70/ReleaseNotes/whatsnew.html
 
My most interesting parts are Spark 3.x and Native Object Store. 
As you know, Spark 3.x can use Delta lake which is supporting ACID as big data lake and Object Store is s3 alike store. 

I wonder if S3 will be final destination. I didn't expect S3 became popular like these days. It was one of services in AWS. 
My personal impression was cheap and slow. Very slow. 

Thing is the most computation process is engine level not store level. I did see that. 
Snowflake and Spark can be based S3 which is slow and cheap storage but scalabl easily. 

And people are thinking s3 is cool. :) who can expect this?

OK. then let's go alongside it. 

Anyway, DF7 object store is not opensource. it's native store based on MFS.
it must be faster. and compatible with AWS S3 IAM policy. It means you can implement your own s3 on premise if you like Hybrid combination

Let's see what's going on this. 
