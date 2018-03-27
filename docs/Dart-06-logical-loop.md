## Dart 조건문과 반복문

자바스크립트에 있는 대부분의 조건문과 반복문은 Dart에도 동일하게 있습니다.

Dart에만 있는 문법만 알아봅니다

## Iterable

List와 Set과 같은 [Iterable](https://api.dartlang.org/stable/dart-core/Iterable-class.html)은 데이터베이스 쿼리를 요청하는 듯한 유사한 문법의 조회를 할 수 있습니다.

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

`candidates` 가 리스트인 경우에 `yearsExperience` 변수가 5 이상인 사람에 한하여 `interview` 함수를 실행시킬 수 있습니다.

`where`의 조건에 맞는 첫번째를 찾는 `firstWhere`와 마지막을 찾는 `lastWhere`도 있습니다. 

더 많은 메소드는 [Iterable](https://api.dartlang.org/stable/dart-core/Iterable-class.html) 문서를 읽어보세요.

## Assert

Assert는 개발환경에서만 작동하는 기능입니다. assert 함수 내부의 구문이 참이 아닌 경우에 프로그램을 멈추도록 만들어줍니다.

```dart
// null이면 멈춥니다.
assert(text != null);

// number는 항상 100보다 작아야합니다.
assert(number < 100);

// URL은 https로 시작해야합니다.
assert(urlString.startsWith('https'));
```