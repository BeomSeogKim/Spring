#Embedded Type(임베디드 타입)
임베디드 타입은 새로운 값 타입을 직접 정의할 수 있다. JPA는 이러한 타입을 임베디드 타입이라고 한다.   
주로 기본 값 타입을 모아서 만들기 때문에 복합 값 타입이라고도 한다. 임베디드 타입의 경우 int, String과 같은 값 타입이다. 

만약 회원 Entity가 다음과 같을 때 
![IMG_69A12ACEB6DA-1](https://user-images.githubusercontent.com/110332047/186930749-18ecfd61-5b22-4157-813a-1a7efd5927a3.jpeg)   
임베디드 타입을 사용하면 다음과 같이 표현이 가능하다.  
![IMG_08686FC97805-1](https://user-images.githubusercontent.com/110332047/186931302-79ee50e4-f34e-43ea-a77b-cc9bf85f356a.jpeg)   
또한 Member 와 Embedded type 간 관계는 다음과 같이 재정의 된다. 
![IMG_096752C49F79-1](https://user-images.githubusercontent.com/110332047/186932301-0a9ea196-373d-4b03-9727-c64a518b906e.jpeg)   
___
### 임베디드 타입 사용법
임베디드 타입의 사용법은 간단하다.
* @Embeddable: 값 타입을 정의하는 곳에 표시
* @Embedded: 값 타입을 사용하는 곳에 표시
* 기본 생성자는 필수임

### 임베디드 타입의 장점
* 재사용성
* 높은 응집도
* 해당 값 타입만 사용하는 의미 있는 메소드를 만들 수 있음
* 임베디드 타입을 포함한 모든 값 타입은, 값 타입을 소유한 엔티티에 생명주기를 의존함

### 임베디드 타입과 테이블 매핑의 관계 
![IMG_484B1C658E3F-1](https://user-images.githubusercontent.com/110332047/186934594-39b8d4e6-501c-4304-bbfc-60510022467b.jpeg)  
* 결국 임베디드 타입은 엔티티의 값일 뿐이다. 
* 임베디드 타입을 사요하기 전과 후에 매핑하는 테이블은 같다.
* 객체와 테이블을 아주 세밀하게 매핑하는 것이 가능하다.

