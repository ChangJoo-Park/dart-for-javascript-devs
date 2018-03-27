# 연산자

자바스크립트와 마찬가지로 대부분의 연산자는 Dart에 모두 있습니다.
자바스크립트에 없는 연산자들만 확인합니다.

## 단항연산자 ?.

객체에 접근하는 `.` 연산자와 유사하지만 `?.`은 해당 멤버 변수가 null일 수 있음을 표시하는 연산자입니다. 

## 타입테스트 연산자 as, is, is!

타입 테스트용 연산자인 as, is, is!는 아래와 같이 사용합니다.

```dart
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}
```
자바스크립트의 `typeof` 와 유사합니다. is!은 `is not` 의 의미입니다.

as는 타입캐스팅에 사용합니다

```dart
(emp as Person).firstName = 'Bob';
```

**is** 의 경우 emp가 null이거나 Person이 아니면 아무것도 하지않습니다.

**as**는 exception을 발생합니다.

## if null 체크용 ?? 와 ??=

```dart
exp ?? otherExp
```

위 문법이 있을 경우  아래와 같습니다.

```dart
((x) => x == null ? otherExp : x)(exp)
```

```dart
x = y ?? z;
```
위 문법은 y가 null이면 z를 x에 대입하고, null이 아니면 y를 x에 대입합니다.

```dart
x ??= y;
```

위 문법은 x가 null이면 y를 대입합니다.

## cascade 연산자 ..

Cascade 연산자는 메소드체이닝처럼 자신의 스스로를 계속 불러내 실행하는 연산자입니다.

일반적인 객체의 멤버변수를  처리하는 방법입니다. 자바스크립트 문법과 약간 다르지만 넘어가도록합니다.

```dart
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

위 내용은 cascade 연산자를 이용해 아래처럼 바뀝니다.

```dart
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

엄밀히 말해, `..`은 연산자라고 부르기보다는 Dart에서 지원하는 문법의 일부로 보는 것이 맞습니다.
