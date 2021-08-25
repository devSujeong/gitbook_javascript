# background

## Javascript?

javascript의 표준인 ECMAScript가 기본 뼈대를 이루고 브라우저가 별도로 지원하는 ClientSide Web API도 함께 포함됩니다.

{% hint style="info" %}
\*\*\*\*[**ClientSide Web API**](https://developer.mozilla.org/ko/docs/Web/API)\*\*\*\*

DOM, BOM, Canvas, XMLHttpRequest, fetch, requestAnimationFrame, SVG, Web Storage, Web Component, Web Worker ...
{% endhint %}

## Features

* Web browser에서 동작하는 유일한 프로그래밍 언어
* 인터프리터 언어
* 멀티 패러다임 프로그래밍 언어\(명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍 지원\)

## Strict mode

strict mode는 엄격하게 문법을 적용하는 모드를 뜻합니다.  
그러나 이보다 ESLint를 사용하는 것이 코딩 컨벤션을 강제할 수도 있어 더 강력합니다. 또 ES6에서 도입된 클래스와 모듈은 기본적으로 strict mode입니다.

strict mode는 전역의 선두 혹은 함수 몸체의 선두에 `use strict;`를 사용하여 선언합니다.  
그러나 둘 다 권장하지 않습니다. 어디엔 선언하고 어디엔 선언하지 않는 것이 더 오류를 일으킬 수 있기 때문입니다.

* 암묵적 전역 에러: 선언하지 않은 변수는 참조할 수 없습니다.
* delete 연산자로 변수, 함수, 매개변수를 삭제할 수 없습니다.
* 매개변수를 중복된 이름으로 쓸 수 없습니다.
* with문을 사용할 수 없습니다. : with문은 전달된 객체를 스코프 체인에 추가하는 문이라네요.
* 일반 함수로 호출하면 this가 undefined입니다.
* 매개 변수에 값을 재할당해도 arguments 객체에 반영되지 않습니다.

