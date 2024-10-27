## 싱글턴 패턴
유일한 객체 인스턴스만을 생성하는 디자인 패턴이다.
- 객체가 2개 이상일 때 프로그램에 문제가 발생할 경우 사용 가능
- ex. 결과 이상/불필요한 자원 차지 - 캐시, 스레드 풀, 로깅

**전역 변수 vs 싱글턴 패턴**
|            | 전역 변수     | 싱글턴 패턴        |
|------------|-----------|---------------|
| **접근성**    | 전역        | 전역            |
| **생성**     | 애플리케이션 시작 | 사용할 때 (lazy)  |
- 전역 변수를 사용하면 네임스페이스가 오염될 수 있다

**싱글턴 객체 생성**
```java
public class ChocolateBoiler {
  private static ChocolateBoiler instance;

  private ChocolateBoiler() {}

  private static ChocolateBoiler getInstance() {
    if (instance == null) {
      instance = new ChocolateBoiler();
    }
    return instance;
  }
}
```
- 객체가 필요할 때만 생성한다

**멀티 스레딩 환경**
- 멀티 스레딩 환경에서 여러 스레드에 의해 동시 접근될 때 싱글턴 패턴이 지켜지지 않을 수 있다
  - 컨텍스트 스위칭

1. `synchronized` 메소드로 선언하기
```java
public static synchronized ChocolateBoiler getInstance() { }
```
- 락을 사용해 공유 자원에 최대 1개의 스레드만 접근하도록 제한한다
  - 코드 실행을 제어하고 값의 가시성을 확보
- 그러나 메소드 동기화는 성능을 100배 정도 저하시킴!
 - `synchronized`를 사용하는 다른 메서드들로 불필요하게 접근 제한됨  

2. 즉시 초기화하기
```java
public class ChocolateBuilder {
  private static ChocolateBuilder instance = new ChocolateBuilder();
}
```
- 클래스가 JVM으로 로딩될 때 단 한번만 초기화된다
- 인스턴스가 항상 필요할 경우 사용하기 적합하다

3. DCL (Double-Checked Locking) 적용하기
```java
public class ChocolateBoiler {
  private volatile static ChocolateBoiler instance;

  private ChocolateBoiler() {}

  private static ChocolateBoiler getInstance() {
    if (instance == null) {
      synchronized (Singleton.class) {
        if (instance == null) {
          instance = new ChocolateBoiler();
        }
      }
    }
    return instance;
  }
}
```
- 값을 처음 초기화할 때만 `synchronized` 블록을 사용한다
- `synchronized` 블록 밖에서 변수 가시성 확보를 위해 `volatile`로 선언한다

**enum**
- enum을 사용하면 걱정없이 간편하게 싱글턴 객체를 생성할 수 있다.
