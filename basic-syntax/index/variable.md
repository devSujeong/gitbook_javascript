---
description: 변수
---

# Variable

## 컴퓨터의 동작원리에서 보는 변수의 필요

사람이 두뇌를 통해 무엇을 기억하고 처리하는 것처럼 컴퓨터도 기억은 memory에서 연산은 CPU에서 처리합니다. 컴퓨터는 memory cell에 데이터를 저장할 수 있고, memory cell 하나의 크기는 1byte\(8bit\)이며 컴퓨터는 1byte 단위로 데이터를 write\(저장\)하거나 read\(읽어 들입니다.\)

그러나 우리가 컴퓨터의 memory address를 통해 값에 직접 접근하면 치명적인 오류가 생길 가능성이 많습니다. \(데이터의 주소가 매번 바뀌는 동작 원리 등으로 인해\) 그래서 안전하게 memory에 접근할 수 있는 variable을 만듭니다. 또한 변수로 만드는 것이 개발자가 코드를 작성할 때도 의미를 담을 수 있어 데이터에 대한 이해가 빠를 것입니다.

## What is Variable?

**값**을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름. 상징적인 이름이지만 개발자가 데이터의 의미를 빠르게 파악할 수 있습니다. 즉, variable은 값 자체를 기억하는 게 아니라 값이 저장된 메모리 주소를 기억하는 것입니다.

```javascript
var result; // (1)
var result = 10 + 20; // (2)
result // (3)
```

* \(1\)의 `result`는 variable name \(변수이름\). var로 변수를 선언할 때는 variable declaration\(변수 선언\).  + undefined initialization\(변수 초기화\) 같이 일어남.
* \(2\)는 variable assignment\(변수 할당\)
* \(3\)은 reference \(참조\)

## Variable declaration

변수를 생성하는 것입니다. 자바스크립트에게 자신의 존재를 알리는 것이며 구체적으로는 메모리 공간을 allocate\(확보\)하고 변수 이름과 확보된 메모리 공간의 주소를 name binding\(연결\)해서 값을 저장할 수 있게 준비하는 것입니다. 이 메모리 공간은 release\(해제\)되기 전까지 보호됩니다. variable declaration은 `var`, `let`, `const` 와 같은 키워드로 구현합니다.

{% hint style="warning" %}
### Reference Error

variable declaration을 한 번도 하지 않은 identifier에 접근하면 Reference Error가 납니다. javascript execution context\(실행 컨텍스트\)에 등록되지 않았으니 찾을 수가 없는 것이죠.
{% endhint %}

### Variable Hoisting

hoisting은 변수 선언이 **스코프**의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징입니다. 자바스크립트 엔진은 runtime\(소스코드가 실행되는 시점\) 이전에 소스코드를 평가하는 과정을 거칩니다. 이때 모든 선언문들은 먼저 실행\(hoisting\)이 되고, 그 이후에 코드가 한 줄 씩 순차적으로 실행됩니다. variable reference를 먼저 하고 나중에 variable declaration을 하여도 오류가 나지 않는 것은 variable hosting을 할 때, variable declaration과 variable initialization을 같이 한다는 증거입니다. 그러나 let, const는 declaration과 initialization을 같이 하지 않습니다.

## Variable assignment

assignment와 declaration은 실행 시기가 다릅니다. assignment는 runtime에서 실행되고, declaration은 before runtime\(hoisting\)에 실행되므로 아래 예제에서 score는 80이 됩니다.

```javascript
score = 80;
var score;

console.log(score) // 80
```

### Re-assignment

값을 다시 할당하면 재할당이 되는데, 이 때 기존 메모리 주소에 값을 덮어 씌우는 것이 아니라 새로운 공간에 값을 담고 그 주소를 mapping합니다. 이러면 garbage collector가 더 이상 참조하지 않는 메모리 주소를 release합니다.

## Identifier naming rules

1. 문자, 숫자, \_, $만 이름 지을 수 있습니다.
2. 첫 글자로 숫자가 올 수 없습니다.
3. reserved word\(예약어\)는 사용할 수 없습니다.
4. javascript에서는 변수와 함수에는 camel case를 권장하고 생성자 함수, 클래스의 이름에는 pascal case를 권장합니다.
5. es5부터 한글, 일본어 식별자도 사용가능하지만 권장하지 않습니다.
6. 대소문자는 구분됩니다.

## variable life cycle

global variable은 전역 [스코프](../../environment/background/scope.md)를 가지기 때문에 application의 종료와 함께 끝납니다. 즉, garbage collector의 수집 대상이 끝까지 되지 못합니다. local variable은 함수의 실행과 함께 시작되어 함수가 종료되면 끝이 납니다.

### global variable's problem

1. implicit coupling\(암묵적 결합\)

   코드 전역에서 참조하고 변경이 가능하므로 코드의 가독성이 나빠지고 의도치 않게 상태가 변경될 가능성도 높습니다.

2. long life cycle

   garbage collector의 수집 대상이 끝까지 되지 못하므로 오류에 빠지기도 쉽고 메모리 공간 활용도도 낮습니다.

3. 스코프 체인 상에서 종점에 존재

   전역 스코프는 스코프 체인을 탈 때 가장 마지막에 검색되는 것이므로 전역 변수의 검색 속도가 가장 느립니다.

4. Namespace의 오염

   자바스크립트는 파일이 분리되어 있어도 하나의 전역스코프를 공유하므로 의도치 않게 값을 바꿔버릴 수 있습니다.

### global variable 사용을 억제하는 방법

1. 즉시실행함수

   즉시실행함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 됩니다.

2. 네임 스페이스 객체

   전역에 네임스페이스 역할을 담당할 객체를 생성하고, 네임 스페이스 객체의 property로 전역 변수를 추가합니다. 그러나 네임 스페이스 객체도 전역변수로 할당되므로 유용해 보이진 않습니다.

   ```javascript
   var MYAPP = {};

   MYAPP.name = 'kim';
   ```

3. module pattern

   클래스를 모방해 관련이 있는 변수와 함수를 즉시실행함수로 감싸서 하나의 모듈을 만듭니다.

   ```javascript
   var Counter = (function() {
       var num = 0; // private

       return {
           increase() {
               return ++num;
           }
       }
   }());

   console.log(Counter.num); // undefined
   console.log(Counter.increase()); // 1;
   ```

4. es6 module

   es6는 전역 변수를 사용할 수 없습니다. 모듈 파일 자체의 독자적인 모듈 스코프가 생깁니다.

## var vs let vs const

세 변수의 특징과 차이점을 정리합니다. es6+ 이상의 자바스크립트 개발을 할 때는 더 이상 var를 사용하지 않고 의도적인 재할당을 방지하기 위해 먼저 const로 변수를 정의하고, 이후 재할당이 필요한 경우에만 let을 사용하되, 변수의 scope를 최대한으로 제한합니다.

{% tabs %}
{% tab title="var" %}
* 중복 선언 허용: 주의하지 않으면 의도치 않게 변수의 값을 바꿔버릴 수 있습니다.
* function level scope
* hoisting: hoisting하면서 undefined로 initialization합니다.
* window 객체의 속성으로 접근 가능.
{% endtab %}

{% tab title="let" %}
* hoisting 시에는 declaration만 하고 Temporal Death Zone 상태로 둡니다. 이는 undefined로 initialization하지 않고 runtime때 변수가 declaration 시에 undefiend를 할당합니다. 따라서 reference syntax error가 발생되고 이는 변수 중복 선언을 금지하는 효과가 됩니다.

> hoisting\(declaration\) -&gt; TDZ -&gt; initialization step -&gt; assignment step

* block level scope: {} 단위에 변수의 유효범위가 갇힙니다.
* for문의 i변수도 block scope로 인정합니다.
* 전역 객체의 프로퍼티가 아닌 전역 변수로만 존재합니다.
{% endtab %}

{% tab title="const" %}
* block level scope
* 반드시 declaration과 동시에 assignment 해야 합니다.
* tdz 존재
* 불변을 의미하는 게 아니라 재할당을 금지. 
* 원시 값을 할당한 경우 변수 값을 변경할 수 없습니다.
* 즉, 참조값을 할당한 경우에는 값을 변경할 수 있습니다.
* 기존 for문을 제외하고 for문에서 const 사용 가능

```javascript
for (const prop in obj) {
  console.log(prop)
}
```
{% endtab %}
{% endtabs %}

## variable rules

* 변수는 꼭 필요한 경우에 한해 제한적으로 사용합니다. 변수의 개수가 많을 수록 타입이 바뀔 수 있는 여지가 생기고 오류가 발생할 확률이 높아집니다.
* 변수의 scope는 최대한 좁게 만들어 빨리 메모리에서 사라지게 합니다.
* 전역 변수는 최대한 사용하지 않습니다. 의도치 않게 값이 오염될 여지가 많고 다른 코드에 side effect를 줄 수 있습니다.
* 변수 보다는 상수를 사용해 값의 변경을 억제합니다.
* 변수 이름은 변수의 목적이나 의미를 담아서 짓습니다.

