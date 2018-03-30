# Mixins

믹스인은 클래스에 여러개의 다른 클래스를 상속하는 방법입니다.
일반적인 부모 - 자식 상속에서 사용하는 `extends` 키워드가 아닌 `with` 키워드를 사용합니다. 믹스인을 사용하는 예제입니다.

```dart
class Musician extends Performer with Musical {
  // ···
}

class Maestro extends Person
    with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```

`Musician` 클래스는  `Performer`를 상속받고, `Musical` 믹스인을 가집니다. `Maestro`는 여러개의 믹스인을 가지고 있는 것을 볼 수 있습니다.

아래는 `Musical` 믹스인을 정의한 예제입니다.

```dart
abstract class Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```

`mixin`을 구현하려면 생성자를 정의하지 않고, `super` 클래스를 호출하지 않아야 합니다. 

Dart의 2버전에는 아직 `super mixins`을 지원하지 않습니다. 

믹스인의 자세한 내용은 [Mixins in Dart](https://www.dartlang.org/articles/language/mixins)에 있습니다.

