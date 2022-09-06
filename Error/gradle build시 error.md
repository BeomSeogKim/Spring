# Javax.annotation.meta.When 에러

## 문제 발생 에러 코드
![스크린샷 2022-09-06 오후 3 00 11](https://user-images.githubusercontent.com/110332047/188582666-ead36872-d913-4010-9176-062ac3eb1bd8.png)

## 문제 발생 상황 
새로운 코드 추가 후 build시에 위의 그림과 같이 javax.annotation.meta.When 에러 발생 
build가 안되는 것은 아니었지만 찜찜한 마음에 구글링을 진행함. 

## 해결 방법 
build.gradle에 추가적으로 의존성 주입을 해주면 된다.   

build.gradle의 경우 
```java
dependencies {

  implementation 'com.google.code.findbugs:jsr305:3.0.2' 
}
```
추가    

pom.xml의 경우 

```java
<dependency>
        <groupId>com.google.code.findbugs</groupId>
        <artifactId>annotations</artifactId>
        <version>3.0.1</version>
    </dependency>
```
추가 하면 해결 된다. 

