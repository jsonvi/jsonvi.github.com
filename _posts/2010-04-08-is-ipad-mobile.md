---
layout: post
title: ipad mobile? 是手机? 不... 
category: web
---

使用UA string 判断 浏览器 是jquery的御用方法
<!-- end_preview -->

{% highlight javascript %}

uaMatch: function( ua ) {
  var ret = { browser: "" };

  ua = ua.toLowerCase();

  if ( /webkit/.test( ua ) ) {
    ret = { browser: "webkit", version: /webkit[\/ ]([\w.]+)/ };

  } else if ( /opera/.test( ua ) ) {
    ret = { browser: "opera", version:  /version/.test( ua ) ? /version[\/ ]([\w.]+)/ : /opera[\/ ]([\w.]+)/ };

  } else if ( /msie/.test( ua ) ) {
    ret = { browser: "msie", version: /msie ([\w.]+)/ };

  } else if ( /mozilla/.test( ua ) &amp;&amp; !/compatible/.test( ua ) ) {
    ret = { browser: "mozilla", version: /rv:([\w.]+)/ };
  }

  ret.version = (ret.version &amp;&amp; ret.version.exec( ua ) || [0, "0"])[1];

  return ret;
}

{% endhighlight %}

这方法很方便，也很脆弱，不信的话，可以看看我们亲爱的ipad...

随着ipad的出现，浏览网页的方式似乎出现了新的路，介于手机与电脑之间的，给人一种“特仑苏”的感觉，尤其是当你看到了ipad的UA string 时

<code>
Mozilla/5.0 (iPad; U; CPU OS 3_2 like Mac OS X; en-us) AppleWebKit/531.21.10 (KHTML, like Gecko) Version/4.0.4 Mobile/7B334b Safari/531.21.10
</code>

请注意后面的Mobile字样！！！
<blockquote>是手机吗？不...
是ipad，不是所有移动设备都叫ipad</blockquote>
诚然，一句

{% highlight javascript %}
navigator.userAgent.match(/iPad/i) != null;
{% endhighlight %}

可以解决问题

但是，那些判断UA string 为mobile的网站呢？
不妨想象一下，那些使用着“大屏幕”的ipad用户访问 www.某网站.com ，却被直接转到针对手机设计的 m.某网站.com 时的心情...

没有标准的useragent ， 在如今的web海域中，还要漂泊多久？
