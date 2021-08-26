---
description: 빌트인 객체
---

# Built-in Object

## Object의 분류

* 표준 빌트인 객체\(standard built-in objects/native objects/ global objects\): ECMAScript 사양에 정의된 객체를 말하며 애플리케이션 전역의 공통 기능을 제공합니다. 실행 환경과 상관없이 언제나 사용할 수 있습니다.
* 호스트 객체\(host objects\): ECMAScript 사양에 정의되어 있지 않지만 자바스크립트 실행 환경에서 추가로 제공하는 객체
* 사용자 정의 객체\(user-defined objects\): 표준 빌트인 객체와 호스트 객체처럼 기본 제공되는 객체가 아닌 사용자가 직접 정의한 객체

## Standard built-in objects

40 여 가지의 표준 빌트인 객체를 제공합니다. Math, Reflect, JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체입니다. 

## 원시 값과 래퍼 객체

편리하게 문자열 숫자 불리언 등의 원시값을 생성할 수 있는데도 String, Number, Boolean 등의 표준 빌트인 생성자 함수가 존재하는 이유는 이들을 다루는 프로퍼티나 메서드들을 사용하기 위해서입니다.  
즉, 원시값을 객체처럼 사용하면 그 때만 잠깐 자바스크립트가 원시값과 연관된 객체를 생성하여 그 객체로 프로퍼티나 메서드를 사용하고 다시 원시값으로 되돌립니다. 이 객체를 wrapper object라고 합니다.

문자열, 숫자, 불리언, 심벌은 래퍼 객체가 있으며 이들 외의 원시값인 null 과 undefinedㅇ는 래퍼 객체가 없으므로 객체처럼 사용할 수 없습니다.

## global objects

global objects는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며 어떤 객체에도 속하지 않은 최상위 객체입니다.  
전역 객체는 표준 빌트인 객체와 호스트 객체 그리고 var 키워드로 선언한 전역 변수와 전역 함수를 프로퍼티로 갖습니다. 이는 프로토타입 상속 관계상 최상위임을 의미하는 게 아니고 계층 구조상 프로퍼티로 소유한다는 뜻입니다.

### 빌트인 전역 프로퍼티

* Infinity : 무한대를 나타내는 숫자값
* NaN : Not-a-Number
* undefined

### 빌트인 전역 함수

* eval: 전달받은 문자열을 런타임에 동적으로 자바스크립트 코드로 실행합니다. 단, strict mode에서는 eval 함수가 기존의 스코프를 수정하지 않고 자체적인 스코프를 생성합니다. 그러나 이는 보안에 매우 취약한 방법이며 최적화가 수행되지 않아 일반적인 코드 실행에 비해 처리 속도도 느려서 사용을 금지해야 합니다.

  ```javascript
  eval('1 + 2'); // 3
  ```

* isFinite: 전달받은 인수가 정상적인 유한수인지 검사

  ```javascript
  isFinite(3); // true
  isFinite(null); // true
  isFinite(NaN); // false
  ```

* isNaN: 전달받은 인수가 NaN인지 검사합니다.

  ```javascript
  isNaN(NaN); // true
  ```

* parseFloat: 전달받은 문자열 인수를 부동 소수점 숫자, 즉 실수로 parsing하여 반환

  ```javascript
  parseFloat('3.14'); // 3.14
  ```

* parseInt: 전달받은 문자열 인수를 정수로 반환

  ```javascript
  parseInt('10.123', 10); // 10

  const x = 15;
  x.toString(16); // f. 해당 진수로 변환하여 문자열로 반환.
  ```

* encodeURI / decodeURI: 어느 시스템에서도 읽을 수 있는 아스키 문자 셋으로 변환. 인수로 전달되는 값이 완전한 URI 값이라고 간주합니다.

  ```javascript
  const uri = 'https://example.com?name=김수정';
  const enc = encodeURI(uri);
  const dec = decodeURI(enc);
  ```

* encodeURIComponent / decodeURIComponent: 위와 같은 맥락이나 인수로 전달된 값이 쿼리 스트링의 일부로 간주하여 =, ?, &까지 인코딩합니다.

### 암묵적 전역

선언을 하지 않은 식별자는 암묵적 전역을 일으킵니다. 이는 전역변수의 프로퍼티가 됨을 의미하며, 전역 변수가 된 것은 아니므로 변수 호이스팅이 발생하지 않고 delete 연산자로 삭제할 수 있습니다.

```javascript
function foo() {
    console.log(y);
    y = 20;
}

foo(); // referenceError
```



