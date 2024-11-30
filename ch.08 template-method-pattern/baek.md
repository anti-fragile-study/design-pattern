# Template Method Pattern

## 정의
- 알고리즘의 골격을 템플릿 메소드로 정의하고, 알고리즘의 각 단계 일부를 서브클래스에서 구현하도록 하는 패턴
- 알고리즘의 구조를 그대로 유지하며 서브클래스에서 각 단계를 재정의할 수 있음
- 여기서 틀이란, 일련의 단계들로 알고리즘을 나열한 메소드

## 예시
```java
abstract class AbstractClass {

  // final로 선언하여 서브클래스에서 재선언하는 것을 방지
  final void templateMethod() {
    operation1();
    operation2();
    concreteOperation();
    hook();
  }

  // 추상 메소드로 선언하여 서브클래스에서 반드시 재정의하도록 강제
  abstract void operation1();

  abstract void operation1();

  // 서브클래스에서 재선언할 수 없게 강제하고자 하면 final로 선언할 수 있음
  void concreteOperation() {
    // some operations..
  }

  // 구상 메소드이지만, 아무 일도 하지 않으면 hook이라고 부름.
  // 서브클래스에서의 재정의를 강제하지 않으나 원할 때 재정의하여 알고리즘 중간에 끼어들 수 있음
  void hook() {}
}
```

## Hook
- 구상 클래스이나 아무 동작이 없는 메소드
- 다양한 위치에서 알고리즘 사이사이에 끼어들 수 있는 옵션을 제공

## 헐리우드 원칙
> 먼저 연락하지 마세요, 저희가 연락 드리겠습니다.
- 저수준 구성요소가, 언제 시스템에 참여할지를 고수준 구성요소가 결정한다는 원칙
- 템플릿 메소드가 서브클래스의 구현이 언제 참여할지를 관리한다는 점에서 템플릿 메소드 패턴은 헐리우드 원칙을 준수함

## 스트래티지 패턴과의 비교
- 둘 다 일련의 알고리즘군을 정의하고, 유연하게 바꿔가면서 쓸 수 있도록 한다는 공통점이 있음
- 템플릿 메소드 패턴은 상속을 통해 강력한 프레임워크를 제공하며, 스트래티지 패턴은 상속 뿐만 아니라 구성을 통해서도 유연하게 알고리즘 구현을 선택할 수 있게 함

## 활용 예시
- Java Comparable
- Java Swing
- [XUnit](https://www.youtube.com/watch?v=tdKFZcZSJmg)의 setup, teardown 메소드들
