---
title: 'xml parsing - snowflake '
author: ''
date: '2021-02-19'
slug: []
categories: []
tags:
  - xml
  - snowflake
  - parsing
Description: ''
Tags: []
Categories: []
DisableComments: no
---

I don't know why we are coming back to traditional DL. Maybe it is cause of well-degined Cloud Servvces such as Snowflake. 
There are so many lagacy DL having history. 
Up to situation, all technology will be chanaged. Haha. 

These days, many clients want to migrate data into new DL, in particular, snowflake. It looks fancy and cool. 
No question about this. 

But when you have old style data like XML, it's a bit tricky to parse it. Snowflake maybe like 'JSON' than XML.

- No support xpath: Unfortunaltly, they do not support xpath. If you have deep nested xml data structure, and your old query use it before, the migration is not cool. :(

in future, maybe snowflake can support it. I hope so. but it's none of my buessiness. 

Until that, we have to parse each tag one by one. 

ex, xpath for XML_DATA column. 
```
xpath_find(XML_DATA, '//tag1/tag2/tag3/tag4'::varchar(133), 1)
```
This throws the value of tag4.


For the snowflake,
```
XMLGET(XMLGET( XMLGET(PARSE_XML(MSG_DATA), 'tag2'), 'tag3'), 'tag4', 0):"$"::varchar(100)
```

## reference 

`parse_xml` is taking away the root element, and index is from 0 in snowflake. 

- https://docs.snowflake.com/en/sql-reference/functions/parse_xml.html
- https://docs.snowflake.com/en/sql-reference/functions/xmlget.html




