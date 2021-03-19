20210317\_TIL
==============
Spring 입문 1화_ Layerd Architecture는 Spring의 핵심
----------------------------------------


-   IntelliJ로 Java Spring으로 개발할 개발 환경을 설정해보았다.

-   Java 언어의 기초 문법을 배웠다. 알고리즘 주차때 파이썬이라는 프로그래밍 언어를 충분히 익혔던 터라, 기본 개념 학습은 수월했다. 

-   딱 어제 알고리즘 주차를 마치며 Class 구현 능력이 미흡하다고 언급했는데, 오늘 강의를 들으며 Class 개념을 처음부터 꼼꼼히 잡으며 구현까지 연습해볼 기회가 있었다. (굿 타이밍!) Java로 클래스를 구현하고 멤버변수를 선언하고, 클래스 내 메소드들을 만들어보았다. 이러면 나중에 Python으로 다시 다뤘을 때 이해가 더 쉬울 듯 하다.

-   Spring Framework의 주 Layer인 Controller, Service, Repository Layer를 간단하게 구현해 보았다.  DB에 접근하는 Repository Layer 부터 시작해 클라이언트의 요청을 전달받고 응답하는 Controller Layer까지 다루었다. 각각의 Layer에 코드들을 집어넣으며 왜 이 코드가 이 Layer에 있어야 하는지에 대한 감을 잡으려 노력했다.

-   Repository Layer를 다루는 과정에서 RDBMS 개념을 학습하고 작동 명령어인 SQL에 대해 간단히 알아보았다. 이후 자바 명령어를 SQL로 번역해주는 JPA까지 한번 빠르게 다루어 보았다.

---


### **1\. IntelliJ Java 개발 환경 설정**

아래의 사진과 똑같이 설정해주면, Java Spring으로 서버를 띄울 수 있다.

![개발환경](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FthryE%2Fbtq0AId50rj%2FyKbncNzYuf4WjZGVxo0K00%2Fimg.png)

![개발환경](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRqFA5%2Fbtq0vP63akz%2FthO9xxb3fk4f9cJ87H2fm1%2Fimg.png)

![개발환경](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbw67d6%2Fbtq0ApTmjHo%2FAwM47dSFmAa521MMXke521%2Fimg.png)

---


### **2\. Java 언어 문법 공부**

-   변수, 기초 문법
-   숫자 - int, float, Long
-   문자 - String
-   참거짓 - boolean
-   배열 - List
-   임포트
-   주석, 정렬 단축키
-   메소드
-   반복문 - for
-   조건문 - if
-   클래스 - 생성자, Getter, Setter

배우면서 파이썬 언어와 비슷한 흐름을 가지고 있으나, 구현에 세세하게 차이가 있는 듯 하였다. 기본 문법 안에서는 파이썬이 가지고 있는 기능들과 다른 기능들이 없었다. 따라서 디테일하게 파이썬과 다른 점들에 집중하며 강의를 수강하였다. 리스트 길이 len은 자바에서 size로 구현하고, 변수는 자료타입을 먼저 선언한다던지와 같은 형식적인 차이에 빨리 익숙해질 수 있도록 말이다.

추가적으로 자바의 정석 저자가 하는 자바 문법 강의가 유튜브에 올라와있던데, 틈틈히 보아두도록 해야겠다.

---


### **3\. 클래스**

클래스는 정보를 묶기 위해 사용한다. 클래스 내에서 정보들을 분류해 담기 위해 멤버 변수를 사용한다. 예를 들어 People이라는 클래스가 있다면, 그 안에서 굴러다니는 정보들을 name, age, address 등을 멤버 변수로 선언한다. 이렇게 함으로서 정보를 보다 체계적으로 관리할 수 있다. name, age, address 을 만들어주는 각각의 붕어빵틀을 생성해, 새로운 데이터를 만날 때마다 name 붕어빵1, age 붕어빵1, address 붕어빵1로 찍어서 관리한다. 

그리고 항상 생성자 개념이 헷갈렸는데 감이 좀 잡혔다. 어떠한 정보를 이 People이라는 클래스에 담아 People 클래스가 가지고 있는 분류 기준으로 나누어 관리하고 싶을 때, 클래스 변수를 새롭게 만들어야 한다. 그러기 위해서는 클래스 안에 클래스 명과 똑같은 이름을 가진 빈 메소드를 만들어주어야 하고, 이를 "생성자"라고 부른다.

오늘 private과 public 변수 까지 다루었다. public 변수로 설정하면 누구든지 Domain data들을 바꿀 수 있게 되어 데이터 관리에 구멍이 생긴다. 따라서 아무나 데이터를 바꿀 수 없도록 멤버 변수를 private으로 설정할 수 있다. 이후 관리는 getter와 setter에 해당하는 method들을 public으로 만들어 method를 통해서만 데이터를 변경할 수 있도록 관리할 수 있다.

(그런데 이 getter와 setter 변수명은 거의 통상적으로 이름이 지어지던데, 그럼 사실상 아무나 데이터를 변경할 수 있는것 아닌가...? 라는 의문이 든다. )

---


### **4\. Controller, Service, Repository Layer - Layered Architecture**

![사진](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbqx7OO%2Fbtq0zeLNS6p%2FAmsYTW7avUA2Q6A59OxfpK%2Fimg.png)

****1) Controller Layer (Presentation Layer)****

\- 클라이언트가 이용하는 End Point

\- 클라이언트의 요청을 전달받고 응답한다

**2) Service Layer (Business Layer)**

\- 기능을 수행한다 (비즈니스 로직을 수행한다)

\- transaction을 수행한다

**3) Repository Layer (Data Acess Layer)**

\- 데이터 베이스에 연동되어 데이터의 저장과 조회를 담당한다

\- JPA가 이 곳에서 불러와진다.


**이 세 Layer들의 유기적 결합을 얼마나 잘 이해하는지가 Spring 사용에 있어서 가장 중요할 것 같다는 생각이 든다. 각 Layer들 마다 각각의 책임이 있다고 생각한다. 경험상, 일을 할 때에도 수많은 업무를 적절한 책임자에게 돌아가게끔 하는 게 일을 잘 하는 방법이었다. 그렇기에 Spring에서도 이 세 친구들의 역할을 잘알아야, 일을 잘 분배해 줄 수 있기 때문에 역할을 명확히 알아야 하겠다.**  

아직 각 Layer에 코드들을 넣어 이들간의 유기적 연결을 경험한 횟수가 압도적으로 적기 때문에 어떠한 코드들이 어느 Layer에 들어가서 어떤 작용을 하는지는 아직 명확히 알 지 못한다. 때문에 이번 주차 Spring 학습을 진행하면서 가장 주의를 기울여야 할 부분이다. 간단하게 서비스를 만들어보면서 어떤 기능을 하는 코드가 어느 Layer에 들어가 어느 Layer들과 연결되어 있는지를 의식적으로 고려하며 학습을 진행해야 겠다. **다음주 목요일에는 Controller Layer, Service Layer, Repository Layer들 안에 어떤 코드를 넣어야 하고 어떤 Layer와 연결해야 하는지 명확히 아는 것이 목표다.**  

![사진](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdYyvc%2Fbtq0zuU5XU4%2FrL6jAyKXZPzSXI4FBFNv90%2Fimg.png)

생성 폴더를 통해서도 Spring의 뼈대에 대한 감을 잡아볼 수 있겠다.