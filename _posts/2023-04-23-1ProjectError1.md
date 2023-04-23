---
layout: single
title:  "[Java] Error preloading the connection pool"
categories: Java-1차ProjectError
toc: true
---

<br/><br/>

# Error preloading the connection pool #

![error1](https:/images/2023-04-23-1차프로젝트오류/connection/Error%20preloading%20the%20connection%20pool.png)
<br/><br/>

원인 : 코드를 작성하면서, 오류발생이 계속 발생하였더니 close가 수행되지 않아서 커넥션 풀에 계속 싸이게 됨. 그래서 커넥션 풀이 다 찼기 때문에 발생하는 오류
<br/><br/>

해결 : jvm(이클립스)을 다시 실행. 
