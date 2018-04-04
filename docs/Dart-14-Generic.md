# 제네릭

초반에 익혔던 JavaScript의 배열에 해당하는 [List의 API 문서](https://api.dartlang.org/stable/dart-core/List-class.html)를 보면 `List<E>`라고 쓰여있습니다. Dart에는 JavaScript에 없는 제네릭이라는 개념을 가지고 있습니다. `<...>` 표현식은 리스트가 타입을 가지고 있다는 표시입니다.


## 제네릭 기초

문자열만 담아야할 리스트가 필요하면, `List<String>` 으로 리스트를 만들어야합니다. Dart는 IDE와 Dart VM이 타입 확인을 하므로 실수를 줄일 수 있습니다. 그리고 제네릭을 사용하면 코드 중복을 방지할 수 있수 있습니다. 하나의 인터페이스를 이용해 여러 타입으로 구현할 수 있음에도 위의 타입 확인을 통한 실수 방지가 가능합니다.

객체를 캐시하는 추상 클래스가 필요하다고 가정할 때 제네릭이 없으면 이렇게 해야합니다.

```dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
```

만약 문자열 캐시가 추가로 필요하면 어떻게 될까요?

```dart
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
```

StringCache라는 이름만 다른 내용은 거의 유사한 추상클래스가 하나 더 생겼습니다.

제네릭을 이용해 하나의 `Cache` 추상 클래스로 해결할 수 있습니다.

```dart
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

## 컬렉션 리터럴

리스트와 맵 리터럴은 파라미터를 이용해 만들 수 있습니다.  파라미터로 만드는 리터럴은 생성자를 이용하지 않고 리스트의 경우 `<type>`, 맵의 경우 `<keyType, valueType>`를 `[]`, `{}` 앞에 표기해줍니다.

```dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```

## 생성자에서 파라미터화 된 타입 사용하기

리터럴이 아닌 생성자를 이용해 만든 리스트, 맵의 경우에는 아래와 같이 합니다. 리터럴과 다른점은 `new`를 이용해 인스턴스화 하는 것 입니다.

```dart
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
var nameSet = new Set<String>.from(names);
```

맵도 리스트와 같습니다.

```dart
var views = new Map<int, View>();
```

## 제네릭 컬렉션과 타입

Dart의 제네릭은 런타임에 타입 정보를 전달합니다. 프로덕션 모드에서도 컬렉션 타입을 테스트할 수 있습니다.

```dart
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```

## 타입 제한하기

제네릭을 이용하는 경우 타입을 제한할 필요가 있습니다. `extends`를 이용합니다.

```dart
// T must be SomeBaseClass or one of its descendants.
class Foo<T extends SomeBaseClass> {
  // ···
}

class Extender extends SomeBaseClass {
  // ···
}

void main() {
  // It's OK to use SomeBaseClass or any of its subclasses inside <>.
  var someBaseClassFoo = new Foo<SomeBaseClass>();
  var extenderFoo = new Foo<Extender>();

  // It's also OK to use no <> at all.
  var foo = new Foo();

  // Specifying any non-SomeBaseClass type results in a warning and, in
  // checked mode, a runtime error.
  // var objectFoo = new Foo<Object>();
```

제네릭 T는 이제 항상 `SomeBaseClass` 또는 `SomeBaseClass`의 자손 클래스여야 합니다.

## 제네릭 메소드 사용

메소드에서도 제네릭을 사용할 수 있습니다. 클래스에서 사용하듯 타입이 필요한 곳에 `T` 등을 사용해 제네릭으로 만듭니다.

```dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```

제네릭의 다양한 활용은 [제네릭 사용하기](https://github.com/dart-lang/sdk/blob/master/pkg/dev_compiler/doc/GENERIC_METHODS.md)를 읽어보세요