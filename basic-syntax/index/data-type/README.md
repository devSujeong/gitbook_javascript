# Data type

## What is Data type?

값의 종류를 뜻합니다. 모든 값은 타입을 가집니다. 값은 크게 2가지로 구분할 수 있습니다.

{% tabs %}
{% tab title="primitive type" %}
* **immutable value**\(변경 불가능한 값\) - 값을 대체하여 새로운 값으로 변수에 재할당은 할 수 있어도, 원시 값 자체를 바꿀 수는 없습니다. 이는 **값의 신뢰성**을 높입니다.

  Ex\) 문자열의 경우 이터러블한 유사배열 객체로 사용이 가능하지만, 문자열 자체가 immutable한 value기 때문에 문자열 자체를 수정할 수는 없습니다. 그러나 수정하려고 할 때 에러를 주진 않습니다.

  ```javascript
  let str = "string";

  str[0] = "S";

  console.log(str); // "string"
  ```

* **변수에 값 자체가 저장** - 변수는 변수가 기억하고 있는 메모리 주소를 통해 메모리 공간에 저장된 실제 원시값에 접근할 수 있습니다. 값 자체에 접근이 가능하므로 **값을 비교할 수 있습니다.**

  ```javascript
  const a = 1;
  const b = 1;

  a === b // true.
  ```

* 다른 변수에 할당하면 원시 값이 복사되어 전달\(**pass by value**\) - 다른 변수에 원래 값을 할당한 뒤, 나의 값을 바꾸어도 다른 변수에 할당된 값은 바뀌지 않습니다.

  ```javascript
  let a = 1;
  let b = a;

  a = 2;

  console.log(a); // 2
  console.log(b); // 1
  ```

* 원시 래퍼 객체\(object wrapper\)를 가지고 있어 메소드를 가지고 있어도 가볍게 사용이 가능합니다.

{% hint style="info" %}
원시 래퍼 객체

원시 값에도 유용한 메서드를 등록하고 가볍게 원시값으로도 사용하고 싶어서 나온 개념입니다. 원시값을 감싼 객체가 메서드를 호출해주고, 호출된 후에 래퍼 객체는 파괴됩니다.
{% endhint %}

* 원시형을 굳이 객체로 생성하면 생성 방법이 더 번거로운 문제도 있지만, 값을 비교할 때 원시값으로 계산하지 않고 객체로 계산되어 예상치 못한 결과가 생성됩니다.

```javascript
let zero = new Number(0);
if (zero) { // 변수 zero는 객체이므로, 조건문이 참이 됩니다.
  alert( "그런데 여러분은 zero가 참이라는 것에 동의하시나요!?!" );
}
```
{% endtab %}

{% tab title="reference type" %}
* **mutable value** - 값을 변경할 수 있습니다. 이는 누군가가 이 값을 조작할 수 있음을 의미합니다.
* **변수에 참조 값이 저장** - 생성된 객체가 저장된 메모리 공간의 주소만 변수에 할당합니다. 따라서 같은 값을 가지고 있는지 **비교할 수 없습니다.**

  ```javascript
  const a = {
      age: 1
  };

  const b = {
      age: 1
  };

  a === b // false
  ```

* 다른 변수에 할당하면 참조 값이 복사되어 전달\(**pass by reference**\) - 다른 변수에 원래 값을 할당하고 나의 값을 바꾸면 다른 변수에도 바뀐 값이 함께 적용됩니다.

  ```javascript
  const a = {
      age: 1
  };

  const b = a;

  a.age = 2;

  console.log(b.age) // 2
  ```

* 원시형 데이터들의 집합이어서 변수의 선언과 할당이 한 번 더 이루어집니다.\(key가 변수가되고 value에 값이 저장된 주소 값이 할당됩니다.\)
{% endtab %}
{% endtabs %}

| 구분 | 데이터 타입 | 설명 |
| :--- | :--- | :--- |
| 원시타입 | [number](https://dev-sujeong.gitbook.io/javascript/basic-syntax/index/data-type/number) | 숫자 |
| 원시타입 | string | 문자열 |
| 원시타입 | boolean | true/false |
| 원시타입 | undefined | 암묵적으로 할당되는 값 |
| 원시타입 | null | 의도적으로 값이 없음을 명시하는 값 |
| 원시타입 | symbol |  |
| 객체타입 |  | 객체, 함수, 배열, regExp, DATE, map, set, weakMap, weakSet ... |

## Why do you need data type?

* 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해
* 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해
* 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해

## Dynamic type

javascript는 동적 타입 언어입니다. 따라서 변수가 선언될 당시가 아닌 할당에 의해 타입이 결정됩니다. \(type infrerence\)

## Type 확인하기

typeof 연산자를 활용합니다.

```javascript
typeof "테스트" // string
```

## 타입 변환

### explicit coercion\(, type casting\)

명시적 타입 변환은 개발자가 의도적으로 값의 타입을 변환하는 것입니다.

#### 문자열 타입으로 변환

* String 생성자 함수를 new 연산자 없이 호출
* Object.prototype.toString 표준 빌트인 메서드 사용
* 문자열 연결 연산자 사

```javascript
String(1); // -> "1"
NaN.toString; // -> "NaN"
true + ''; // -> "true"
```

#### 숫자 타입으로 변환

* Number 생성자 함수를 new연산자 없이 호출
* parseInt, parseFloat 함수 사용\(문자열만 가능함\)
* * unary arithmetic operator
* \\* arithmetic operator

```javascript
Number(true); // -> 1
parseInt('-1'); // -> -1
+'10.43' // -> 10.43
true * 1; // -> 1
```

#### boolean 타입으로 변환

* Boolean 생성자 함수를 new 연산자 없이 호출
* ! 부정 논리 연산자 두 번 사용

```javascript
Boolean('x'); // -> true
!![]; // -> true
```

### implicit coercion\(, type coercion\)

암묵적 타입 변환은 자바스크립트 엔진에 의해 자동으로 변환하는 것입니다. 원시 타입 중 하나로 타입을 자동 변환합니다.

#### 문자열 타입으로 변환

```javascript
1 + '2' // -> "12" +는 문자열 연 연산자
```

#### 숫자 타입으로 변환

```javascript
// Arithmetic operator
1 - '1' // -> 0
1 * '2' // -> 2
1 / 'abc' // -> NaN

// comparison operator
'1' > 0 // -> true

// + unary operator
+'' // -> 0
+true // -> 1
+null // -> 0
```

#### 불리언 타입으로 변환

조건식의 평가 결과는 불리언 타입으로 암묵적 변환됩니다. falsy값 외의 모든 값은 true로 변환됩니다.

* false
* undefined
* null
* 0, -0
* NaN
* ''

