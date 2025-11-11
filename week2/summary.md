## Q1. 처리율 제한 장치 구현 방식을 알 수 있는데, 이를 어떻게 Spring Boot에서 적용할 수 있을까?
- 구글 `Guava`의 `RateLimiter` : 토큰 버킷 기반 알고리즘
```java
@Component
public class ApiRateLimiter {
    private final RateLimiter rateLimiter = RateLimiter.create(5.0); // 초당 5개 요청

    public boolean allowRequest() {
        return rateLimiter.tryAcquire();
    }
}
```

## Q2. 루아 스크립트와 정렬 집합은 어떻게 race condition의 문제를 해결할까? 왜 이것들이 락보다 더 효율적일까?
- lua script : counter를 증가시키는 연산을 원자적으로 처리하게 해줌
- redis의 hash 자료구조는 순서대로 저장하므로 정렬을 두고 정렬 집합을 사용
