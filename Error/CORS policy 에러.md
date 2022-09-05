# CORS policy 에러.

## 문제 발생 상황 
FrontEnd : EC2 서버 주소 중 8080 port로 Request 를 진행한 후 3000 port로 Response를 받으려고 함.   
BackEnd : 같은 port 에 대해서는 로그인 해야지만 기능을 사용할 수 있도록 권한을 설정해 두었지만 CORS 정책 관련해서는 풀어 둔 것이 없는 상황.

### 문제 발생 
![image](https://user-images.githubusercontent.com/110332047/188483592-9b73ec78-1678-4933-a8c0-545609ffe4a9.png)
FrontEnd 쪽에서 다음과 같이 에러가 난다고 얘기를 전해 받음.   
어떠한 문제인지 직접 구글링을 해보니 CORS 관련한 문제 였다.   
CORS는 Cross-Origin Resource Sharing 인데 이 중 Origin 은 웹 컨텐츠에서의 출처를 의미한다. 여기서 출처란 **스킴 + 호스트 + 포트** 로써 
이 세가지가 모두 일치하는 것을 의미한다. 

![image](https://user-images.githubusercontent.com/110332047/188484551-991a6a8f-3c25-4596-adae-750958fc7498.png)    
이와 같이 React 와 Spring은 서로 다른 포트를 사용한다. 아까 전에 알아본 출처 중 포트가 일치 하지 않으므로 다른 출처를 가진다.   
이러한 경우 접근 권한을 줄 수 있도록 브라우저에 알려주는 체제인 CORS를 이용 해야 한다. 

#### 제한된 교차 출처 HTTP 요청 
접근 권한을 서로 열어두면 편할것 같지만 이렇게 교차 출처 HTTP 요청을 제한 하는 것은 **보안**을 위해서다. 개발자 도구만 확인하더라도 어떤 서버와 통신하고 어떤 정보를 주고 받는 지 
제제 없이 열람이 가능하다. 만약 다른 출처를 가진 애플리케이션 접근 제한이 없다면 XSS나 CSRF등을 통해 중요한 데이터를 빼가는게 쉬워진다.   
> Postman으로 확인 할 땐 잘 되던데요?
> => CORS를 확인하는 로직이 서버가 아닌 브라우저에 구현이 되어 있다. 이로 인해 Postman 과 같은 툴을 이용할 경우에는 에러가 나지 않는다.    

### 에러 해결 방법
기본적으로 웹 클라이언트 애플리케이션은 다른 출처의 리소스를 요청할 떄 HTTP 프로토콜을 사용한다. 이때 브라우저는 요청 헤더에 Origin 이라는 필드를 출처에 함께 담아 보낸다. 이후 서버가 
이 요청에 대한 응답을 할 때 Access-Control-Allow-Origin 이라는 값에 이 리소스에 접근하는 것이 허용된 출처를 내려준다. 응답을 받은 브라우저는 브라우저가 보냈던 Origin 과 서버에서 
받아온 Access-Control-Allow-Origin 두값을 비교해 이 응답이 유효한지 아닌지를 결정한다. 

해당 문제는 다음 코드로 해결이 가능함.
```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    public static final String ALLOWED_METHOD_NAMES = "GET,HEAD,POST,PUT,DELETE,TRACE,OPTIONS,PATCH";

    @Override
    public void addCorsMappings(final CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedMethods(ALLOWED_METHOD_NAMES.split(","));
    }
}
```


* addMaping : 해당 설정을 적용할 API 범위 선택 (/**-> 전체 적용)
* allowedOrigins : Origin을 허용할 범위 선택 (생략 시 * 와 같은 의미로 전체 허용됨)
* allowedMethods : 허용할 HTTP메서드 선택

