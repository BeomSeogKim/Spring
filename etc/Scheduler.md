# Scheduler 
> 특정 시간 마다 혹은 특정 시간 간격으로 코드가 실행 될 수 있도록 설정하는 기법

Scheduler의 경우 어노테이션을 먼저 붙여줘야 한다. 

1. Spring application이 돌아가는 파일에 EnableScheduling 어노테이션을 붙여준다.
```java

@EnableScheduling
@SpringBootApplication
public class FinalProjectApplication {

	public static void main(String[] args) {
		SpringApplication.run(FinalProjectApplication.class, args);
	}
}

```

2. 실제 스케쥴링 작업을 수행할 클래스를 만든다.
```java
@Service
@RequiredArgsConstructor
public class SchedulerService {

    private final PostRepository postRepository;


    /**
     * 매일 오전 0시 기준으로 게시글들 상태 업데이트
     * 모집 마감일이 지난 경우 ==> DONE 상태로 바뀜
     * 모임 일이 지난 경우 ==> CLOSURE 상태로 바뀜
     */

    @Scheduled(cron = "0 0 0 * * *")
    @Transactional
    public void run() {
        LocalDate now = LocalDate.now();

        List<Post> postList = postRepository.findAll();
        for (Post post : postList) {
            if (now.isAfter(post.getEndDate())) {
                post.updateStatus();
            }
            if (now.isAfter(post.getDDay())) {
                post.closeStatus();
            }
        }
    }
}
```
이 두가지만 잘 설정해 준다면 특정 시간마다 잘 돌아간다. 다만 두가지 규칙을 지켜야 함
1. Method 는 void 타입으로 만들 것
2. Method 는 매개변수 사용 불가

@Scheduled에 여러가지 메서드를 사용할 수 있지만 그 중 cron에 대해서 알아본다면 

```java
// 매일 오후 18시에 실행
@Scheduled(cron = "0 0 18 * * *")
public void run() {
System.out.println("Hello CoCo World!");} 
// 매달 10일,20일 14시에 실행
@Scheduled(cron = "0 0 14 10,20 * ?") 
public void run() {
System.out.println("Hello CoCo World!");} 
// 매달 마지막날 22시에 실행
@Scheduled(cron = "0 0 22 L * ?") 
public void run() {
System.out.println("Hello CoCo World!");} 
// 1시간 마다 실행 ex) 01:00, 02:00, 03:00 ...
@Scheduled(cron = "0 0 0/1 * * *") 
public void run() {
System.out.println("Hello CoCo World!");} 
// 매일 9시00분-9시55분, 18시00분-18시55분 사이에 5분 간격으로 실행
@Scheduled(cron = "0 0/5 9,18 * * *") 
public void run() {  
System.out.println("Hello CoCo World!");} 
// 매일 9시00분-18시55분 사이에 5분 간격으로 실행
@Scheduled(cron = "0 0/5 9-18 * * *") 
public void run() {    S
ystem.out.println("Hello CoCo World!");}
// 매달 1일 10시30분에 실행
@Scheduled(cron = "0 30 10 1 * *") 
public void run() {    
System.out.println("Hello CoCo World!");} 
// 매년 3월내 월-금 10시30분에 실행
@Scheduled(cron = "0 30 10 ? 3 1-5") 
public void run() {    
System.out.println("Hello CoCo World!");} 
// 2022-2023년 매달 마지막 토요일 10시30분에 실행
@Scheduled(cron = "0 30 10 ? * 6L 2022-2023") 
public void run() {    
System.out.println("Hello CoCo World!");}
```

출처 : https://dev-coco.tistory.com/176
