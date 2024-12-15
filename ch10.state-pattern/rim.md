# CHAPTER 10. 상태 패턴
> 내부 상태를 바꿈으로써 객체가 행동을 바꿀 수 있도록 한다.
- 여러 가지 상태와 상태를 전환하는 행동이 존재할 때, 상태를 별도의 클래스로 캡슐화하여 현재 상태를 나타내는 객체에헤 행동을 위임한다.
- 클라이언트는 알지 못하게 내부 상태를 적절히 바꾼다.

**뽑기 기계 코드 만들기 (1)**
```java
public class GumbalMachine {
  final static int SOLD_OUT = 0;
  final static int NO_QUARTER = 1;
  final static int HAS_QUARTER = 2;
  final static int SOLD = 3;

  int state = SOLD_OUT;
  int count = 0;

  public void insertQuarter() {
    if (state == HAS_QUARTER) {}
    else if (state == NO_QUARTER) {}
    else if (state == SOLD_OUT) {}
    else if (state == SOLD) {}
  }
}
```
- 가능한 모든 상태를 상수로 정의
- 모든 액션 메서드에서 현재 상태로 분기 처리

**상태 변경**
- 특정 상태에서 어떠한 액션 수행이 달라지거나 새로운 상태가 추가된다면?
  - ex. 10분의 1 확률로 손잡이를 돌릴 때 알맹이 2개가 나오도록
  - 액션 함수별로 복잡하게 분기 처리가 되어있어 코드 이해하기 어려움 (상태별로 어떤 처리가 필요한지 파악하기 어려움)
  - 특정 상태에 대해서만 수정하면 되는데, 모든 상태 처리 코드가 하나의 메서드에 구현되어 있음 (영향받는 코드가 많아짐)
- 바뀌는 부분인 상태, 상태별 액션을 캡슐화

**뽑기 기계 코드 만들기 (2)**
```java
interface State {
  insertQuarter();
  ejectQuarter();
  turnCrack();
  dispense();
}

class NoQuarterState implements State {
  GumballMachine gumballMachine;

  public NoQuarterState(GumballMachine gumballMachine) {
    this.gumballMachine = gumballMachine;
  }
}

  public void insertQuarter() {
    System.out.println("동전을 넣으셨습니다.");
    gumballMachine.setState(gumballMachine.getHasQuarterState());
  }
```
- `State`를 구현한 상태 클래스에서 액션 수행 정의
- 상태 클래스에서 `GumballMachine`의 변화된 상태 설정

**상태 vs 전략**
- 공통점
  - 공통 인터페이스를 구현한 객체 (전략 or 상태) 내에서 동일 액션을 서로 다르게 정의
- 차이점
  - 전략 : 클라이언트가 필요한 전략을 바꿔 넣음, 서로 다른 전략 객체 간에는 알지 못함
  - 상태 : 클라이언트는 내부 상태 변화를 알지 못함, 상태 간 종속성 있음
  
(1) 전략패턴 예시
```java
public class DuckSimulator {
  public static void main(String[] args) {
    Duck model = new ModelDuck();
    model.performFly();
    model.setFlyBehavior(new FlyRocketPowered());
    model.performFly();
  }
}
```
- 실행 중에 modelDuck의 특정 행동을 바꾸고 싶을 때, 원하는 행동에 전략 객체를 넣어줌

(2) 상태패턴 예시
```java
public class GameSimulator {
  public static void main(String[] args) {
    GumballMachine machine = new GumballMachine(5);
    machine.insertQuarter();
    machine.turnCrank();
  }
}
```
- 내부 상태 변화를 알지 못함
