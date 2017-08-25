---
title: Refactor IndexWriter
date: '2014-03-21'
description:
categories:
- 技术

---

IndexWriter分明就是个坑。单个文件足足4000多行源代码，加上剪不断、理还乱的DocumentsWriter，为了平衡CPU和IO的DocumentsWriterPerThread，以及管理DWPT的pool，都是巨大的文件。我能够理解，为了不让IW成为上帝类，而分理处DW和DWPT的良苦用心。不过，这丝毫抵不上那些为了扩充功能，而不断向IW加上的“海量”代码。其实像有些功能抽的就比较好，比如说segments的抽象，比如说对于删除的特殊处理，还有flush的精细控制。如果能对IW、DW以及DWPT进一步的细分，对于将来维护和扩展代码更好。Lucene的邮件列表里面，大概几年前有人提过这件事，不过后来估计也就不了了之了。IW本身大量的同步机制其实就暴露了其内部数据的离心力，比如说关闭的状态、flush的状态，commit的状态等等。我会持续加以关注的。