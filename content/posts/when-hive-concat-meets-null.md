---
title: "When hive concat meets null"
date: 2023-07-10T12:00:00+00:00
# weight: 1
# aliases: ["/first"]
tags: ["hive"]
author: "yaoshengjian"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/YSJ1996/yaoshengjian_blog/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

`concat()` function is frequently used in hive to combine multiple string. However there is a small caveat: if `null` is passed as an argument, the function will return `null` regardless of the other parameters! Therefore, the recommend usage is as follows:

>```sql
>select concat(nvl(col_1, ''), nvl(col_2, ''))
>```

Here I use `nvl()` function to make sure the parameters of `concat()` function will not be `null`.
This is also applicable to the `concat_ws()` function in Hive SQL. 

Let us check the [source code](https://github.com/apache/hive/blob/24a82a65f96b65eeebe4e23b2fec425037a70216/ql/src/java/org/apache/hadoop/hive/ql/udf/generic/GenericUDFConcat.java) of `concat()` function.


![source code](../images/concat_source_code.png)
