# ORM에 대하여 
### ORM이란?
ORM은 Objective-Relational Mapping의 약자로 객체와 관계형 데이터를 매핑하기 위한 기술이다.  
객체지향언어와 관계형 데이터 베이스 사이의 패러다임 불일치가 존재하기 때문에 매핑이 필요로 하게 된다.  
이러한 패러다임 불일치 때문에 더 많은 코드를 작성해야하며 이러한 코드들은 반복적이며 실수가 잦은 작업이 된다.   
결국에는 객체지향적인 설계에 집중하기 힘들게 된다. 이러한 문제를 해결하기 위해  ORM이 등장했다. 
![image](https://user-images.githubusercontent.com/110332047/185833006-0ec3d4a1-c116-49ed-8d18-653b8ac970ae.png).  
(출처: https://medium.com/@emccul13/object-relational-mapping-9d84807f5536)

#### 패러다임 불일치
객체와 관계형 데이터 간 패러다임 불일치가 일어나게 되는 이유중 하나는 두가지의 목표와 동작방식이 다르기 때문이다.  
* 객체 지향
  - 필드와 메서드 등을 묶어서 객체로 잘 만들어 사용하는 것이 목표
  - 객체 지향 프로그래밍은 추상화, 캡슐화, 정보은닉, 상속, 다형성 등 시스템 복잡성을 제어할 수 있는 다양한 장치들을 제공

* 관계형 데이터베이스
  - 데이터를 잘 정규화하여 보관하는 것이 목표

___ 
### JPA
JPA는 Java Persistance API의 약자로, 자바 ORM 기술에 대한 API 표준 명세이다.  JPA는 인터페이스의 모음으로 대표적인 프레임워크로  
하이버네이트(Hibernate) 가 있다. JPA는 어플리케이션과 JDBC 사이에서 동작을 하는데,  개발자가 JPA를 사용하면 JPA 내부에서
JDBC API를 사용해 SQL을 호출하여 Database와 통신한다. 
![image](https://user-images.githubusercontent.com/110332047/185833725-cef33fdb-a675-4d23-a36f-91a66e386476.png)  
___
### Spring Data JPA
Spring Data JPA는 Spring framework에서 JPA를 보다 편리하게 사용할 수 있도록 지원하는 모듈이다. Spring Data JPA의 목적은 예상가능하고 
반복적인 코드들을 대신 작성해줘서 코드를 줄요주는 것이다. 이는 JPA를 한단계 추상화 시킨 Repository라는 인터페이스를 제공함으로써 이루어진다.
Spring Data JPA는 항상 하이버네이트와 같은 JPA Provider가 필요하다는 것이 특징이다. 

![image](https://user-images.githubusercontent.com/110332047/185839257-5add5688-fea5-4b4f-b535-01e248276213.png)
(출처 : 스프링부트와 aws로 혼자 구현하는 웹서비스)


출처: https://doing7.tistory.com/105
