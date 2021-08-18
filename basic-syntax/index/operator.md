---
description: 연산자
---

# Operator

## Operator

연산자는 value\(값\)로 evaluation\(평가\)되는 operand\(피연산자\)를 가지고 산술, 할당, 비교, 리, 타입, 지수 연산 등을 수행하여 하나의 값을 만듭니다.

## Arithmetic operator\(산술 연산자\)

수학적 계산을 수행합니다. 산술 연산이 불가능한 경우, NaN을 반환합니다.

{% tabs %}
{% tab title="binary arithmetic operator" %}
이항연산자는 operand의 값을 바꾸는 side effect가 없습니다.

`+`\(덧셈\), `-`\(뺄셈\), `*`\(곱셈\), `/`\(나눗셈\), `%`\(나머지\)
{% endtab %}

{% tab title="unary arithmetic operator" %}
단항 산술 연산자는 side effect가 있을 수도 있습니다.

* `++`: 증가. operand 값이 증가함. prefix 연산자라면 operand 값이 바뀌고 다른 연산 수행하고 postfix 연산자라면 다른 연산 수행 후 operand의 값이 바
* `--`: 감소. operand 값이 감소함. prefix 연산자라면 operand 값이 바뀌고 다른 연산 수행하고 postfix 연산자라면 다른 연산 수행 후 operand의 값이 바뀜 
* `+`: 산술 효과는 없음. 암묵적인 숫자형 변환, 문자열 연결 연산자로 사용.
* `-`: 양수를 음수로, 음수를 양수로 바
{% endtab %}
{% endtabs %}

## Assignment operator\(할당 연산자\)

우항에 있는 operand 평가 결과를 좌항에 있는 변수에 할당합니다. 좌항의 값을 바꾸는 side effect가 있습니다. 할당문은 값으로 평가되는 표현식인 문이기 때문에 변수에 할당할 수 있습니다.

```javascript
a = b = c = 0;
```

* `=` : 우항의 값을 좌항에 assignment
* `+=` : 좌항의 값에 우항의 값을 더해서 좌항에 할당 
* `-=` : 좌항의 값에 우항의 값을 빼서 좌항에 할당
* `*=` : 좌항의 값에 우항의 값을 곱해서 좌항에 할당
* `/=` : 좌항의 값에 우항의 값을 나눠서 좌항에 할당
* `%=` : 좌항의 값에 우항의 값을 나눈 나머지를 좌항에 할당

## Comparison operator\(비교 연산자\)

좌항과 우항의 피연산자를 비교한 다음 그 결과를 불리언 값으로 반환합니다.

* loose equality: 동등 비교 \(==, !==\): x와 y의 값이 같은지 여부를 반환. 암묵적으로 타입을 일치시킨 후 같은 값인지 비교.
* strict equality: 일치 비교 \(!=, !==\): x와 y의 값과 타입이 같은지 여부를 반환. **권장**

> 예외 사항
>
> \(1\) NaN은 자신과 일치 하지 않습니다.
>
> ```javascript
> NaN === NaN // false
> isNaN(NaN) // true
> Object.is(NaN, NaN) // false
> ```
>
> \(2\) 0과 -0은 같습니다.
>
> ```javascript
> 0 === -0 // true
> Object.is(-0, +0) // false
> ```

### **대소 관계 비교 연산**

* `>` : 좌항이 우항보다 크다 
* `<` : 좌항이 우항보다 작다
* `>=` : 좌항이 우항보다 크거나 같다
* `<=` : 좌항이 우항보다 작거나 같다

## Ternary operator\(삼항 연산자\)

조건식의 평가 결과에 따라 반환할 값을 결정합니다. 값으로 평가할 수 있는 표현식인 문입니다.

> 조건식 ? 조건식이 true일 때 반환 값 : 조건식이 false일 때 반환 값

## Logical operator\(논리 연산자\)

* `||` : or. 좌항과 우항 중 하나라도 true면 true
* `&&` : and. 좌항과 우항 둘 다 true여야 true
* `!` : 부정. 값의 반대를 boolean으로 나타냄

## Comma operator\(쉼표 연산자\)

왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피연산자의 평가가 끝나면 마지막 피연산자의 평가 결과를 반환

```javascript
x = 1, y = 2, z = 3; // 3
```

## Group operator\(그룹 연산자\)

`()`로 연산자의 우선순위를 높입니다.

## typeof operator

operand의 data type을 문자열로 반환합니다.

반환의 종류: string, number, boolean, undefined, symbol, object, function

아쉬운 점은 이를 제외한 거의 모든 것이 object로만 표현된다는 것입니다. null, array, Date, regExp 등등..

## 지수연산자

좌항의 피연산자를 base\(밑\)으로 우항의 피연산자를 exponent\(지수\)로 거듭 제곱하여 숫자를 반환

```javascript
2 ** 2 // 4
Math.pow(2, 2)
(-5) ** 2 // 25

var num = 5;
num **= 2 // 25

2 * 5 ** 2 // 50 이항 연산자 중에 우선순위가 제일 높
```

## 기타 연산자

* `?.` : 옵셔널 체이닝 연산자
* `??` : null 병합 연산자
* `delete` : 프로퍼티 삭제. side effect 있음
* `new` : 생성자 함수 호출하여 새 인스턴스 생성
* `instanceof` : 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별
* `in` : 프로퍼티 존재 확인

## 연산자 우선순위

1. \(\)
2. new\(매개변수 존재\), \[\]\(프로퍼티 접근\), \(\)\(함수호출\), ?.
3. new\(매개변수 미존재\)
4. x++. x--
5. !x, +x, -x, ++x, --x, typeof, delete
6. \*\*
7. \*, /, %
8. +, -
9. &lt;, &lt;=, &gt;, &gt;=, in, instanceof
10. ==, !=, ===, !==
11. ??
12. &&
13. \|\|
14. 삼항연산자
15. 할당연산자
16. ,

## 단축 평가

### 논리연산자를 사용한 단축 평가

논리 연산자는 피연산자를 타입 변환하지 않고 그대로 반환합니다. 따라서 논리식에서 평가되는 값에 따라 무언가를 실행시킬때 간단하게 사용하기 좋습니다.

| 단축 평가 표현식 | 평가 결과 |
| :--- | :--- |
| true \|\| anything | true |
| false \|\| anything | anything |
| true && anything | anything |
| false && anything | false |

```javascript
if(!done) message = '미완료';
// 위 식을 아래와 같이 간단히 할 수 있습니다.
message = done || '미완료';
```

### optional chaning operator

객체가 가리키기를 기대하는 변수 값이 null이거나 undefined라면 type error가 나면서 프로그램이 강제종료됩니다. 이를 막기 위해서 해당 객체가 null, undefined가 아닐 때 실행하도록 조치를 취합니다.

```javascript
let elem = null;
let value = elem && elem.value; // -> null 
```

이를 더 쉽게 할 수 있는 연산자가 옵셔널 체이닝 연산자 입니다. 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어갑니다. 논리 연산자 &&를 사용할 때는 좌항이 falsy값으로 평가되면 그 값이 사용되는 사이드 이펙트가 있는데, 옵셔널 체이닝 연산자는 오직 null, undefined만 바라봅니다.

```javascript
let elem = null;

let value = elem?.value;

```

### nullish coalescing 연산자

함수 매개 변수의 기본 값을 정할 때 기존에 \|\|로 체킹했지만 이도 마찬가지로 falsy 값들에 대한 side effect가 있었습니다. 이 현상도 null 병합 연산자로 null, undefined 값 일 때에만 우항을 참조하도록 쉽게 해결 할 수 있습니다.

```javascript
function getStringLength(str) {
    str = str || '';
    return str.length;
}
```

```javascript
let foo = null ?? 'default string'; // -> 'default string'
```

## new operator

함수와 함께 쓰여 \[\[constructor\]\] internal method호출함.



