# 싱글톤(Singleton)
### 웹 어플리케이션의 작동방식 
웹 어플리케이션의 경우 보통 고객 여러명이 동시에 요청을 한다. 
![image](https://user-images.githubusercontent.com/110332047/186419831-f3d22728-00a8-4b7c-b14f-4a3cd648f412.png)   
이러한 경우 고객이 요청을 할 때마다 객체가 생성되고 소멸되어 메모리 낭비가 심하다는 단점이 존재한다. 
### 이러한 문제를 해결하기 위해 싱글톤 패턴을 사용한다.
___
## 싱글톤 패턴 
* 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴.
* private 생성자를 사용해 외부에서 임의로 new 키워드를 사용하지 못하도록 조작해줘야함. 
```java
public class SingletonService{

  // static method를 사용해 객체를 1개만 생성
  private static final SingletonService instance = new SingletonService();
  
  // public 으로 공개해 객체 인스턴스가 필요하다면 static method를 통해서만 조회하도록 허용
  public static SingletonService getInstance(){
    return instance;
  }
  
  // 생성자를 private으로 선언해 외부에서 New 키워드를 사용한 객체 생성을 못하게 막자.
  private SinglettonService(){
  }
}
```
이 경우 객체 인스턴스가 필요하면 오직 getInstance() 메서드를 사용해서 조회할 수 있으며 호출하면 같은 인스턴스를 반환한다.  
하지만 이러한 싱글톤 패턴은 다음과 같은 문제점이 존재한다.
### 싱글톤 패턴의 문제점
* 싱글톤 패턴을 구현하는 코드가 많이 들어감.
* 의존 관계상 클라이언트가 구체 클래스에 의존 
* 테스트하기 어려움
* 내부 속성을 변경하거나 초기화 하기 어려움
* 유연성이 떨어짐
이러한 문제점을 해결하기 위해 생겨난 것이 스프링 컨테이너다.
___
## 싱글톤 컨테이너
싱글톤 패턴의 문제점을 해결함과 동시에 객체 인스턴스를 싱글톤으로 관리할 수 있는 방법.
### 싱글톤 컨테이너의 특징
* 싱글톤 패턴을 적용하지 않아도 객체 인스턴스를 싱글톤으로 관리함
* 스프링 컨테이너가 이러한 싱글톤 컨테이너 역할을 함 
* 싱글톤의 단점을 해결하면서 객체를 싱글톤으로 유지 할 수 있음
  - 싱글톤 패턴을 위한 지저분한 코드가 필요 없음
  - DIP, OCP, private 생성자로 부터 자유롭게 싱글톤을 사용 할 수 있음

싱글톤 컨테이너의 경우 다음과 같이 호출한다.
```java

  ApplicationContext ac(이름변경가능) = new AnnotationConfigApplicationContext(AppConfig.class(내가 생성한 config클래스이름 적기));
```
위와 같이 코드르 짜게 되면 다음과 같이 요청에 대한 해결이 가능하다. 
![image](https://user-images.githubusercontent.com/110332047/186422651-f060fc21-c9c2-4b5d-9536-dd4036e753b4.png)   

### 싱글톤 방식의 주의점 
* 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태를 유지하면 안된다.
* 무상태로 설계를 진행해야함.
  - 특정 클라이언트에 의존적인 필드가 존재하면 안됨
  - 특정 클라이언트가 값을 변경할 수 있는 필드가 존재하면 안됨
  - 가급적이면 읽기만 가능하도록 설계
  - 필드 대신에 자바에서 공유되지않는 지역변수, 파라미터, ThreadLocal 등을 사용해야함. 
___
## @Configuration 의 역할 
보통 AppConfig를 짜게되면 
```java
   @Bean
    public MemberService memberService() {
        return new MemberServiceImpl(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
```
위와 같이 설계하게 되는데 다중 호출이 되는 경우가 발생하지 않을까? 라는 걱정이 생기게 된다. 
이러한 경우 ConfigClass에 어노테이션 @Configuration을 사용하면 스프링이 알아서 싱글톤 패턴을 유지하게 해준다.
==> 싱글톤 패턴을 사용하기 위해 Config class에는 **@Configuration** 을 꼭 붙여주도록 하자. 


