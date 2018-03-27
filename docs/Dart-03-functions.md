# 함수

Dart는 객체지향 언어이므로 함수 또한 객체이며, [Function](https://api.dartlang.org/stable/1.24.3/dart-core/Function-class.html) 클래스를 기반으로 작동합니다
이 말은 함수는 변수처럼 사용되거나, 다른 함수의 아규먼트로 전달할 수 있다는 것을 의미합니다. 그리고 클래스를 함수처럼 사용할 수도 있습니다.

## 기본 구조

함수는 자바스크립트처럼 사용할 수 있습니다.

```dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

그러나 리턴 타입, 파라미터 타입을 명시해서 사용하는 것을 추천합니다.

```dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

자바스크립트의 arrow-function과 동일한 방식으로도 사용할 수 있습니다.

```dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

## 옵셔널 파라미터

파라미터를 처리할 때 이름과 위치를 지정할 수 있습니다. 둘 다 하지 않을 수도 있습니다.

### 옵셔널 네임드 파라미터

옵셔널 네임드 파라미터는 함수를 호출할 때 이름을 지정하는 방식입니다. _파라미터 이름: 값_ 형태로 사용합니다.

옵셔널 네임드 파라미터는 자바스크립트의 **Destructuring** 과 유사합니다.

```dart
// 호출할 떄
enableFlags(bold: true, hidden: false);
```

```dart
// 함수 원형
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold, bool hidden}) {
  // ...
}
```

### 옵셔널 포지셔널 파라미터

옵셔널 포지셔널 파라미터는 값을 전달하지 않아도 처리할 수 있도록 도와줍니다.

```dart
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}

// 두가지 device를 생략해도 호출할 수 있습니다.
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```


## 파라미터 기본값

파라미터 기본값은 옵셔널 네임드 파라미터와 같이 자바스크립트의 **Destructuring** 과 유사합니다. 전달받은 값이 없으면 자동으로 기본 값을 채워줍니다.

```dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {
  // ...
}

// hidden은 자동으로 false가 됩니다.
enableFlags(bold: true);
```

옵셔널 포지셔널 파라미터에서도 파라미터 기본값을 지정할 수 있습니다.

```dart
String say(String from, String msg,
    [String device = 'carrier pigeon', String mood]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  if (mood != null) {
    result = '$result (in a $mood mood)';
  }
  return result;
}

assert(say('Bob', 'Howdy') ==
    'Bob says Howdy with a carrier pigeon');
```

리스트 / 맵을 파라미터로 사용하는 경우에도 기본값 지정이 가능합니다.

```dart
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```

## main 함수

main 함수는 앱의 가장 최상위에 있는 함수입니다. 모든 앱의 시작점이 됩니다. main함수는 void를 리턴하며, `List<String>`을 파라미터로 사용할 수 있습니다.

## 1급객체인 함수

Dart에서 함수는 일급 클래스 객체입니다. 이 말은 함수를 다른 함수의 파라미터로 전달할 수 있다는 것을 의미합니다. 

```dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// printElement 함수를 파라미터로 전달합니다.
list.forEach(printElement);

var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

## 익명함수

자바스크립트처럼 Dart도 익명함수를 가지고 있습니다. 
익명함수의 형태입니다.

```dart
([[Type] param1[, …]]) { 
  codeBlock; 
}; 
```

**주의** Dart 2는 타입을 생략할 수 없습니다.

```dart
var list = ['apples', 'bananas', 'oranges'];
// 타입을 지정하려면 `String item`
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```

## 리턴

모든 함수는 값을 반환해야합니다. 리턴을 하지않으면 자동으로 `retun null;` 처리합니다.