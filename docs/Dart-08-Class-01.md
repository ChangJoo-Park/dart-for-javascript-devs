# 클래스

아시다시피 Dart는 객체지향언어입니다. 클래스와 믹스인을 이용한 상속을 지원합니다. 모든 객체는 당연히 클래스의 인스턴스이며 모든 클래스는 Object를 부모로 가집니다. 믹스인 기반 상속은 한개의 수퍼 클래스를 가지며 클래스는 여러개의 다른 클래스를 상속하여 상속받은 클래스의 내용을 사용할 수 있습니다.


## 클래스 기본

객체를 만드려면, 자바스크립트와 같이 `new` 키워드를 사용합니다. 클래스를 이용해 객체를 만드는 방법은 `new` 키워드와 `ClassName`을 사용하거나 `ClassName.identifier`를 사용하는 방법 두가지입니다.

Dart는 JSON을 이용해 객체를 만들 수 있습니다. 여기서는 `fromJson`을 사용합니다.

```dart
var jsonData = JSON.decode('{"x":1, "y":2}');

// Create a Point using Point().
var p1 = new Point(2, 2);

// Create a Point using Point.fromJson().
var p2 = new Point.fromJson(jsonData);
```

객체는 인스턴스 변수를 가지고 있는데, Dart는 `?.` 오퍼레이터를 이용해 null이 아닌경우에만 값을 바꾸는 문법을 지원합니다. `?.`를 사용하면 null때문에 발생하는 Exception을 방지할 수 있습니다.

```dart
// If p is non-null, set its y value to 4.
p?.y = 4;
```

## 생성자

Dart의 객체 생성에는 `new`가 외에 `const` 키워드를 제공합니다.  const에서 알 수 있듯 컴파일 타임에 상수인 객체를 만듭니다. 같은 값을 가지고 있다면 같은 인스턴스가 됩니다.

```dart
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b)); // 같은 인스턴스 입니다.
```
## 
인스턴스 변수

Dart의 인스턴스 변수는 JavaScript와 마찬가지로 초기에 값을 정해주지 않으면 null 입니다.

##  생성자

Dart의 생성자는 JavaScript의 클래스와 거의 같습니다. JavaScript가 `constructor`를 사용한다면, Dart는 클래스 이름을 사용합니다.

이보다 중요한 것은 생성자 코드 길이를 극적으로 줄일 수 있다는 점입니다.

```dart
// 일반적인 클래스 생성자
class Point {
  num x, y;

  Point(num x, num y) {
    this.x = x;
    this.y = y;
  }
}

class Point {
  num x, y;
  
  // 클래스 생성자의 신택스 슈가입니다
  Point(this.x, this.y);
}
```

## 기본 생성자 

생성자를 선언하지 않으면 기본 생성자를 자동으로 호출합니다.

## 이름이 있는 생성자

처음에 객체를 만들 때 두가지 방법(`ClassName`, `ClassName.identifier`)을 사용할 수 있습니다. 이름이 있는 생성자란 `ClassName.identifier`를 이용하는 방법입니다.

```dart
class Point {
  num x, y;

  Point(this.x, this.y);

  // 이름이 있는 생성자입니다.
  Point.origin() {
    x = 0;
    y = 0;
  }
}
```

##   기본생성자가 아닌 상위 생성자 호출

아래 예제는 기본 생성자가 없는 `Person` 클래스와 `Employee` 클래스 입니다. Person에는 `identifier`를 이용한 생성자가 있습니다. `Employee`에서 `.fromJson` 생성자의 부모 생성자를 호출하려면 `super.identifier`를 이용합니다.

```dart
class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

main() {
  var emp = new Employee.fromJson({});

  // Prints:
  // in Person
  // in Employee
  if (emp is Person) {
    // Type check
    emp.firstName = 'Bob';
  }
  (emp as Person).firstName = 'Bob';
}
```

## 불변 생성자

클래스가 만든 객체가 절대 변경될 일이 없다면 컴파일 타임에 상수로 만들 수 있습니다. 불변 생성자를 만드려면 `const` 생성자를 만들고 모든 인스턴스 변수를 `final`로 지정합니다.

## Factory 생성자

`factory` 키워드를 가진 생성자는 매번 새 인스턴스를 새로 만들지 않습니다. Factory 생성자는 캐시에서 인스턴스를 리턴하거나 서브타입의 인스턴스를 리턴합니다. Factory 생성자는 `this`에 접근할 수 없습니다.