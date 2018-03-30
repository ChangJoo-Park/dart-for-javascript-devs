# enum

enum은 자바스크립트에는 없는 표현식입니다. 대부분의 타입이 있는 프로그래밍언어처럼 Dart에도 enum(혹은 enumeration)을 지원합니다. 상수 변수를 가지고 있는 클래스라고 이해하면 됩니다.

enum을 사용예 입니다. 자주 사용하는 색 빨강, 초록, 파랑을 자주 사용하는 경우, enum으로 사용합니다. 왜냐하면 위 색은 고정된 값이며 사용자가 변경할 일이 없습니다.

```dart
enum Color { red, green, blue }
```

위 예제처럼 변수는 있지만 값을 따로 지정하진 않습니다. 각 값의 인덱스는 접근할 수 있습니다.

```dart
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
```

enum의 모든 값을 가져오려면 `enumName.values`를 사용합니다.

```dart
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```

`switch - case` 문법을 사용하는 경우, `switch` 안의 값이 enum이면 `case` 조건에서 사용할 수 있습니다.

```dart
var aColor = Color.blue;

switch (aColor) {
  case Color.red:
    print('Red as roses!');
    break;
  case Color.green:
    print('Green as grass!');
    break;
  default: // Without this, you see a WARNING.
    print(aColor); // 'Color.blue'
}
```

두가지 제한이 있습니다.

- enum을 subclass로 만들거나, 믹스인 또는 구현체를 만들 수 없습니다.
- enum을 명시적으로 인스턴스화 할 수 없습니다.

