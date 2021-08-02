# Data type

## What is Data type?

값의 종류를 뜻합니다. 모든 값은 타입을 가집니다. 값은 크게 2가지로 구분할 수 있습니다.

{% tabs %}
{% tab title="primitive type" %}
* 각 저장공간의 값을 이용하여 비교가 가능합니다.
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
* d원시형 데이터들의 집합이어서 변수의 선언과 할당이 한 번 더 이루어집니다.\(key가 변수가되고 value에 값이 저장된 주소 값이 할당됩니다.\)
* 참조형 데이터들은 어느 한 부분의 값을 변경하면 전체가 변경됩니다.
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





