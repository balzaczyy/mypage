---
title: RFT经验技巧
date: '2005-08-01'
description:
categories:
- 技术
tags:
- RFT

---

在IBM实习了的这两个礼拜一直在做测试，所以对RFT(Rational Functional Tester)的使用也有了一点积累，先总结一下。

## WebUI测试中对象属性的获取

在Web环境下，对象属性的获取必须分情况考虑，而不是直接调用.getProperty方法。对于静态对象属性，只要考虑对象捕捉失败的情况就可以了，但是对于动态对象属性（即依赖浏览器载入的属性）必须考虑载入时间，永远要假设最坏情况（比如服务器在美国，或者真的存在错误），同时对于不同层次的调用，还要提供可选择的异常处理和日志记录功能，代码如下：

	public String getPropFromObj(
	    TestObject to,
	    String prop,
	    int TTL,
	    boolean doLog) throws Exception {
 	  if (TTL == 0) return ""; //Time to Live
 	  assert (to != null);
 	  assert (to.getProperties().containsKey(prop));
 	  try {
  	    String text = to.getProperty(prop).toString().trim();
  	    if (text == null || text.length() == 0) {
   	      return getPropFromObj(to, prop, TTL-1, doLog);
  	    }
  	    return text;
 	  } catch (Exception e) {
  	    if (TTL > 1) return getPropFromObj(to, prop, TTL-1, doLog);
  	    String msgErr = "Can't get property(" + prop + ") from object " + to.getNameInScript();
  	    if (doLog) {
   	      logException(e);
  	      logError(msgErr);
  	    }
  	    e.printStackTrace();
  	    System.err.println(msgErr);
  	    throw e;
 	  }
	}

在此基础上，还要考虑速度过快，使得先前的属性被读出的情况，还有就是如果预先知道正确的属性值，可以提供给方法以加快判断速度：

	private String lastValue = null;
	public String getPropFromObjExt(
	    TestObject to,
	    String prop,
	    int TTL,
	    String curValue) throws Exception {
	  if (TTL == 0) return "";
	  assert (to != null);
	  assert (to.getProperties().containsKey(prop));
	  try {
	    while (TTL-- > 0) {
	      String text = getPropFromObj(to, prop, 1, false);
	      if (text.equals(curValue)) return curValue;
	      if (text.equals(lastValue)) continue;
	      if (text.length == 0) continue;
	      lastValue = text;
	      return text;
	    }
	  } catch (Exception e) {
	    if (TTL > 1) return getPropFromObj(to, prop, TTL, doLog);
	    String msgErr = "Can't get property(" + prop + ") from object " + to.getNameInScript();
	    if (doLog) {
	      logException(e);
	      logError(msgErr);
	    }
	    e.printStackTrace();
	    System.err.println(msgErr);
	    throw e;
	  }
	}

还可以有许多的改进，我暂时没有想到，但是Web环境下面真的要当心哦。
 
## 全球化中的语言测试

这也是今天学到的，利用Character.UnicodeBlock.of(Char c)能够判断c是属于什么字符集的，但是光凭字符集还是没有办法判断语言系统（如日语、繁体中文、阿拉伯语等），大公司做的软件都要求任何平台、任何语言、任何浏览器和任何环境都能正确工作，所以语言是比较重要的。BC总结了一下各种语言系统和字符集的关系，代码的话明天再贴。
