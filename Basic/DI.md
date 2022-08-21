# DI(Dependency Injection)
### DI의 정의 
DI는 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴으로 인터페이스를 사이에 둬서 클래스 레벨에서는 
의존 관계가 고정되지 않도록 하고 런타임 시 관계를 동적으로 주입해 유연성을 확보하고 결합도를 낮추게 하는 방식이다.  
의존성이란 한 객체가 다른 객체를 사용할 때 의존성이 있다고 한다.
```java
public class Store {

    private Pencil pencil;

}
```
이 경우 Store 객체가 Pencil 객체에 의존성이 있다고 표시한다.
___
### DI가 필요한 이유
예를 들어 다음과 같은 클래스가 있다고 하자.
```java
public class Store {

    private Pencil pencil;

    public Store() {
        this.pencil = new Pencil();
    }

}
```
이러한 코드는 다음의 문제점을 가진다.
* 두 클래스가 강하게 결합되어 있음.
* 객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐.

**두 클래스가 강하게 결합되어 있음**
위와 같은 클래스는 강하게 결합되어 있어 Store에서 Pencil이 아닌 Food와 같은 다른 상품을 판매하려고  한다면 
Store 클래스의 생성자 변경이 필요하다. 즉, 유연성이 떨어진다. 이러한 경우 확장성이 떨어지기 때문에 좋은 코드는 아니다.

**객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐**
올바른 객체지향적 설계의 경우 클래스 간에 관계가 맺어지는 것이 아닌 객체들 간에 관계가 맺어져야 한다. 
객체들 간에 관계가 맺어진다면 다른 객체의 구체 클래스는 알지 못하더라도 인터페이스의 타입으로 사용할 수 있기 때문이다.

___
### 의존성 주입을 통한 문제 해결 
위와 같은 문제를 해결하기 위해서는 다형성이 필요하다. 여러가지 제품을 하나로 표현하기 위해서는 Product 라는
인터페이스가 필요하다.
```java
public interface Product{
}

public class Pencisl implements Product{
}
```
그 후 Store와 Pencil이 강하게 결합되어 있는 부분을 제거해야한다. 이를 제거하기 위해서는 외부에서 상품을 
주입(Injection) 받아야 한다. 
```java
public class Store{
  private Product product;
  
  public Store(Product product){
    this.product = product;
  }
}
```
여기서 DI 컨테이너가 필요로 하게 되는데 Store에서 Product 객체를 주입하기 위해서는 필요한 객체를 생성
해야하며, 의존성이 있는 두 객체를 연결하기 위해 한 객체를 다른 객체로 주입시켜야 하기 때문이다. 
DI 컨테이너는 다음과 같다.
```java
public class BeanFactory{
  public void store(){
    Product pencil = new Pencil();
    
    Store store = new Store(pencil);
    }
  }
```
___

출처 https://mangkyu.tistory.com/150
