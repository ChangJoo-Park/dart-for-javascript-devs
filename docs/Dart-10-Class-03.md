# 클래스 - 3

클래스 챕터 2에서 `abstract`를 사용하여 추상 메소드를 가진 클래스를 살펴봤습니다. 이번에는 추상클래스와 인터페이스, 클래스를 확장하는 방법 등을 알아봅니다

## 추상 클래스

추상클래스는 인스턴스화 할수 없는 클래스입니다. 인터페이스를 정의할 때 유용하게 사용할 수 있습니다. 추상 클래스를 이용해 인스턴스를 만드려면 [Factory 생성자](https://www.dartlang.org/guides/language/language-tour#factory-constructors)를 사용합니다.

주로 추상 메소드를 만드는데 사용합니다. 아래에 추상 클래스와 추상 메소드를 만드는 예제가 있습니다.

```dart
// This class is declared abstract and thus
// can't be instantiated.
abstract class AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren(); // Abstract method.
}
```

추상 클래스를 상속받은 클래스는 인스턴스화할 수 있습니다. 그리고 추상 메소드는 상속받은 클래스 안에서 구현해야합니다.

```dart
class SpecializedContainer extends AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren() {
    // Provide an implementation, so the method is not abstract here...
  }

  // Abstract method causes a warning but
  // doesn't prevent instantiation.
  void doSomething();
}
```

Dart 2에서는 추상클래스만 추상 메소드를 가질 수 있습니다. 다른 경우에는 모두 에러입니다.

## 인터페이스 명시

모든 클래스는 클래스의 모든 인스턴스 멤버와 구현할 인터페이스의 모든 인스턴스를 포함하는 인터페이스를 암묵적으로 정의합니다. B에서 구현된 내용을 상속하지 않고 클래스 B의 API를 지원하는 클래스 A를 만드려면 클래스 A가 B 인터페이스를 구현해야합니다.

아래 두 예제는 한개의 인터페이스를 구현하는 경우와 여러개의 인터페이스를 구현하는 예제를 보여줍니다.

```dart
// A person. The implicit interface contains greet().
class Person {
  // In the interface, but visible only in this library.
  final _name;

  // Not in the interface, since this is a constructor.
  Person(this._name);

  // In the interface.
  String greet(String who) => 'Hello, $who. I am $_name.';
}

// An implementation of the Person interface.
class Impostor implements Person {
  get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(new Person('Kathy')));
  print(greetBob(new Impostor()));
}

class Point implements Comparable, Location {
  // ···
}
```

## 클래스 확장

`extends` 키워드로 하위 클래스를 만들고 상위 클래스의 내용을 `super` 키워드를 이용하여 참조합니다.

```dart
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ···
}

class SmartTelevision extends Television {
  void turnOn() {
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ···
}
```

## @override

서브클래스는 인스턴스 메소드, getter, setter를 오버라이드 할 수 있습니다. `@override` 어노테이션을 사용해 명시적으로 해당 클래스 멤버를 오버라이드하고 있음을 표시해주어야 합니다.

## noSuchMethod

`noSuchMethod`는 존재하지 않는 메소드나 인스턴스 변수에 접근할 때마다 호출할 수 있는 메소드입니다. `@override`를 이용해 `noSuchMethod`를 재정의할 수 있습니다.

```dart
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void noSuchMethod(Invocation invocation) {
    print('You tried to use a non-existent member: ' +
        '${invocation.memberName}');
  }
}
```

Dart 2에서는 다음 중 하나가 참이어야 `noSuchMethod`가 호출됩니다.

- 리시버가 정적 타입인 `dynamic`을 가집니다
- 리시버는 구현되어 있지 않은 메소드를 정의하는 static 타입을가집니다 (abstract는 괜찮습니다). 리시버의 다이나믹 타입은 `Object` 클래스의 것과는 다른 `noSuchMethod()` 구현을가집니다.

Dart Tour에는 `@proxy`가 있으나 Dart 2에서 제거됩니다