---
layout: default
title: "EOFException오류"
tags: Tomcat
---

EOFException 오류
---------------

<br>
<<오류 : 심각: Exception loading sessions from persistent storage >>

java.io.EOFException: 톰캣을 종료할때 세션을 저장해 두었다가 restart 할때 저장된 세션을 복구할때 실패할 경우 발생하는 에러

해결방법
1. 톰캣설치위치/work/catalina/ 이하 디렉토리에서 SESSIONS.ser 파일을 삭제
2. Context.xml 파일에 <Manager className="org.apache.catalina.session.StandardManager" pathname=""/> 추가해 주기

----------------------------------------------------------------------------------------------------------------

IOException while loading persisted sessions: java.io.EOFException
톰캣은 persist session을 저장 할 수 있다고 한다. 
persist session은 톰캣을 shutdown, restart 할때 생성이 되고, start는 삭제된다고 한다.
그런데 이러한 작업을 실패했을때에 java.io.EOFException이 발생한다는 것이다.
해결방법은 그냥 Work Directory에서 "session.ser" 파일을 찾아서 삭제하고 다시 실행시키면 해결이 된다고 한다.

"SESSION.SER", ".SER"의 의미는 SERIALIZED OBJECT FILE이다.

출처: https://planmaster.tistory.com/97 [떵짜루의 끄적임...]