---
title: GoLucene Week 12 Dev Status
date: '2013-08-24'
description:
categories:
- 技术
tags:
- go
- lucene
- golucene
---

In early weeks of the migration, I tried to implement all the logic that might be required to read the index. But I found it rather inefficient, so later I tried to create various stubs with specific panic messages. So whenever I hit a panic complaining about missing implementation, then I do the migration. It would save me a lot of time to avoid migrate unnecessary stuff. It does help and I have been hitting several panic messages now, including

1. Supported slice in SimpleFSIndexInput.
2. Added Numeric entry parsing in DocValuesReader.
3. Added CompressingStoredFieldsReader and CompressingStoredFieldsIndexReader.
4. Error handling of currupted index. 
5. Fixed FieldInfo read logic.