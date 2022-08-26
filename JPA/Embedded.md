#Embedded Type(임베디드 타입)
임베디드 타입은 새로운 값 타입을 직접 정의할 수 있다. JPA는 이러한 타입을 임베디드 타입이라고 한다.   
주로 기본 값 타입을 모아서 만들기 때문에 복합 값 타입이라고도 한다. 임베디드 타입의 경우 int, String과 같은 값 타입이다. 

만약 회원 Entity가 다음과 같을 때 
![IMG_69A12ACEB6DA-1](https://user-images.githubusercontent.com/110332047/186930749-18ecfd61-5b22-4157-813a-1a7efd5927a3.jpeg)   
임베디드 타입을 사용하면 다음과 같이 표현이 가능하다.  
![IMG_08686FC97805-1](https://user-images.githubusercontent.com/110332047/186931302-79ee50e4-f34e-43ea-a77b-cc9bf85f356a.jpeg)   
또한 Member 와 Embedded type 간 관계는 다음과 같이 재정의 된다. 
