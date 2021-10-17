# Object

## Object?

Object를 정의하고 종류를 나누는 표현은 여러 개가 있습니다. 그 용어가 다 다른 것을 의미한다기 보다는 관점에 따라 표현이 다른 것입니다. javascript is Object-based programming. 원시 값을 제외한 모든 값으로써 자바스크립트를 구성하는 거의 모든 것이기도 하고, 원시 값이 아니기에 변경이 가능한 값입니다.

객체는 속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료 구조입니다. 즉, 0개 이상의 프로퍼티로 구성된 집합입니다. **프로퍼티는 key와 value로 구성**됩니다. 함수도 property의 value가 될 수 있는데 이 때는 일반 함수와 구분하기 위해 method라고 부릅니다.

* property: 객체의 **상태**를 나타내는 값(data)
* method: property를 참조하고 조작할 수 있는 **동작**(behavior)

```javascript
const person = {
    name: "Kim", // name = key, "Kim" = value
    age: 31 // name = age, 31 = value
    increase: function() { // method
        this.age++;
    }
};
```

객체는 Class와 Instance를 포함한 개념이기도 합니다.

* Class: 객체의 다른 표현
* Instance: 클래스의 실질적인 개체.

### Object expression

* 원시 값이 아닌 값
* mutable value
* 0개 이상의 property 구성된 집합
* 클래스와 인스턴스

### Object creation

*   Object literal

    간편하지만 인스턴스를 만들 수 없어서 단 하나의 객체만 생성할 수 있습니다.

    ```javascript
    const person = {};
    ```
*   Object constructor function

    여기서 Object는 생성자 함수(constuctor)입니다. 생성자 함수는 new 연산자와 함께 instance객체를 만듭니다.

    ```javascript
    const person = new Object();
    ```
*   constructor function

    인스턴스를 생성하기 위한 템플릿처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있습니다. 일반 함수와 동일하게 만들고 new 연산자와 함께 호출하면 생성자 함수가 됩니다.

    ```javascript
    // constructor
    function Circle(radius) {
        this.radius = radius;
        this.getDiameter = function() {
            return 2 * this.radius;
        }
    }

    const circle1 = new Circle(5);
    ```

    1.  인스턴스 생성과 this 바인딩

        암묵적으로 빈 객체를 만들고 인스턴스는 this에 바인딩됩니다. javascript 영역.
    2.  인스턴스 초기화

        this에 바인딩되어 있는 인스턴스를 초기화합니다. 개발자 영역.
    3.  인스턴스 반환

        완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됩니다. 만일 명시적으로 다른 것을 return문에 적으면 명시한 객체가 반환됩니다. (원시 값 반환하면 원래대로 진행됨)
*   Object.create method

    첫 번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성합니다. 즉, 객체를 생성하면서 직접적으로 상속을 구현하는 것입니다.

    * ```javascript
      function Person(name){
          this.name = name;
      }
      obj = Object.create(Person.prototype);
      ```
* Class

## Property

* Property Key - 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
* Property Value - 자바스크립트에서 사용할 수 있는 모든 값

### Key

키는 **value에 접근할 수 있는 이름**입니다. 빈 문자열을 포함하여 **모든 문자열이나 심벌 값을 사용**할 수 있습니다. 문자열이므로 원래는 key를 따옴표로 묶어야 하지만 **식별자 네이밍 규칙을 지킨다면 따옴표를 사용하지 않아도 됩니다**. 키를 동적으로 생성하고 싶다면 `[]`로 묶어서 사용할 수 있습니다.

hasOwnProperty : 객체의 프로퍼티 키가 **고유한** 프로퍼티 키인지 확인할 때 사용.

```javascript
const key = "name";

const obj = {
    [key]: 'Sujeong';    
};

obj.hasOwnProperty('name')
```

### Property approach

* dot notation(마침표 표기법)
* bracket notation(대괄호 표기법): 대괄호 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 합니다. 또 객체의 프로퍼티 키가 식별자 네이밍 규칙을 지키지 않았을 때에도 접근 가능한 방법입니다.

```javascript
const person = {
    name: "kim",
    1: 10
};

console.log(person.name); // dot notation으로 접근
console.log(person["name"]); // bracket notation
console.log(person[name]); // ReferenceError. name을 키가 아닌 식별자로 인식
console.log(person.age); // undefined. 객체에 없는 프로퍼티에 접근하면 에러가 나지 않음에 주의
console.log(person["1"]) // 10. 숫자 키여도 문자열로 표현하는 게 정석
console.log(person[1]) // 10. 1을 문자열로 자동 형변환하여 계산함.
```

### Property update

```javascript
const person = {
    name: "kim"
};

person.name = "lee";
person.age = 31; // 존재하지 않는 프로퍼티에 값을 할당하면 동적으로 추가됩니다.

delete person.age; // property delete
```

### Property delete

```javascript
const obj = {
    name: 'sujeong'
}

delete obj.name
```

### Property expression

```javascript
// property 축약 표현

let x = 1, y = 2;

const obj = { x, y }; 

console.log(obj); // {x: 1, y: 2}
```

```javascript
// computed property name
const prefix = 'prop';
let i = 0;

const obj = {
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,

    // method shorthand
    print() { 
        console.log(this["prop-1"]);
    }
};

consol.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

## Property attribute

property attribute를 이해하기 위해서는 먼저 internal slot과 internal method를 알아야 합니다. 이들은 ECMAScript에서 사용하는 pseudo property와 pseudo method입니다. 자바스크립트 엔진의 내부 로직이므로 원칙적으로 개발자가 직접 접근하거나 호출할 수 있는 방법을 제공하지 않지만 일부는 제공합니다.

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본 값으로 자동 정의합니다.

* property value
* property writable(갱신 가능 여부)
* property enumerable(열거 가능 여부)
* property configurable(재정의 가능 여부)

```javascript
const person = {
    name: 'kim'
};

Object.getOwnPropertyDescriptor(person, 'name'); // property attribute 확인하는 방법
// 이 메소드는 propertyDescriptor 객체를 반환함.


Object.getOwnPropertyDescriptors(person); // 모든 프로퍼티의 attribute 정보를 확
```

### Property 종류

* data property: 키와 값으로 구성된 일반적인 프로퍼티
  * \[\[Value]] : 프로퍼티 키를 통해 프로퍼티 값에 접근하면 반환되는 값. 프로퍼티 키를 통해 프로퍼티 값을 변경하면 \[\[Value]]에 값을 재할당하고 이 때 프로퍼티가 없으면 프로퍼티를 동적 생성하여 값을 저장함.
  * \[\[Writable]] : 프로퍼티 값의 변경 가능 여부 boolean. false면 읽기 전용
  * \[\[Enumerable]] : 프로퍼티의 열거 가능 여부 boolean. false면 반복문 사용 안됨
  * \[\[Configurable]] : 프로퍼티의 재정의 가능 여부 boolean. false면 프로퍼티 삭제, 값 변경 금지. 단 \[\[writable]]이 true면 \[\[value]] 변경, \[\[writable]] false로 변경 허용.
* accessor property(접근자 프로퍼티): 자체적인 값이 없고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는  접근자 함수로 구성된 프로퍼티
  * \[\[Get]] : 접근자 프로퍼티를 통해 프로퍼티의 값을 읽을 때 호출되는 접근자 함수. getter 함수가 호출되고 그 결과가 프로퍼티의 값으로 반환됨.
  * \[\[Set]] : 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수.
  * \[\[Enumerable]] : 데이터 프로퍼티와 같음
  * \[\[Configurable]] : 데이터 프로퍼티와 같음

```javascript
const person = {
    // data property
    firstNam: 'sujeong',
    lastName: 'kim',

    // accessor property
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
    set fullName(name) {
        [this.firstName, this.lastName] = name.split(' ');
    }
};
```

### Property definition

property attribute를 명시적으로 정의하거나 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의. 이를 통해 객체의 프로퍼티가 어떻게 동작해야 하는지 명확히 알 수 있습니다. defineProperty 메소드를 사용하며, 일부 생략하고 만들면 기본 값이 적용됩니다. 여러 개를 한 번에 정의하려면 Object.definedProperties 메소드를 사용합니다.

```javascript
const person = {};

Object.defineProperty(person, 'firstName', {
    value: 'sujeong',
    writable: true,
    enumerable: true,
    configurable: true
});

Object.defineProperties(person, {
    firstName: {
        value: 'sujeong',
        writable: true,
        enumerable: true,
        configurable: true    
    },
    lastName: {
        value: 'kim',
        writable: true,
        enumerable: true,
        configurable: true    
    },
    fullName: {
        get() {
            return `${this.firstName} ${this.lastName}`;
        }
    }
});
```

## Object 변경 금지

객체는 변경 가능한 값이므로 변경을 방지하기 위한 메서드가 따로 존재합니다. 그러나 이들은 전부 얕은 변경 방지입니다.

| 구분      | 메서                       | <p>프로퍼티</p><p>추가</p> | <p>프로퍼티</p><p>삭</p> | <p>프로퍼티</p><p>값 읽기</p> | <p>프로퍼티</p><p>값 쓰기</p> | <p>프로퍼티</p><p>attribute</p><p>재정</p> |
| ------- | ------------------------ | -------------------- | ------------------- | ---------------------- | ---------------------- | ------------------------------------ |
| 객체 확장 금 | Object.preventExtensions | X                    | O                   | O                      | O                      | O                                    |
| 객체 밀봉   | Object.seal              | X                    | X                   | O                      | O                      | X                                    |
| 객체 동결   | Object.freeze            | X                    | X                   | O                      | X                      | X                                    |

### 객체 확장 금지

프로퍼티 추가가 금지됩니다. 즉 프로퍼티 동적 추가, Object.defineProperty 금지. 확장 가능 여부는 Object.isExtensible로 확인 가능합니다.

```javascript
const person = {name: 'kim'};
console.log(Object.isExtensible(person)); // true

Object.preventExtensions(person)); // 확장 금지

console.log(Object.isExtensible(person)); // false
```

### 객체 밀봉(sealing)

밀봉된 객체는 읽기와 쓰기만 가능합니다.

```javascript
const person = {name: 'kim'};
console.log(Object.isSealed(person)); // false

Object.seal(person)); // 확장 금지

console.log(Object.isSealed(person)); // true
```

### 객체 동결(freezing)

읽기만 가능한 객체입니다.

```javascript
const person = {name: 'kim'};
console.log(Object.isFrozen(person)); // false

Object.freeze(person)); // 확장 금지

console.log(Object.isFrozen(person)); // true
```

### 불변객체

재귀함수를 사용하여 깊은 동결을 이룹니다.

```javascript
function deepFreeze(target){
    if(target && typeof target === 'object' && !Objct.isFrozen(target)) {
        Object.freeze(target);
        Object.keys(target).forEach(key => deepFreeze(target[key]));
    }

    return target;
}
```

## 객체 복사

Object.assign(targetObj, sourceObj); 얕은 복사임. 열거 순서는 지켜짐.

## This

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수입니다. this를 통해 자신 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있습니다. this는 어디서나 참조 가능하지만 용도가 객체의 프로퍼티나 메서드를 참조하기 위함이므로 객체의 메서드 내부, 또는 생성자 함수 내부에서만 의미가 있습니다.

### this binding

this 바인딩은 함수 호출 방식에 의해 동적으로 결정됩니다.

#### 일반 함수 호출

기본적으로 this에는 전역 객체가 바인딩됩니다. 단, strict mode에서는 undefined입니다. 일반 함수 호출은 중첩함수, 콜백 함수도 포함됩니다. 그러나 메서드 안에서의 중첩함수, 콜백함수는 객체의 내부 로직을 담당하는 경우가 많은데 그 객체를 참조하지 못하는 것은 문제가 있을 확률이 높습니다. 이 때는 apply/call/bind 메서드를 사용하거나 arrow function으로 this를 일치시킬 수 있습니다.

```javascript
var value = 1;

const obj = {
    value: 100,
    foo() {
        setTimeout(function() {console.log(this.value)}.bind(this), 100);
    }
};

obj.foo();
```

```javascript
var value = 1;

const obj = {
    value: 100,
    foo() {
        setTimeout() => console.log(this.value), 100);
    }
};

obj.foo();
```

#### 메서드 호출

메서드 내부의 this에는 메서드를 **호출**한 객체가 바인딩 됩니다. 메서드가 만들어진 객체와 상관이 없고 메서드를 호출하는 객체만을 따라갑니다.

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.getName = function() {
    return this.name;
}

const me = new Person('lee');

me.getName(); // lee

Person.prototype.name = 'kim';

Person.prototype.getName(); // kim
```

#### 생성자 함수 호출

생성자 함수 **내부**의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩 됩니다.

### Function.prototype.apply/call/bind

이들은 Function.prototype의 메서드입니다. 즉, 모든 함수가 사용할 수 있습니다.

apply와 call은 인수를 전달하는 방법이 다를 뿐, this를 전달함과 동시에 함수를 호출합니다. 이들은 유사 배열 객체에 배열 메서드를 사용하는 경우에 많이 사용합니다.

```javascript
Function.prototype.apply(thisArg[, argsArray])
// thisArg: this로 사용할 객체
// argsArray: 함수에게 전달할 인수 리스트의 배열 또는 유사 배열 객체

Function.prototype.call(thisArg[, arg1[, arg2[, ...]]])
// argsArray대신 인자 하나 하나로 인수를 넘김
```

```javascript
function convertArgsToArray() {
    const arr = Array.prototype.slice.call(arguments);
}
```

bind는 인수도 전달하지 않고, 함수를 호출하지도 않습니다. this로 사용할 객체만 전달합니다. 따라서 객체 내부의 중첩함수, 콜백함수 등의 this 불일치에 많이 사용됩니다.

```javascript
const person = {
    name: 'kim',
    foo(callback) {
        setTimeout(callback.bind(this), 100);
    }
};

person.foo(function() {
    console.log(this.name);
});
```
