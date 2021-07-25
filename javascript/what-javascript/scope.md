---
description: 변수와 함수랑 관련이 깊은 유효범위에 대해 알아봅시다.
---

# Scope

## What is Scope?

scope란 모든 identifier\(variable, function, class\)가 가진 것으로 다른 코드가 자신을 reference 할 수 있는 범위입니다.

## Scope type

* Global scope: 코드의 가장 바깥 영역으로 전역 변수입니다.
* Local scope: 함수 내부까지만 영향을 미치는 지역 변수입니다.

## Scope chain

scope chain이란 scope가 계층적으로 연결된 것을 이릅니다. 모든 지역 스코프의 최상위 스코프는 전역 스코프이며 nested function\(중첩 함수\)들의 중첩 정도에 따라 계층을 다 갖습니다.

> 전역 스코프 &gt; outer function &gt; nested function

javascript는 변수를 참조할 때 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 찾습니다.\(identifier resuolution\) 즉, 상위 스코프에서 선언한 변수는 하위 스코프에서도 사용 가능합니다. 

### scope를 결정하는 방식

scope chain 개념은 중요합니다. 내가 찾고자 하는 식별자의 값을 정확하게 추측할 수 있게 해주기 때문입니다. 상위 스코프를 결정하는 방식은 크게 2가지가 있습니다.

* Dynamic scope: 함수가 호출되는 시점에 동적으로 상위 스코프를 결정함
* Lexical scope\(or Static scope\): 함수 정의가 평가되는 시점에 상위 스코프가 정적으로 결정됨.

javascript는 lexical scope를 따르기 때문에 함수가 선언된 곳의 scope를 따져야 합니다. 즉, 함수가 생성될 때 함수 객체는 결정된 상위 스코프를 계속 reference하고 있을 것이며 이를 이용해 우리는 closure 를 만들 수 있습니다.

## scope + hoisting

hoisting은 변수 선언이 스코프의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징입니다. 따라서 전역 스코프는 전역에서 실행되기 전에 모든 identifier가 hoisting되고, 함수가 실행될 때 함수 내부의 모든 identifier가 hoisting됩니다.

