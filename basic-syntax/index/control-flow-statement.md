---
description: 제어문
---

# Control flow statement

일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행됩니다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있습니다.

## Block statement, compound statement

0개 이상의 문을 중괄호로 묶은 것입니다. javascript는 블록문을 하나의 실행 단위로 취급합니다.

```javascript
{
    let foo = 1;
}
```

## Conditional statement

조건식\(boolean으로 평가될 수 있는 표현식\)의 평가 결과에 따라 코드 블록의 실행을 결정합니다.

### if...else문

논리적 참/거짓으로 실행할 코드를 작성하고자 할 때 사용합니다.

```javascript
if(conditional expression1) {
    // 조건식1이 true면 실행되는 블록문
} else if (conditional expression2) {
    // 조건식2가 true면 실행되는 블록문
} else {
    // 조건식 1과 2가 false면 실행되는 블록문
}
```

### switch문

주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문입니다. 논리적 참, 거짓 보다는 다양한 case에 따라 실행할 코드 블록을 결정할 때 사용합니다.

```javascript
switch(expression) {
    case expression1:
        // expression과 expression1이 일치하면 실행될 문
    break;
    case expression2:
        // expression과 expression2가 일치하면 실행될 문
    break;
    default:
        // expression과 일치하는 case문이 없을 때 실행될 문
        
}
```

## Loop statement

조건식의 평가 결과가 참인 경우 코드 블록을 실행하는데, 거짓일 때까지 반복합니다.

### for

조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행합니다. 반복 횟수가 명확할 때 사용합니다.

> for\(변수 선어문 또는 할당문; 조건식;\) {조건식이 참인 경우 반복 실행될 문}

```javascript
for(let i=0; i < 10; i++) {
    console.log(i);
}
```

### while

평가 결과가 참이면 코드 블록을 반복 실행합니다. 반복 횟수가 불명확할 때 사용합니다. 반복문을 멈추려면 while문 안에 조건문을 만들어 break;를 넣어줍니다.

```javascript
let count = 0;

while(true) {
    console.log(count);
    count++;
    
    if (count === 3) break;
}
```

### do...while

코드 블록을 먼저 실행하고 조건식을 평가합니다. 무조건 한 번 이상은 실행할 때 사용합니다.

```javascript
let count = 0;

do {
    console.log(count);
    count++;
} while (count < 3);
```

## break문

label문\(식별자가 붙은 문. switch문의 case, default문도 레이블 문입니다.\), 반복문 또는 switch문의 코드 블록을 탈출합니다.

## continue문

반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킵니다. 즉, continue문을 만나면 반복을 그 자리에서 멈추고 다음 반복으로 진행이 시작됩니다.

