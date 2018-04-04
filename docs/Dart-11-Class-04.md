# 클래스 - 4

클래스 변수/메소드는 클래스 전체에서 사용할 수 있는 변수/메소드를 말합니다. `static` 키워드를 이용해서 접근합니다.

## 정적 변수

```dart
class Queue {
  static const int initialCapacity = 16;
  // ···
}

void main() {
  assert(Queue.initialCapacity == 16);
}
```

정적 클래스 변수는 클래스 레벨에서 접근할 수 있는 변수입니다. `className.variableName`으로 사용합니다.

## 정적 메소드

정적 메소드는 인스턴스에서 사용하는 메소드가 아닌 클래스가 가지는 메소드입니다. `className.methodName`으로 사용합니다.

```dart
import 'dart:math';

class Point {
  num x, y;
  Point(this.x, this.y);

  static num distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = new Point(2, 2);
  var b = new Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
```

정적 메소드는 컴파일타임에 상수입니다. 정적 메소드를 파라미터로 상수 생성자에 전달할 수 있습니다.

