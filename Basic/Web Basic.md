# 스프링 웹 개발 기초
* 정적 컨텐츠
* MVC와 템플릿 엔진
* API
___
## 정적 컨텐츠
![IMG_1A7704876C0C-1](https://user-images.githubusercontent.com/110332047/183669303-f48dd970-988c-47ee-81ee-f65a2c0f2f5a.jpeg)
정적 컨텐츠란 html을 그대로 서버에 전달하는 것을 말함.  
정적 컨첸츠의 경우 우선적으로 스프링 컨테이너에 hello-static 관련 컨트롤러가 있는지를 찾음.  
그 이후 컨트롤러가 없다면 resources안에 있는 static/hello-static.html을 찾아서 반환해주는 구조.

___
## MVC와 템플릿 엔진
![IMG_970AC2577C0E-1](https://user-images.githubusercontent.com/110332047/183671952-b3584d93-8fb9-4981-81f0-0b0663ee7e45.jpeg)
Spring MVC는 Model, View Controller 세가지 구성요소를 사용해 **사용자의 다양한 HTTP Request를 처리하고 단순한 텍스트 형식의 응답, REST 형식의 응답, View를 표시하는 html을 return
하는 응답까지 다양한 응답을 할 수 있도록 하는 프레임웍**

___
## API
![IMG_6001E6F24A39-1](https://user-images.githubusercontent.com/110332047/183675059-4a4707cd-9ef5-4673-a720-46754f380a5b.jpeg)
API는 Application Programming Interface의 약자.   
> 여기서 Application Programming : 응용 프로그래밍
> Interface : 서로 다른 두개의 시스템이 정보를 주고 받도록 이어주는 경계를 의미한다.
즉, API는 운영체제와 응용프로그램 사이의 통신에 사용되는 언어나 메세지 형식을 의미함.

### @ResponseBody   
이 문구는 데이터 자체를 전달하기 위한 용도임을 알려주는 annotation이다.   
@ResponseBody 를 사용하면 HTTP의 BODY에 문자 내용을 직접 반환한다.
이 때 HttpMessageConverter가 동작하는데 받은내용이 문자인 경우 StringHttpMessageConverter, 객체인 경우 MappingJackson2HttpMessageConverter로 불린다.






___
참고글   
https://kotlinworld.com/326#recentComments  
https://uhhyunjoo.tistory.com/50
