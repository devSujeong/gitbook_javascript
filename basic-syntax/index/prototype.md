# Prototype

## Object oriented programing

자바스크립트는 클래스 기반 객체지향 프로그래밍 언어보다 효율적이며 더 강력한 객체지향 프로그래밍 능력을 지니고 있는 프로토타입 기반의 객체지향 프로그래밍 언어입니다.

## Inheritance

javascript는 prototype을 기반으로 inheritance를 구현합니다. 상속은 코드의 재사용이라는 관점에서 매우 유용합니다. 

```javascript
function Circle(radius) {
    this.radius = radius;
}

Circle.prototype.getArea = function() {
    return Math.PI * this.radius ** 2;
}

const circle1 = new Circle(1);
const circle2 = new Circle(2);

console.log(circle1.getArea === circle2.getArea); // true
```

## Prototype object

prototype \(object\)는 어떤 객체의 상위\(부모\) 객체의 역할을 하는 객체로서 다른 객체에 공유 프로퍼티를 제공합니다. 모든 객체는 \[\[Prototype\]\]이라는 내부 슬롯을 가지며 이 내부 슬롯은 프로토타입을 참조합니다. \[\[Prototype\]\]에는 객체가 생성될 때 객체 생성 방식에 따라 프로토타입이 결정됩니다.

### --proto-- \(\_\_로 써야 하지만 여기에서 제대로 표시되지 않는다\)

모든 객체는 --proto-- 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 \[\[Prototype\]\] 내부 슬롯에 간접적으로 접근할 수 있습니다. 직접 접근하지 않고 --proto--를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서 입니다.

 --proto-- 프로퍼티는 Object.prototype의 프로퍼티인데 모든 객체는 상속을 통해 --proto--를 사용할 수 있습니다. 그러나 es5까지는 비표준이었고, ES6에서 표준이 되었지만 Object.prototype을 상속받지 않는 객체를 생성할 수도 있기 때문에 해당 접근자 프로퍼티를 코드에서 사용하지 않고 대신 getPrototypeOf, setPrototypeOf 메서드를 사용할 것을 권장합니다.

```javascript
const obj = {};
const parent = { x: 1 };

Object.getPrototypeOf(obj); // obj.__proto__
Object.setPrototypeOf(obj, parent); // obj.__proto__ = parent

console.log(obj.x) // 1
```

## function object's prototype property

함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킵니다. 생성자 함수로 호출할 수 없는 함수 \(arrow function, es6 method shotand\)는 prototype을 소유하지 않습니다.

## Constructor property

all prototype has constructor property. 이 constructor property는 prototype property로 자신을 참조하고 있는 생성자 함수를 가리킵니다.

## Prototype 생성

객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 객체화되어 존재합니다. 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토타입은 생성된 객체의 \[\[Prototype\]\] 내부 슬롯에 해당합니다.

### 리터럴로 생성한 객체의 프로토타입

리터럴로 객체를 생성할 때 전달되는 프로토타입은 Object.prototype입니다. Object 생성자 함수에 의해 생성된 객체의 프로토타입도 동일합니다.

```javascript
const obj = { x: 1 };
const obj2 = new Object();

console.log(obj.constructor === Object) // true
console.log(obj1.constructor === obj2.constructor) // true
```

### 사용자 정의 생성자 함수의 프로토타입

함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성됩니다. 늘 Object.prototype입니다.

### 사용자 정의 생성자 함수로 생성한 객체의 프로토타입

프로토타입이 사용자 정의 생성자 함수가 되며, 이는 Object.prototype와 달리 사용자 정의 생성자 함수에서 내가 만든 프로퍼티나 메소드를 제외하고는 constructor만 갖고 있습니다. 그러나 결국 사용자 정의 생성자 함수 자체의 프로토타입이 Object.prototype이므로 프로토타입 체인에 의해 이 인스턴스 역시 Object.prototype의 프로퍼티 사용할 수 있습니다.

### 빌트인 생성자 함수의 프로토타입

빌트인 생성자 함수가 생성되는 시점에 프로토타입이 생성됩니다. 모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성됩니다. 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티입니다.

## Prototype chain

javascript는 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 \[\[Prototype\]\] 내부 슬롯의 참조를 따라서 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색합니다.

* 프로토타입 체인 - 프로퍼티 검색을 위한 메커니즘
* 스코프 체인 - 식별자 검색을 위한 메커니즘

## Overriding and property shadowing

프로토 타입이 소유한 프로퍼티를 프로토타입 프로퍼티  
인스턴스가 소유한 프로퍼티를 인스턴스 프로퍼티라고 합니다.  
프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에도 추가하면 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가합니다. 이 현상을 오버라이딩한다고 표현하고, 오버라이딩에 의해서 \(상속 관계에 의햇\) 프로퍼티가 가려지는 현상을 property shadowing이라고 합니다.

재정의하는 것이기 때문에 인스턴스 프로토타입을 삭제해도 프로토타입 프로퍼티는 삭제되지 않습니다.  
하위 객체가 프로토타입 프로퍼티를 프로토 접근자 프로퍼티로 접근한다 하더라도 삭제할 수 없으며 프로토타입 프로퍼티를 삭제하려면 직접 프로토타입에 접근해야 합니다.

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function() {
    console.log(`Hi, My name is ${this.name}`);
}

const me = new Person('kim sujeong');

delete me.sayHello // error
delete Person.prototype.sayHello // ok
```

## Prototype 교체

프로토타입은 임의의 다른 객체로 변경 가능합니다. 동적으로 부모 객체를 바꿀 수 있다는 뜻입니다.

### 생성자 함수에 의한 프로토타입 교체

미래에 생성할 인스턴스의 프로토타입을 교체한다는 뜻입니다.

```javascript
const Person = (function() {
    function Person(name){
        this.name = name;
    }
    
    // Person의 prototype을 객체로 바꿔버림.
    Person.prototype = {
        sayHello() {
            console.log(`Hi, My name is ${this.name}`);
        }
    }
}());
```

### 인스턴스에 의한 프로토타입 교체

이미 생성된 객체의 프로토타입을 교체하는 것입니다.

```javascript
function Person(name) {
    this.name = name;
}

const me = new Person("sujeong");

const parent = {
    sayHello() {
        console.log(`Hi, My name is ${this.name}`);
    }
};

// me 객체의 prototype을 parent로 바꿈.
Object.setPrototypeOf(me, parent);
me.__proto__ // parent
```

## instanceOf operator

생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인합니다.

```javascript
function Person(name) {
    this.name = name;
}

const me = new Person("sujeong");

me instanceOf Person // true
me instanceOf Object // true
```

## Object.create 직접 상속

첫 번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성합니다. 즉, 객체를 생성하면서 직접적으로 상속을 구현하는 것입니다. 이는 아래와 같은 장점이 있습니다.

* new 연산자가 없어도 객체를 생성 할 수 있습니다.
* 프로토타입을 지정하면서 객체를 생성할 수 있습니다.
* 객체 리터럴에 의해 생성된 객체도 상속받을 수 있습니다.

그러나 ESLint에서는 Object.prototype 빌트인 메서드를 객체가 직접 호출하는 것을 권장하지 않습니다. Object.create로 만들어진 객체는 Object.prototype을 상속받지 않은 객체도 만들 수 있기 때문입니다.

```javascript
let obj = Object.create(null);
Object.getPrototypeOf(obj) === null // true

obj = Object.create(Object.prototype);
Objct.getPrototypeOf(obj) === Object.prototype // true

obj = Object.create(Object.prototype, {
    x: {value: 1, writable: true, enumerable: true, configurable: true}
});
Object.getPrototypeOf(obj) === Object.prototype // true

const myProto = {x: 10};
obj = Object.create(myProto);
Object.getPrototypeOf(obj) === myProto // true

function Person(name){
    this.name = name;
}
obj = Object.create(Person.prototype);
Objct.getPrototypeOf(obj) === Person.prototype // true
```

## \_\_proto\_\_ 에 의한 직접 상속

```javascript
const myProto = {x: 10};

const obj = {
    y: 20,
    __proto__: myProto
};

Object.getPrototypeOf(obj) === myProto
```

## static property/method

인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메소드. 인스턴스로 참조/호출할 수 없습니다.

```javascript
function Person(name){
    this.name = name;
}

Person.prototype.sayHello = function() {
    console.log(`Hi! My name is ${this.name}`);
};

// static property
Person.staticProp = 'static prop';

// static method
Person.staticMethod = function() {
    console.log('static method');
}

const me = new Person('kim');

Person.staticMethod(); // 가능
me.staticMethod(); // error
```

## property 확인

### in 연산자\(=Reflect.has\(\)\)

객체 내에 특정 프로퍼티가 존재하는지 여부를 확인합니다. in 연산자는 해당 객체의 프로퍼티 뿐만 아니라 상속받은 프로토타입의 프로퍼티도 확인합니다.

```javascript
const person = {
    name: 'kim',
    address: 'Seoul'
};

'name' in person // true
Reflect.has(person, 'name') // true
```

### Object.prototype.hasOwnProperty

해당 객체에 속해있는 프로퍼티만 존재하는지 확인합니다. 상속받은 프로토타입의 프로퍼티는 검사하지 않습니다.

```javascript
person.hasOwnProperty('name')
```

## property 열거

### for...in문

객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 \[\[Enumerable\]\]의 값이 true인 프로퍼티를 순회하며 열거합니다. 순회할 때 순서를 보장하지 않습니다.

```javascript
const person = {
    name: 'kim',
    address: 'Seoul'
};

for(const key in person) {
    console.log(key + ': ' + person[key]);
}
```

### Object.keys/values/entries

객체 자신이 가지고 있는\(상속받지 않은\) 프로퍼티만 열거하기 위해서 사용합니다.

* Object.keys : 객체 자신의 열거 가능한 프로퍼티 키를 배열로 반환
* Object.values : 객체 자신의 열거 가능한 프로퍼티 값을 배열로 반환
* Object.entries : 객체 자신의 열거 가능한 프로퍼티 키와 값의 쌍의 배열을 배열로 반환

```javascript
const person = {
    name: 'kim',
    address: 'Seoul',
    __proto__: {age: 20}
};

Object.keys(person) // ["name", "address"]
Object.values(person) // ["kim", "Seoul"]
Objct.entries(person) // [["name", "kim"], ["address", "Seoul"]
Object.entries(person).forEach(([key, value]) => console.log(key, value));
```

