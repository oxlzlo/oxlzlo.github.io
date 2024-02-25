---
title: 11. 논리 연산자
description: 11. 논리 연산자
date: 2024-02-26
update: 2024-02-26
tags:
  - 패스트캠퍼스
  - 부트캠프
  - 프론트엔드 부트캠프
  - 국비지원교육
  - 내일배움카드
  - KDT
series: "study"
---



# 11. 논리 연산자

# 논리 연산자

- || (OR)
- && (AND)
- ! (NOT)

### || (OR)

- 인수 중 하나라도 ‘true’이면 ‘true’를 반환 하고, 그렇지 않으면 ‘false’를 반환

```jsx
alert (true || true); // true
alert (false || true); // true
alert (true || false); // true
alert (false || false); // false
```

피연산자가 모두 false인 경우를 제외하면 연산 결과는 항상 true

- 피연산자가 불린형이 아니라면, 평가를 위해 불린형으로 변환된다.
    - ex) 연산 과정에서 숫자 1은 true, 숫자 0은 false

```jsx
let hour = 9;

if (hour<10 || hour>18) {
	alert ('영업시간이 아닙니다.');
}
```

OR 연산자는 if문에서 자주 사용된다. ⇒ 주어진 조건 중 하나라도 참인지를 테스트

```jsx
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
  alert( '영업시간이 아닙니다.' ); // isWeekend가 true이기 때문에 alert 실행
}
```

### 첫 번째 truthy를 찾는 OR연산자 ‘||’

- 자바스크립트에서만 제공하는 논리연산사 OR의 ‘추가’기능

- OR 연산자와 피연산자가 여러 개인 경우

```jsx
result = value1 || value1 || value3;
```

1. 가장 왼쪽 피연산자부터 시작해 오른쪽으로 나아가며 피연산자를 평가
2. 각 피연산자를 불린형으로 변환. 변환 후 값이 ture이면 연산을 멈추고 해당 피연산자의 변환 전 원래 값을 반환
3. 피연산자가 모두 false로 평가되는 경우엔 마지막 피연산자를 반환

⚠️ 반환 값은 형 변환을 하지 않는 원래 값

ex:

```jsx
alert( 1 || 0 ); // 1 

alert( null || 1 ); // 1 
alert( null || 0 || 1 ); // 1 

alert( undefined || null || 0 ); // 0 (모두 false이므로, 마지막 값인 0 반환)
```

이런 OR 연산자의 추가 기능을 이용하면 여러 용도로 활용할 수 있다.

1. 변수 또는 표현식으로 구성된 목록에서 첫 번째 truthy 얻기

```jsx
let firstName = "";
let lastName = "";
let nickName = "바이올렛";

alert( firstName || lastName || nickName || "익명"); // 바이올렛
```

fistName, lastName이 빈문자열으로, false라서 첫 번째 truthy값인 ‘바이올렛’ 출력

모든 변수가 falsy였을 경우, ‘익명’이 출력되었을 것이다.

1. 단락 평가

```jsx
true || alert("not printed");
false || alert("printed");
```

첫 번째 줄 코드에서는 처음에 true를 만나고 평가를 멈추기 때문에 alert가 실행되지 않는다.

때문에 두 번째 줄의 alert(’printed’)만 실행된다.

### && (AND)

AND 연산자는 모든 피연산자가 모두 참일 때 true를 반환, 아닐 경우 false 반환

```jsx
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

AND 연산자를 if문과 함께 활용하면 아래와 같다.

```jsx
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
  alert( '현재 시각은 12시 30분입니다.' );
} // 모두 true이기 때문에 alert창 실행

if (1 && 0) { // 피연산자가 숫자형이지만 논리형으로 바뀌어 true && false가 된다
  alert( "if 문 안에 falsy가 들어가 있으므로 alert창은 실행되지 않습니다." );
}
```

### 첫 번째 falsy를 찾는 AND연산자 ‘&&’

- AND 연산자와 피연산자가 여러 개인 경우

```jsx
result = value1 && value2 && value3;
```

1. 가장 왼쪽 피연산자부터 오른쪽으로 나아가며 평가
2. 각 피연산자를 불린형으로 변환. 변환 후 값이 false이면 연산을 멈추고 해당 피연산자의 변환 전 원래 값을 반환
3. 피연산자가 모두 true로 평가되는 경우엔 마지막 피연산자를 반환

ex:

```jsx
// 첫 번째 피연산자가 truthy이면, AND는 두 번째 피연산자를 반환
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// 첫 번째 피연산자가 falsy이면, AND는 첫 번째 피연산자를 반환하고, 두 번째 피연산자는 무시
alert( null && 5 ); // null
alert( 0 && "아무거나 와도 상관없습니다." ); // 0
```

피연산자 여러 개를 연속해서 전달할 경우, 아래와 같다

```jsx
alert( 1 && 2 && null && 3 ); // null
alert( 1 && 2 && 3 ); // 마지막 값, 3
```

ℹ️ &&의 우선순위가 || 보다 높다

`a && b || c && d`는 `(a && b) || (c && d` 와 동일하게 동작

⚠️ **if를 ||나 &&로 대체하지 마세요!**

if문을 짧게 줄이는 용도로 사용하곤 하지만, if문을 사용한 예시가 코드에서 무엇을 구현하고자 하는지

더 명백히 드러내고, 가독성도 좋다.

### ! (NOT)

- NOT 연산자는 인수를 하나만 받고, 다음 순서대로 연산을 수행

```jsx
alert( !true ); // false
alert( !0 ); // true
```

- NOT을 연달아 두 개 사용(!!)하면 값을 불린형으로 변환할 수 있다.

```jsx
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

- 내장 함수 Boolean을 사용하면 ‘!!’를 사용한 것과 같은 결과를 도출할 수 있다.

```jsx
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```

- `NOT` 연산자의 우선순위는 모든 논리 연산자 중에서 가장 높기 때문에 항상 `&&`나 `||` 보다 먼저 실행된다.

## 과제

### 다음 OR연산의 결과는 무엇일까요?

```jsx
alert( null || 2 || undefined ); // 첫 번째 truthy인 2 출력
```

### OR연산자의 피연산자가 alert라면?

```jsx
alert( alert(1) || 2 || alert(3) ); // 첫 번째 truthy인 2까지 출력 (1, 2)
```

### 다음 AND연산의 결과는 무엇일까요?

```jsx
alert( 1 && null && 2 ); // 첫 번째 false인 null 출력
```

### AND연산자의 피연산자가 alert라면?

```jsx
alert( alert(1) && alert(2) );
// && 연산자는 falsy를 만나면 그 값을 출력하고 즉시 연산을 멈추기 때문에
// alert(1)을 평가하며 1을 출력하고, 그의 평가 결과인 undefined 출력
```

### OR AND OR 연산자로 구성된 표현식

```jsx
alert( null || 2 && 3 || 4 );
// &&의 우선순위가 ||보다 높기 때문에 && 먼저 실행
// 2 && 3 = 3이므로, 아래와 같이 바꿔쓸 수 있다.

null || 3 || 4
// 따라서 첫 번째 truthy인 3 출력
```

### 사이 범위 확인하기

`age`(나이)가 `14`세 이상 `90`세 이하에 속하는지를 확인하는 `if`문을 작성하세요.

"이상과 이하"는 `age`(나이) 범위에 `14`나 `90`이 포함된다는 의미입니다.

```jsx
if (age >= 14 && age <= 90)
```

### 바깥 범위 확인하기

`age`(나이)가 `14`세 이상 `90`세 이하에 속하지 않는지를 확인하는 `if`문을 작성하세요.

답안은 NOT `!` 연산자를 사용한 답안과 사용하지 않은 답안 2가지를 제출해 주세요.

```jsx
if (!(age >= 14 && age <= 90));
if (age < 14 || age > 90);
```

### “if”에 관한 고찰

아래 표현식에서 어떤 `alert`가 실행될까요?

`if(...)` 안에 표현식이 있으면 어떤 일이 일어날까요?

```jsx
if (-1 || 0) alert( 'first' ); // (-1 || 0)은 -1(true), 따라서 alert 실행
if (-1 && 0) alert( 'second' ); // (-1 && 0) 은 0(false), 따라서 alert 실행x
if (null || -1 && 1) alert( 'third' );
// => if (null || 1) => if(1) == true, 따라서 alert 실행
```

### 로그인 구현하기

`프롬프트(prompt)` 대화상자를 이용해 간이 로그인 창을 구현해보세요.

사용자가 `"Admin"`를 입력하면 비밀번호를 물어보는 프롬프트 대화상자를 띄워주세요. 이때 아무런 입력도 하지 않거나 Esc를 누르면 "취소되었습니다."라는 메시지를 보여주세요. 틀린 비밀번호를 입력했다면 "인증에 실패하였습니다."라는 메시지를 보여주세요.

비밀번호 확인 절차는 다음과 같습니다.

- 맞는 비밀번호 "TheMaster"를 입력했다면 "환영합니다!"라는 메시지를 보여주세요.
- 틀린 비밀번호를 입력했다면 "인증에 실패하였습니다."라는 메시지를 보여주세요.
- 빈 문자열을 입력하거나 입력을 취소했다면 "취소되었습니다."라는 메시지를 보여주세요.

순서도는 다음과 같습니다.

![스크린샷 2024-02-20 오전 12 51 08](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/afc5a8b9-d3bc-41b6-b633-fade021b50dc)


중첩 `if` 블록을 사용하고, 코드 전체의 가독성을 고려해 답안을 작성하세요.

힌트: 프롬프트 창에 아무것도 입력하지 않으면 빈 문자열인 `''`가, ESC를 누르면 `null`이 반환됩니다.

```jsx
let userName = prompt("사용자 이름을 입력해주세요.", '');

if (userName == 'Admin') {

  let pass = prompt('비밀번호:', '');

  if (pass == 'TheMaster') {
    alert( '환영합니다!' );
  } else if (pass == '' || pass == null) {
    alert( '취소되었습니다.' );
  } else {
    alert( '인증에 실패하였습니다.' );
  }

} else if (userName == '' || userName == null) {
  alert( '취소되었습니다.' );
} else {
  alert( "인증되지 않은 사용자입니다." );
}
```
