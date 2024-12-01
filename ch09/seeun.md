## Iterator Pattern

> 반복 로직을 Iterator 인터페이스에 캡슐화하는 패턴

- Iterator 인터페이스를 호출할 때 어떤 객체를 반복하는 지 몰라도 된다. (캡슐화)
- Iterator 인터페이스를 구현할 수 있다면 어떤 컬렉션이든 반복할 수 있다. (다형성)
- 컬렉션을 관리하는 클래스(ex.일급 컬렉션)와 반복 작업을 관리하는 클래스(Iterator)를 분리한다. (SRP)
  - 각 클래스는 하나의 이유로만 변경될 수 있으므로 클래스 관리가 쉬워진다.
  - 응집도가 높아진다.
 
### Java Iterable Interface

```java
public interface Iterable<T> {

  Iterator<T> iterator();

  default void forEach(Consumer<? super T> action) {
      Objects.requireNonNull(action);
      for (T t : this) {
          action.accept(t);
      }
  }

  default Spliterator<T> spliterator() {
      return Spliterators.spliteratorUnknownSize(iterator(), 0);
  }
}
```

- Iterator 인터페이스와 `forEach()` 메서드를 통해 향상된 for 순환문을 사용할 수 있다.
  - `hasNext()` 등 Iterator 인터페이스의 메서드를 직접 호출하지 않고 반복할 수 있다.

<br/>

## Composite Pattern

> 객체들을 트리 구조로 구성하여 부분-전체 계층을 표현하는 구조적 디자인 패턴

```
1. Component (컴포넌트)
   - 모든 구체적인 클래스에 대한 공통 인터페이스 정의
   - 기본 동작 구현 및 공통 메서드 선언

2. Leaf (잎)
   - Component의 기본 요소
   - 자식 요소를 가지지 않는 개별 객체

3. Composite (복합체)
   - Component를 상속받아 자식 요소들을 관리
   - 자식 요소 추가, 제거, 순회 기능 구현
```

- 복합 객체(Composite)와 개별 객체(Leaf)를 대상으로 똑같은 작업을 적용할 수 있다.

### 투명성 (Transparency)

> 클라이언트가 Composite(복합 객체)와 Leaf(개별 객체)를 동일한 방식으로 취급할 수 있는 설계 접근 방식으로, 클라이언트 입장에서 객체의 복합 여부를 신경 쓰지 않고 동일한 인터페이스로 작업할 수 있다.

Component 인터페이스에 자식들을 관리하는 기능과 잎으로써의 기능을 모두 넣기 때문에, 단일 역할 원칙(SRP)를 깨는 대신 투명성을 확보한다.
