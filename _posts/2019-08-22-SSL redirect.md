---
layout: default
title: "SSL redirect"
tags: Tomcat
---

SSL redirect
---------------

<br>
servcer.xml 설정

```
<Connector port="80" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="443" />

<Connector port="443" protocol="org.apache.coyote.http11.Http11Protocol"
           maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
           clientAuth="false" sslProtocol="TLS"
           keystoreFile="conf/domain.jks" keystorePass=".jks 비밀번호" />
````

		   
----------------------------------------------------------------------------		   
		   
web.xml 설정
```
<security-constraint>
    <web-resource-collection>
        <web-resource-name>SSL Forward</web-resource-name>
        <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
        <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
</security-constraint>


특정소스는 http, https 모두 가능하도록 처리 / 하단은 images, css 가능처리
<security-constraint>
    <web-resource-collection>
        <web-resource-name>HTTPS or HTTP</web-resource-name>
        <url-pattern>/images/*</url-pattern>
        <url-pattern>/css/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
        <transport-guarantee>NONE</transport-guarantee>
    </user-data-constraint>
</security-constraint>
```