# 데코레이터 패턴
- 구성(Composition)을 사용하여 객체에 추가 요소를 동적으로 더할 수 있는 패턴
- 구현 방법: 슈퍼 클래스를 상속하는 구상 클래스와 구성 요소를 생성하고 런타임 시점에 구상 클래스에 구성 요소를 추가

## 예시 : 토핑 추가가 가능한 카페 음료

### 상속

1. Beverage 추상 클래스

```java
public abstract class Beverage {
    // 토핑
    boolean milk = false;
    boolean whip = false;
    
    double milkCost = 1.0;
    double whipCost = 2.0;
    
    double cost() {
        double condimentCost = 0.0;
        if (hasMilk()) {
            condimentCost += milkCost;
        }
        if (hasWhip()) {
            condimentCost += whipCost;
        }
        return condimentCost;
    }
    
    boolean hasMilk() {
        return milk;
    }
    
    boolean hasWhip() {
        return whip;
    }

    void setMilk() {
        milk = true;
    }

    void setWhip() {
        whip = true;
    }
}
```

2. Beverage 를 상속하는 음료

```java
class Espresso extends Beverage {

    public double cost() {
        return 5.0 + super.cost();
    }
}
```

3. 음료 주문

```java
Beverage beverage = new Expresso();
beverage.setMilk(); // 우유 토핑 추가
beverage.setWhip(); // 휘핑 크림 추가
System.out.println("가격 : " + beverage.cost());
```

- 토핑이 추가/삭제 될 때마다 Beverage 코드 변경
- 서브 클래스는 불필요한 기능까지 상속받게 됨

### 구성을 활용하여 데코레이터 패턴 적용

1. Beverage 추상 클래스

```java
abstract class Beverage {
    public abstract double cost();
}
```

2. Beverage 를 상속하는 음료
```java
public class Espresso extends Beverage {

    @Override
    public double cost() {
        return 5.0;
    }
}
```

3. Beverage 를 확장하는 Decorator

```java
public abstract class CondimentDecorator extends Beverage {
    Beverage beverage;
}
```

4. CondimentDecorator 를 상속하는 토핑
```java
public class Milk extends CondimentDecorator {
    
    public Mild(Beverate beverage) {
        this.beverage = beverage;
    }

    @Override
    public double cost() {
        return beverage.cost() + 1.0;
    }
}

public class Whip extends CondimentDecorator {

    public Whip(Beverate beverage) {
        this.beverage = beverage;
    }

    @Override
    public double cost() {
        return beverage.cost() + 2.0;
    }
}
```

5. 음료 주문

```java
Beverage beverage = new Espresso();
beverage = new Milk(beverage); // 우유 토핑 추가
beverage = new Whip(beverage); // 휘핑 크림 추가

System.out.println("가격 : " + beverage.cost());
```

- 토핑이 추가/삭제 될 때마다 기존의 코드를 변경할 필요 없이 Decorator 를 상속하여 새로운 클래스를 생성하기만 하면 됨
- 토핑 클래스가 독립적이기 때문에 필요한 토핑만 음료에 추가하면 됨
