# 클래스 2 - 메소드

OOP에서 메소드는 객체가 할 수 있는 행동을 의미합니다. 자바스크립트의 클래스와 같이 Dart도 클래스에 메소드가 있습니다.

## 인스턴스 메소드

인스턴스 메소드는 객체 밖에서 `인스턴스.메소드이름`으로 호출하거나 객체 안에서 `this.메소드이름`으로 호출할 수 있습니다.  다음 예제의 `distanceTo()` 메소드를 확인하세요

```dart
import 'dart:math';

class Point {
  num x, y;

  Point(this.x, this.y);

  num distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqrt(dx * dx + dy * dy);
  }
}
```

`Point` 클래스의 인스턴스가 `p` 라면, `p.distanceTo(new Point(0, 0)`을 호출할 수 있습니다.


## Getter / Setter

getter와 setter는 객체의 속성(혹은 변수)을 읽거나 변경시킬 수 있는 특별한 메소드입니다.  기본적으로 클래스 변수들은 암묵적인 getter와 setter를 가지고 있습니다.

명시적으로 getter를 지정하면 computed property와 같은 기능을 할 수 있습니다.

```dart
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}

void main() {
  var rect = new Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```

`main` 함수에서 getter / setter에 접근하고 값이 변경되는 것을 확인할 수 있습니다.

## 추상 메소드

인스턴스와 getter, setter 메소드는 추상화할 수 있습니다. 인터페이스를 정의하고 구현을 하지 않는 방식을 사용합니다. 자바스크립트에서도 추상메소드와 인터페이스를 유사하게 구현할 수 있으나 공식적으로 지원하는 것은 아닙니다. [비교해보세요](https://medium.com/@yuribett/javascript-abstract-method-with-es6-5dbea4b00027)

```dart
abstract class Doer {
  // Define instance variables and methods...

  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // Provide an implementation, so the method is not abstract here...
  }
}
```



## 오버라이드 가능한 연산자

Dart는 연산자 오버라이드를 지원합니다. 단 모든 연산자는 아닙니다. 오버라이드 가능한 연산자 목록은 다음과 같습니다.

```dart
<	+	|	[]
>	/	^	[]=
<=	~/	&	~
>=	*	<<	==
–	%	>>	 
```

`Vector` 클래스를 사용할 때 `+`와 `-` 연산자를 오버라이드 해서 자동으로 Vector 연산을 하도록 만들 수 있습니다.

```dart
class Vector {
  final int x, y;

  const Vector(this.x, this.y);

  /// Overrides + (a + b).
  Vector operator +(Vector v) {
    return new Vector(x + v.x, y + v.y);
  }

  /// Overrides - (a - b).
  Vector operator -(Vector v) {
    return new Vector(x - v.x, y - v.y);
  }
}

void main() {
  final v = new Vector(2, 3);
  final w = new Vector(2, 2);

  // v == (2, 3)
  assert(v.x == 2 && v.y == 3);

  // v + w == (4, 5)
  assert((v + w).x == 4 && (v + w).y == 5);

  // v - w == (0, 1)
  assert((v - w).x == 0 && (v - w).y == 1);
}
```

`==` 연산자도 오버라이드 할 수 있습니다. 이를 위해 Object 클래스의 `hashCode` getter를 오버라이드해야합니다.
