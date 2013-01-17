---
title: Web Storage
layout: page
category: bom
date: 2012-12-28
modifiedOn: 2012-12-28
---

## 概述

这个API使得网页可以在浏览器端储存数据，在多个网页之间分享。它分成两类：sessionStorage和localStorage。

sessionStorage保存的数据用于浏览器的一次会话，当会话结束（通常是该窗口关闭），数据被清空；localStorage允许浏览器长期保存网页数据，下一次访问的时候，网页可以直接读取以前保存的数据。这两个API很像cookie机制的强化版。

与cookie一样，它们也受同域限制。某个网页存入的数据，只有同域下的网页才能读取。它们能够动用的存储空间的下限是5MB，上限视浏览器而定，通常大大高于5MB。

通过检查window对象是否包含sessionStorage和localStorage属性，可以确定浏览器是否支持这两个API。

{% highlight javascript %}

function checkStorageSupport() {
 
  //sessionStorage
  if (window.sessionStorage) {
    return true;
  } else {
    return false;
  }
   
  //localStorage
  if (window.localStorage) {
    return true;
  } else {
    return false;
  }
}

{% endhighlight %}

## 存入/读取数据

sessionStorage和localStorage保存的数据，都以“键值对”的形式存在。每一项都有一个键名，以及相对应的数据。这里需要注意，所有的数据都是以文本格式保存。

存入数据使用setItem方法。它接受两个参数，第一个是键名，第二个是保存的数据。

{% highlight javascript %}

window.sessionStorage.setItem("key","value");

window.localStorage.setItem("key","value");

{% endhighlight %}

读取数据使用getItem方法。它只有一个参数就是键名。

{% highlight javascript %}

var valueSession = window.sessionStorage.getItem("key");

var valueLocal = window.localStorage.getItem("key");

{% endhighlight %}

clear方法用于清除所有保存的数据。

{% highlight javascript %}

window.sessionStorage.clear();

window.localStorage.clear(); 

{% endhighlight %}

## storage事件

当储存的数据发生变化时，会触发storage事件。我们可以指定这个事件的回调函数。

{% highlight javascript %}

window.addEventListener("storage",onStorageChange);

{% endhighlight %}

回调函数接受一个event参数。这个event对象的key属性，保存发生变化的键名。

{% highlight javascript %}

function onStorageChange(e) {

     if(e.key == "key") {
          alert(e.key);    
     }
    
}

{% endhighlight %}

event对象的属性还有：

- oldValue：更新前的值。如果该键为新增加，则这个属性为null。
- newValue：更新后的值。如果该键被删除，则这个属性为null。

## 参考链接

-  Ryan Stewart，[Introducing the HTML5 storage APIs](http://www.adobe.com/devnet/html5/articles/html5-storage-apis.html)