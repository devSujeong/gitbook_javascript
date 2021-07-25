---
description: 변수
---

# Variable

## 컴퓨터의 동작원리에서 보는 변수의 필요

사람이 두뇌를 통해 무엇을 기억하고 처리하는 것처럼 컴퓨터도 기억은 memory에서 연산은 CPU에서 처리합니다. 컴퓨터는 memory cell에 데이터를 저장할 수 있고, memory cell 하나의 크기는 1byte\(8bit\)이며 컴퓨터는 1byte 단위로 데이터를 write\(저장\)하거나 read\(읽어 들입니다.\)

그러나 우리가 컴퓨터의 memory address를 통해 값에 직접 접근하면 치명적인 오류가 생길 가능성이 많습니다. \(데이터의 주소가 매번 바뀌는 동작 원리 등으로 인해\) 그래서 안전하게 memory에 접근할 수 있는 variable을 만듭니다. 또한 변수로 만드는 것이 개발자가 코드를 작성할 때도 의미를 담을 수 있어 데이터에 대한 이해가 빠를 것입니다.

## What is Variable?

값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름. 상징적인 이름이지만 개발자가 데이터의 의미를 빠르게 파악할 수 있습니다. 즉, variable은 값 자체를 기억하는 게 아니라 값이 저장된 메모리 주소를 기억하는 것입니다.

```javascript
var result; // (1)
var result = 10 + 20; // (2)
result // (3)
```

* \(1\)의 `result`는 variable name \(변수이름\). 저 행위는 variable declaration\(변수 선언\).  + undefined initialization\(변수 초기화\).
* \(2\)는 variable assignment\(변수 할당\)
* \(3\)은 reference \(참조\)

## Variable declaration

변수를 생성하는 것입니다. 자바스크립트에게 자신의 존재를 알리는 것이며 구체적으로는 메모리 공간을 allocate\(확보\)하고 변수 이름과 확보된 메모리 공간의 주소를 name binding\(연결\)해서 값을 저장할 수 있게 준비하는 것입니다. 이 메모리 공간은 release\(해제\)되기 전까지 보호됩니다.

variable declaration은 `var`, `let`, `const` 와 같은 키워드로 구현합니다. 아직 assignment를 하지 않아서 값이 비어있을 것 같지만 javascript는 암묵적으로 undefined value로 initialization 되어 있습니다.

{% hint style="warning" %}
### Reference Error

variable declaration을 하지 않은 identifier에 접근하면 Reference Error가 납니다. javascript execution context\(실행 컨텍스트\)에 등록되지 않았으니 찾을 수가 없는 것이죠.
{% endhint %}

### Variable Hoisting

자바스크립트 엔진은 runtime\(소스코드가 실행되는 시점\) 이전에 소스코드를 평가하는 과정을 거칩니다. 이때 모든 선언문들은 먼저 실행이 되고, 그 이후에 코드가 한 줄씩 순차적으로 실행됩니다. variable declaration 전에 variable reference를 하여도 오류가 나지 않는 것은 variable hosting을 할 때, variable declaration과 variable initialization을 같이 한다는 증거입니다.

## Variable assignment

assignment와 declaration은 실행 시기가 다릅니다. assignment는 runtime에서 실행되고, declaration은 before runtime에 실행되므로 아래 예제에서 score는 80이 됩니다.

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

