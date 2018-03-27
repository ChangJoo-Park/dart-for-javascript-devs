# 렉시컬 스코프와 클로저

자바스크립트와 마찬가지로 Dart 언어 또한 렉시컬 스코프와 클로저를 가지고 있습니다. 이 말은 변수의 범위는 포함된 영역에 따라 바뀌게 된다는 것을 의미합니다.

## 렉시컬 스코프 

```dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```

각 변수들은 자신이 포함된 영역을 기준으로 영향을 미칩니다. `nestedFunction()`의 경우 자신을 감싸고 있는 모든 상위 변수에 접근할 수 있습니다.


## 렉시컬 클로저

클로저는 함수가 원래 범위 밖에서 사용되는 경우에도 해당 렉시컬 스코프의 변수에  접근할 수 있는 함수 객체입니다.


```dart
Function makeAdder(num addBy) {
  return (num i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```

`makeAdder` 함수는 숫자 2와 4를 가지고 있다가 다시 호출할 때 사용합니다.
