# Function

## function?

function은 일련의 과정을 statement\(문\)으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것입니다. 함수는 객체 타입의 값입니다.

* parameter: 매개변수. 함수 내부로 입력을 전달받는 변수. 예제에서 x, y
* argument: 인수. 입력 값. 예제에서 2, 5
* return value: 반환값. 예제에서 x + y
* name: 함수 이름. 함수 몸체 내에서만 참조할 수 있는 식별자. 예제에서 add

```javascript
// function definition (함수 정의)
function add(x, y) {
    return x + y;
}

// function call/invoke (함수 호출)
add(2, 5);

// function literal -> 객체 값으로 변수에 할당됨.
const f = function add(x, y) {
    return x + y;
}
```

## Why we use function?

* 코드의 재사용성을 높임 -&gt; 유지보수의 편의성을 높이고 코드의 신뢰성을 높임.
* 적절한 함수 이름 사용 -&gt; 코드 내부를 보지 않고도 함수의 역할을 파악하게 도움. 코드의 가독성을 향상

## function definition

정의란 변수에 값을 할당하여 변수의 실체를 명확히 하는 것입니다. 선언과는 다릅니다.

### 함수 선언문

* 함수 리터럴과 동일한 형태
* 함수 이름은 생략할 수 없습니다.
* 표현식이 아닌 문입니

```javascript
function add(x, y) {
    return x + y;
}
```

### 함수 표현식\(function expression\)

* 표현식인 문입니다.

```javascript
const add = function (x, y) {
    return x + y;
}
```

> 함수 호이스팅
>
> 함수 선언문은 선언문이기 때문에 runtime 이전에 자바스크립트 엔진에 의해 먼저 실행됩니다. 따라서 함수 선언문 이전에 함수를 참조할 수 있고, 호출할 수도 있습니다.
>
> 함수 표현식은 선언이 아니기 때문에 함수 호이스팅은 일어나지 않지만 변수 호이스팅이 일어납니다.

### Function constructor function

constuctor function 은 객체를 생성하는 함수입니다. 이런 방법이 존재하기는 하나 가독성도 좋지 않고 closure도 생성하지 않는 등 동작 방식도 다르므로 사용하지 않습니다.

```javascript
const add = new Function('x', 'y', 'return x + y');
```

### Arrow function

항상 익명 함수로 정의합니다.

```javascript
const add = (x, y) => x + y;
```

## function invoke

### parameter, argument

* parameter의 scope는 함수 내부입니다.
* 함수는 parameter의 개수와 argument의 개수가 일치하는지 체크하지 않습니다. argument가 부족하면 undefined입니다. 인수가 초과되면 무시합니다.

### return

* 함수의 실행을 주안하고 함수 몸체를 빠져나가는 역할.
* return 키워드 뒤에 오는 표현식을 평가해 반환. 뒤에 식이 없으면 undefined.

## function type

### Immediately Invoked Function Expression

즉시 실행 함수는 단 한 번만 호출되며 다시 호출할 수 없는 함수입니다. 꼭 그룹연산자 `()` 로 감싸야 합니다.

```javascript
(function() {
    return 3 * 5;
}());
```

### recursive function

재귀함수는 자기 자신을 호출하는 함수입니다.

### nested function

wnd중첩함수는 inner function이라고도 합니다. nested function을 포함하고 있는 함수를 outer function이라고 합니다.

### callback function

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수입니다. 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수\(Higher-Order Function\)이라고 합니다. 함수를 합성하는 방법으로 함수의 변하지 않는 공통 로직은 미리 정의해 두고, 경우에 따라 변경되는 로직은 추상화해서 함수 외부에서 함수 내부로 전달하는 것입니다.

### pure / impure function

순수함수는 어떤 외부 상태에 의존하지 않고 변경하지 않는 side effect가 없는 함수. &lt;-&gt; impure function. 함수의 외부 상태를 변경하면 상태 변화를 추적하지 어려워지므로 비순수 함수를 최대한 줄이는 게 좋습니다.

함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 side effect를 최소화 하고 immutablility를 지행하는 프로그래밍 패러다임입니다. 로직 내에 존재하는 조건문과 반복문을 제거하여 복잡성을 해결하고, 변수 사용을 억제하거나 생명ㅇ주기를 최소화해서 상태 변경을 피해 오류를 최소화하는 것을 목표로 합니다.



