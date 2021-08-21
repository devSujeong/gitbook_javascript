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

