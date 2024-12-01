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

