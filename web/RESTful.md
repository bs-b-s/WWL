## 시작하기 전에
잘 알려져 있지만 뭔가 미묘하게 잘 모르는, 팀 프로젝트를 하는 상황이고 코드 리뷰 등을 할 때 
> "그 부분은 뭔가 REST스럽지 않은데요?"

라고 팀원이 말한다면, 
> **"이런게 REST API 인데요?"** 
 
라고 반박은 해주고 싶은데 본인도 사실 잘 모르는 경우가 많다.

이렇게 자신이 매일 개발하는 API의 정확한 정의와 사용법 모르는 개발자들이 대다수다.

## REST
**RE**presentational <br/>
**S**tate<br/>
**T**ransfer<br/>

### REST란?
컴퓨터 시스템간의 상호 운영성을 제공하는 방법 중 하나이다.

### WEB(1991)
> "어떻게 인터넷에서 정보를 공유할 것인가?" (인터넷만 존재하는 시기)

가 기존 인터넷들의 문제점들 중 하나였다. 이에 대한 해답으로 **WEB**이 등장함

월드 와이드 웹(WWW)이 [팀 버너스-리](https://ko.wikipedia.org/wiki/%ED%8C%80_%EB%B2%84%EB%84%88%EC%8A%A4%EB%A6%AC?tableofcontents=1)에 의해 탄생
<br/>
<img width="257" alt="스크린샷 2022-06-09 오전 8 13 24" src="https://user-images.githubusercontent.com/94087228/172732741-215f926f-8639-4da7-97d4-69b78a3c786b.png">

> "정보들을 하이퍼텍스트로 연결하자"
> * 표현 형식 : HTML
> * 식별자 : URI
> * 전송 방법 : HTTP

위의 명세를 바탕으로 HTTP/1.0(1994~1996) 프로토콜을 개발하게 됨(_기존에 사용하고 있던 HTTP에서 더욱 명세에 기능을 더하고 기존의 기능을 고친_)

#### Roy T. Fielding(1994~1996)
> "어떻게 하면 기존에 HTTP로 구축되어 있던 웹들과 호환성의 문제가 생기지 않게 개발할 수 있을까?

### HTTP Object Model(1994)
Roy T. Fielding이 제기했던 문제점들을 해결할 수 있는 방안

## REST(1998, 2000)
(1998)Roy T. Fielding이 Microsoft Research에서 HTTP Object Model을 **REST**이라는 이름으로 발표

(2000)이 때 당시 Roy T. Fielding은 대학원생이였으며, 이를 박사 [논문](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)으로 발표함

이 때 발표한 논문이 우리가 오늘날 알고 있는 REST를 정의하는 논문임

***

## API
인터넷상에 API라는 것이 만들어지기 시작함

1998년에 마이크로소프트가 **XML-RPC**라는 원격으로 다른 시스템의 메서드를 호출할 수 있는 프로토콜을 만듦 -> **SOAP**

### Salesforce API(2000) - **SOAP 형태** - 매우 복잡하고 어려움
<br/>

![image](https://user-images.githubusercontent.com/94087228/172734847-e46bed92-c7d8-4445-862f-39b996360712.png)

### filckr(2004) - **SOAP 형태 && REST 형태** - SOAP보다 매우 쉽고 간결해짐
<br/>

![image](https://user-images.githubusercontent.com/94087228/172738444-9e3e7e87-d255-4846-b686-ff02bc1a2a10.png)

### 사용자들이 생각한 SOAP와 REST의 차이점
|SOAP|REST|
|------|---
|복잡하고|단순하고|
|규칙많고|규칙적고|
|어려운|쉬운|

### 결과
<img width="524" alt="스크린샷 2022-06-09 오전 9 21 16" src="https://user-images.githubusercontent.com/94087228/172738712-f40aecfb-ee74-43a3-ac9f-2ba76355520e.png">

월드 와이드 웹(WWW)이 REST API로 정착을 하기 위해서

### CMIS 등장(2008)
* [CMS](https://ecommerce-platforms.com/ko/glossary/content-management-system-cms)를 위한 표준
* EMC, IBM, Microsoft 등이 함께 작업
* **REST 바인딩 지원**

> Roy T. Fielding : "CMIS에 **REST**는 존재하지 않는다."

### Microsoft REST API Guidelines(2016)
마이크로소프트가 REST API에 대한 구체적인 [가이드라인](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md) 제시
* [URI는 https://{serviceRoot}/{collection}/{id} 형식이어야 한다.](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md#92-serialization)
* [GET, PUT, DELETE, POST, HEAD, PATCH, OPTIONS를 지원해야 한다.](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md#74-supported-methods)
* API [버저닝](https://wiserloner.tistory.com/466)은 [Major.minor로 하고 URI에 버전 정보를 포함시켜야 한다.](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md#121-versioning-formats)
* [쉽게 이해할 수 있도록 일관성을 지켜야한다.](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md#7-consistency-fundamentals)
* [기본 유형에 대한 JSON 형식의 기본 값은 RFC4627 규칙에 따라 JSON으로 직렬화되어야 한다.](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md#11-json-standardizations)
* ....

> Roy T. fielding : "이것은 **REST API**가 아니라, **HTTP API**라고 해야한다."

***

> Roy T. fielding : "이런것들(CMIS, Microsoft REST API Guidelines)을 REST라고 부르려면 **"hypertext-driven"** 이어야 하며, REST API를 위한 최고의 버저닝 전략은 버저닝을 안 하는 것이다."
