# Dart 변수
## 기본 변수

자바스크립트의 `var` 키워드와 동일한 `var` 키워드가 Dart에도 있습니다.
그리고 선언만 한 다음 값을 넣지 않으면 `null`입니다.

## 옵셔널

Dart 2에서 `var` 키워드를 이용해 선언한 변수는 대입된 값에 따라 자동으로 변수의 타입을 유추합니다.

`var` 이외에 `dynamic` 키워드가 있습니다. `dynamic` 키워드로 선언된 변수는 여러가지 타입의 값응ㄹ 대입할 수 있습니다.


## final 그리고 const

final과 const 모두 한번 값이 지정되면 바꿀 수 없습니다.
`var`와 같이 타입을 지정하지 않고 사용할 수 있습니다.  `const`는 암시적으로 `final`입니다. 

## 내장 타입

Dart의 기본 타입은 7가지입니다. 자바스크립트에는 없는 룬(`rune`)이 있습니다

- 숫자
- 문자열
- 부울린
- 리스트 (Array와 같습니다)
- 맵
- 룬 (유니코드 캐릭터를 표현하는데 사용합니다)
- 심볼

## 숫자 ([int](https://api.dartlang.org/stable/dart-core/int-class.html), [double](https://api.dartlang.org/stable/dart-core/double-class.html))

숫자는 정수형 `int`와 실수형 `double` 두가지입니다.
문자열을 정수형 숫자로 바꾸려면 `int.parse`를 이용합니다.
문자열을 실수형 숫자로 바꾸려면 `double.parse`를 이용합니다.
정수형 숫자를 문자열로 바꾸려면 `정수형.toString()`을 이용합니다.
실수형 숫자를 문자열로 바꾸려면 `실수형.toStringAsFixed(소숫점 갯수)`을 이용합니다.

## 문자열

문자열은 작음 따옴표(Single Quote)와 큰 따옴표(Double Quote)두가지 모두 사용할 수 있습니다. 자바스크립트와 같습니다.

문자열 연결(Concatenate)은 자바스크립트와 같이 `+`를 사용합니다.
Dart 줄바꿈에 두가지 방법을 더 제공합니다.

```dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
    'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

```dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```


## 부울린

자바스크립트와 거의 같습니다.

## 리스트

자바스크립트와 같습니다.

다른점은 컴파일타임에 리터럴을 이용할 때 상수형으로 만들 수 있습니다.

```dart
var constantList = const [1, 2, 3];
```

## 맵

Dart의 맵은 자바스크립트의 객체처럼 키 - 값으로 구성합니다.
자바스크립트의 `Map`과는 다릅니다.
타입을 지정하는 모드에서는 `Map<타입, 타입>`을 이용하고, 사용할때는 `맵이름[키]`로  사용하므로 자바스크립트의 객체를 사용할 때 처럼 `맵이름.키`를 사용하면 안됩니다.

## 룬

룬은 UTF-32 코드를 사용할 수 있도록 도와줍니다.

😆는 `\u{1f600}`입니다.

## 심볼

심볼은 자바스크립트의 Symbol 처럼 식별자로 사용합니다.
문법은 자바스크립트와 다르게 `#심볼이름`과 같이 사용합니다.