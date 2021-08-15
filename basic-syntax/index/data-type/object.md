# Object

## Object?

Object를 정의하고 종류를 나누는 표현은 여러 개가 있습니다. 그 용어가 다 다른 것을 의미한다기 보다는 관점에 따라 표현이 다른 것입니다. javascript is Object-based programming. 원시 값을 제외한 모든 값으로써 자바스크립트를 구성하는 거의 모든 것이기도 하고, 원시 값이 아니기에 변경이 가능한 값입니다.

객체는 0개 이상의 프로퍼티로 구성된 집합입니다. **프로퍼티는 key와 value로 구성**됩니다. 함수도 property의 value가 될 수 있는데 이 때는 일반 함수와 구분하기 위해 method라고 부릅니다.

* property: 객체의 상태를 나타내는 값\(data\)
* method: property를 참조하고 조작할 수 있는 동작\(behavior\)

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

### Object creation methods

* Object literal
* Object constructor function
* constructor function
* Object.create method
* Class

## Property

* Property Key - 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
* Property Value - 자바스크립트에서 사용할 수 있는 모든 값

### Key

키는 **value에 접근할 수 있는 이름**입니다. 빈 문자열을 포함하여 **모든 문자열이나 심벌 값을 사용**할 수 있습니다. 문자열이므로 원래는 key를 따옴표로 묶어야 하지만 **식별자 네이밍 규칙을 지킨다면 따옴표를 사용하지 않아도 됩니다**. 키를 동적으로 생성하고 싶다면 `[]`로 묶어서 사용할 수 있습니다. 

```javascript
const key = "name";

const obj = {
    [key]: 'Sujeong';    
};
```

### Property approach

* dot notation\(마침표 표기법\)
* bracket notation\(대괄호 표기법\): 대괄호 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 합니다. 또 객체의 프로퍼티 키가 식별자 네이밍 규칙을 지키지 않았을 때에도 접근 가능한 방법입니다.

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

