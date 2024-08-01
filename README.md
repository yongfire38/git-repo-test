### 날짜 :2023-12-29 11:29 금

### 주제 : #java #springboot

---

### 메모

> **uptime** 은 리눅스 **서버가 얼마나 오랫동안 실행되어 있는지를 확인**할 수 있는 명령어이다.
> 이 명령어의 구현을 Spring Boot에서 유사하게 구현한 코드 예시는 다음과 같다.

```
@RestController
@SpringBootApplication
public class SpringBootUptimeApplication implements ApplicationListener<ApplicationReadyEvent> {

    private long startTime;

    public static void main(String[] args) {
        SpringApplication.run(SpringBootUptimeApplication.class, args);
    }

    @Override
    public void onApplicationEvent(ApplicationReadyEvent event) {
        startTime = event.getTimestamp();
    }

    @GetMapping("/uptime")
    public Map<String, Object> uptime() {
        long uptime = System.currentTimeMillis() - startTime;
        String humanReadableUptime = DurationFormatUtils.formatDurationWords(uptime, true, true);
        return Map.of(
                "startTime", Instant.ofEpochMilli(startTime),
                "uptime", uptime,
                "humanReadableUptime", humanReadableUptime);
    }
}
```

결과를 다음과 같이 확인 가능하다. (실제로는 해당 경로에 대한 권한 설정도 필요하겠지만...)

```
{"humanReadableUptime":"0 days 0 hours 4 minutes 5 seconds","uptime":245074,"startTime":"2024-01-02T04:22:12.655Z"}
```

### 출처(참고문헌)

- https://okky.kr/articles/1483058
- https://jsonobject.tistory.com/412
- https://incheol-jung.gitbook.io/docs/study/srping-in-action-5th/chap-16.
- https://velog.io/@zenon8485/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%EC%95%A1%EC%B6%94%EC%97%90%EC%9D%B4%ED%84%B0
- https://techblog.woowahan.com/9232/

### 연결문서

- [[Spring actuator]]

### 긴급 추가 내용

- 해당 내용은 공유가 필요한 관계로 긴급하게 2번이 push를 진행함
- 작업자들은 해당 내용을 받아서 추가로 작업을 진행할 것

### 추가 내용

- 해당 내용은 테스트를 위해 1번이 추가해서 작업해 놓은 내용임
- 설명이 부족한 거 같아서 1번이 작업한 내용을 조금 더 추가
- 기타 첨삭도 진행 (여기까지 1번 작업)
