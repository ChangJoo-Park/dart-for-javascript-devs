# 에러 핸들링 Exception과 Error

Dart는 자바스크립트와 마찬가지로 throw - catch를 지원합니다. Exception은 예측하지 못한 결과로 인한 에러입니다. Exception이 catch 되지 않으면 프로그램이 중단됩니다.

모든 Dart의 Exception은 확인되지 않은 Exception입니다. 메소드는 throw 가능한 Exception을 선언하지 않으며,  Exception을 catch할 필요가 없습니다.

Dart는 Exception과 Error 타입을 제공합니다. 물론 사용자 정의 Exception도 만들 수 있습니다. Dart 프로그램은 Exception 및 Error 객체뿐만 아니라 모든 null이 아닌 객체를 Exception으로 throw할 수 있습니다.

## Throw

에러인 경우 강제로 Exception을 발생시킬 수 있습니다.

```dart
throw new FormatException('Expected at least 1 section');
```

문자열로도 발생시킬 수 있습니다.

```dart
throw 'Out of llamas!';
```

일반적으로 프로덕션 레벨의 코드는 Error또는 Exception을 throw 합니다.

## Catch

Error를 처리하거나 다시 발생시키지 않으면 예외가 다른 곳으로 영향을 주지 않습니다. 예외를 catch하면 됩니다.

```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```

에러는 여러가지 타입이 있습니다. 각 에러 타입에 따라 다른 처리를 해야하면 아래와 같이 합니다. 자바스크립트에는 없는 `on` 키워드가 있습니다. 에러 핸들러가 Exception 객체가 필요할 떄 `catch`를 사용하세요.

```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```

`catch` 는 한개 또는 두개의 매개변수를 지정할 수 있습니다.
첫번째 매개변수는 throw된 Exception이고, 두번째는 StackTrace입니다.

```dart
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

특정 메소드에서 Exception 중 일부만 처리하고 상위로 전파하려는 경우에 `rethrow` 키워드를 사용합니다.

```dart
final foo = '';

void misbehave() {
  try {
    foo = "You can't change a final variable's value.";
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

## Finally

`finally` 키워드는 `try`, `catch` 두 블럭의 코드를 실행한 후 최종적으로 실행하는 코드블럭입니다. 자바스크립트와 동일합니다.
