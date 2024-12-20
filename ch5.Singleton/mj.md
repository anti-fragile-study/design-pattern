# 싱글톤 패턴
- 클래스 인스턴스를 하나만 만들고, 그 인스턴스로의 전역 접근을 제공
- 한 어플리케이션에 들어있는 어떤 객체도 같은 자원을 활용
- 연결 풀이나 스레드 풀과 같은 자원을 관리

## 고전적인 싱글톤 패턴 구현법
```java
public class Singleton {
    private static Singleton uniqueInstance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```
### 문제점 : 멀티 스레드 환경에서 인스턴스가 2개 이상 생성될 수 있음

### 해결방법1. synchoronized
```java
public static synchoronized Singleton getInstance() {...}
```
- 동기화로 인한 오버헤드 발생(인스턴스가 생성되면 굳이 해당 메소드가 동기화된 상태로 유지될 필요가 없음)

### 해결방법2. static 변수에 바로 생성
```java
private static Singleton uniqueInstance = new Singleton();
```
- 클래스가 로딩될 때 JVM에서 Singleton의 유일한 인스턴스를 생성해줌
- 사용하지 않아도 무조건 생성되어 메모리 공간 차지

### 해결방법3: DCL(Double-Checked Locking)
```java
public class Singleton {
    private volatile static Singleton uniqueInstance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (uniqueInstance == null) {
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```
- volatile : CPU 캐시가 아닌 메인 메모리에서 값을 조회
- 인스턴스가 생성되지 않았을 때만 동기화가 진행

## Enum을 사용한 싱글톤 구현
```java
public enum Singleton {
    UNIQUE_INSTANCE;
}
```
- 멀티 스레딩 동기화 문제, 리플렉션, 직렬화 역직렬화 문제 해결 
- 상속 불가능
