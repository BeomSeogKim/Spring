# 스프링 웹 개발 기초
* 정적 컨텐츠
* MVC와 템플릿 엔진
* API
___
## 정적 컨텐츠
![IMG_1A7704876C0C-1](https://user-images.githubusercontent.com/110332047/183669303-f48dd970-988c-47ee-81ee-f65a2c0f2f5a.jpeg)
정적 컨텐츠란 html을 그대로 서버에 전달하는 것을 말함.  
정적 컨텐츠의 경우 우선적으로 스프링 컨테이너에 hello-static 관련 컨트롤러가 있는지를 찾음.  
그 이후 컨트롤러가 없다면 resources안에 있는 static/hello-static.html을 찾아서 반환해주는 구조.

___
## MVC와 템플릿 엔진
![IMG_970AC2577C0E-1](https://user-images.githubusercontent.com/110332047/183671952-b3584d93-8fb9-4981-81f0-0b0663ee7e45.jpeg)
Spring MVC는 Model, View, Controller 세가지 구성요소를 사용해 html을 서버에서 로그래밍 하여 동적으로 내려주는 것을 말한다.  
Model과 Controller의 경우 비즈니스 로직에 초첨을 두고, View 의 경우 화면을 그리는 것에 초점을 둔다.
___
## API
![IMG_6001E6F24A39-1](https://user-images.githubusercontent.com/110332047/183675059-4a4707cd-9ef5-4673-a720-46754f380a5b.jpeg)
API의 경우 json 포맷 혹은 XML 포맷으로 데이터를 주고받고 한다.   
API는 Application Programming Interface의 약자.   
> 여기서 Application Programming : 응용 프로그래밍   
> Interface : 서로 다른 두개의 시스템이 정보를 주고 받도록 이어주는 경계를 의미한다.   
즉, API는 운영체제와 응용프로그램 사이의 통신에 사용되는 언어나 메세지 형식을 의미함.   
API를 사용하는 경우 Annotation으로 @ResponseBody를 사용하면 viewResolver를 사용하지 않고 HTTP에 body 문자 내용을 직접 전달한다.  
@ResponsBody를 사용하면 다음과 같이 작동을 한다.
* HTTP의 BODY에 문자 내용을 직접 반환
* viewResolver 대신 HttpMessageConverter가 동작
* 기본 문자처리의 경우 StringHttpMessageConverter가 동작
* 기본 객체처리의 경우 MappingJackson2HttpMessageConverter가 동작.
* byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음.  

___
참고글   
https://kotlinworld.com/326#recentComments  
https://uhhyunjoo.tistory.com/50   
김영한 선생님의 강의
