---
title: 15. 함수
description: 15. 함수
date: 2024-02-28
update: 2024-02-29
tags:
  - 패스트캠퍼스
  - 부트캠프
  - 프론트엔드 부트캠프
  - 국비지원교육
  - 내일배움카드
  - KDT
series: "study"
---


## 15. 함수

## 함수

### 함수 선언

- function 키워드, 함수 이름, 괄호로 둘러싼 매개변수를 차례로 써주면 함수를 선언할 수 있다.

```jsx
function name(parmeter1, parameter2, ... parameterN) {
// 함수 본문 
}

// 새롭게 정의한 함수 이름 옆에 괄호를 붙여 호출할 수 있다
function showMessage() {
	alert ('안녕하세요!');
}

showMessage(); // 함수 호출
```

- 함수의 주요 용도 중 하나는 ‘중복 코드 피하기’
    
    위의 예시에서 alert 창에 보여줄 메시지를 바꾸거나 메시지를 보여주는 방식 자체를 변경하고 싶다면,
    
    함수 본문 중 출력에 관여하는 코드만 수정하면 된다.
    

### 지역 변수

함수 내에서 선언한 변수인 지역 변수(local variable)는 함수 안에서만 접근할 수 있다.

```jsx
function showMessage() {
	let message = '안녕하세요!' // 지역 변수

	alert (message);
}

showMessage(); // 안녕하세요! 출력

alert (message); // ReferenceError: message is not defined
```

### 외부 변수 (= 전역변수)

함수 내부에서 함수 외부의 변수인 외부 변수(outer variable)에 접근할 수 있다.

```jsx
let userName = 'John';

function showMessage() {
	let message = 'Hello,' + userName;
	alert(message);
}

showMessage(); // Hello, John

---

let userName = 'John';

function showMessage() {
	userName = 'Bob'; // 외부 변수를 수정

	let message = 'Hello,' + userName;
	alert (message);
}

alert (userName); // 함수 호출 전이므로 John 출력

showMessage();

alert (userName); // 함수에 의해 Bob으로 값이 바뀜
```

위의 예시처럼 함수에서 외부 변수를 수정할 수도 있다.

- 외부 변수는 지역 변수가 없는 경우에만 사용할 수 있다.
    
    함수 내부에 외부 변수와 동일한 이름을 가진 변수가 선언되었다면, 내부 변수는 외부 변수를 가린다.
    
    ⇒ 동일한 이름의 변수를 선언하면 외부 변수는 내부 변수에 가려져 값이 수정되지 않는다.
    

```jsx
let userName = 'John';

function showMessage() {
	let userName = 'Bob'; // 같은 이름을 가진 지역 변수 선언

	let message = 'Hello,' + userName;
	alert (message);
}

showMessage(); // 함수는 내부 변수인 userName만 사용

alert (userName); // 기존 외부 변수의 바뀌지 않은 값 'John' 출력
```

### 매개변수

- 임의의 데이터를 함수 안에 전달할 수 있다

```jsx
function showMessage(from, next) { // 인자 : from, text 
	alert (from + ': ' + text);
}

showMessage ('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage( ('Aknn', "What's up?"); // Ann: Wha's up? (**)
```

위의 예시에서 함수 showMessage는 매개변수 from과 text를 가진다.

- 매개변수는 함수 선언 방식 괄호 사이에 있는 변수 (선언 시 쓰이는 용어)
- 인수는 함수를 호출할 때 매개변수에 전달되는 값 (호출 시 쓰이는 용어)

### 기본값

- 함수 호출 시 매개변수에 인수를 전달하지 않으면 그 값은 undefined가 된다.

```jsx
showMessage ('Ann'); // Ann: undefined
```

매개변수에서의 예시(showMessage(from, text))는 매개변수가 두지만, 위와 같이 인수를 하나만 넣어서 호출할 수 있다.

두 번째 매개변수에 값을 전달하지 않았기 때문에 text엔 undefined가 할당된다. 

- 매개변수에 값을 전달하지 않아도 그 값이 undefined가 되지 않게 하려면
    
    함수를 선언할 때 ‘=’를 사용해 ‘기본값 (default value)’를 설정해주면 된다.
    

```jsx
function showMessage (from, text = 'no text given') {
	alert (from + ': ' + text);
}

showMessage('Ann'); // Ann: no text given
showMessage('Ann', undefined); // Ann: no text given
```

- 함수 표현식도 기본값으로 설정할 수 있다.

```jsx
function showMessage (from, text = anotherFunction()) {
	// anotherFunction()은 text값이 없을 때만 호출
	// anotherFunction()의 반환 값이 text의 값이 된다
}
```

### 매개변수 기본값을 설정할 수 있는 또 다른 방법

- 함수를 선언할 때가 아닌 함수 선언 후에 매개변수 기본값을 설정하는 것이 적절한 경우도 있다.
    
    이런 경우엔 함수를 호출할 때 매개변수를 undefined와 비교하여 매개변수가 전달되었는지 확인
    

```jsx
function showMessage(text) {
	// ...
	if (text === undefined) { // 매개변수가 생략되었다면
		text = '빈 문자열';
	}

	alert (text);
}

showMessage(); // 빈 문자열
```

- if문을 쓰는 것 대신 논리 연산자 || 를 사용할 수도 있다.

```jsx
function showMessage(text) {
	text = text || '빈 문자열';
	...
}
```

- 외에도 nullish 병합 연산자 ?? 를 사용하면 falsy로 평가되는 값들을 일반 값처럼 처리 가능

```jsx
function showCount(count) {
	alert(count ?? 'unknown');
}

showCount(0); // 0
showCount(null); // unknown
showCount(); // unknown
```

### 반환 값

- 함수를 호출했을 때 호출한 곳에 특정 값을 반환하게 할 수 있다. ⇒ 반환 값(return value)

```jsx
function sum(a, b) {
	return a + b;
}

let result = sum(1, 2);
alert(result); // 3
```

실행 흐름이 return을 만나면 함수 실행은 즉시 중단되고 함수를 호출한 곳에 값을 반환

- 함수 하나애 여러 개의 return문이 올 수도 있다.

```jsx
function checkAge(age) {
	if (age >= 18) {
		return true;
	} else {
		return confirm('보호자의 동의를 받으셨나요?');
	}
}

let age = prompt('나이를 알려주세요', 18);

if (checkAge(age)) {
	alert('접속 허용');
} else {
	alert('접속 차단');
}
```

- return만 명시하는 것도 가능하다. 이런 경우 함수는 즉시 종료

```jsx
function showMovie(age) {
	if (!checkAge(age)) {
		return;
	}

	alert('영화 상영'); // 실행되지 않음
	// ...
}
```

ℹ️ return문이 없거나 return만 있는 함수는 undefined를 반환

```jsx
function doNothing() {}
alert( doNothing() === undefined ); // true

function doNothing() {
  return;
}
alert( doNothing() === undefined ); // true
```

⚠️ 자바스크립는 return문 끝에 세미콜론을 자동으로 넣기 때문에 return과 값 사이에 줄을 삽입하면 안 된다.

### 함수 이름짓기

- 코드를 읽는 사람이 함수 이름만 보고도 함수가 어떤 기능을 하는지 힌트를 얻을 수 있도록 간결하고 명확하게
- 함수가 어떤 동작을 하는지 축약해서 설명해 주는 동사를 접두어로 붙여쓴다.
- ex)
    - ‘get…’ :
    - ‘cacl…’
    - ‘create…’
    - ‘check…’

```jsx
showMessage(..)     // 메시지를 보여줌
getAge(..)          // 나이를 나타내는 값을 얻고 그 값을 반환
calcSum(..)         // 합계를 계산하고 그 결과를 반환
createForm(..)      // form을 생성하고 만들어진 form을 반환
checkPermission(..) // 승인 여부를 확인하고 true나 false를 반환
```

ℹ️ 함수는 동작 하나만 담당해야 한다.

### 함수 == 주석

함수가 길어지면 함수를 잘게 쪼갤 때가 되었다는 신호

- 함수를 간결하게 만들면 테스트와 디버깅이 쉬어진다
- 함수 그 자체로 주석의 역할까지 한다

```jsx
// <수정 전>
function showPrimes(n) {
  nextPrime: for (let i = 2; i < n; i++) {

    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }

    alert( i ); // 소수
  }
}

// <수정 후>
function showPrimes(n) {

  for (let i = 2; i < n; i++) {
    if (!isPrime(i)) continue;

    alert(i);  // a prime
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if ( n % i == 0) return false;
  }
  return true;
}
```

### 요약

함수 선언 방식으로 함수를 만들 수 있다.

```jsx
function 함수이름 (복수의, 매개변수는, 콤마로, 구분) {
	// 본문
}
```

- 함수에 전달된 매개변수는 복사된 후 함수의 지역변수가 된다.
- 함수는 외부 변수에 접근할 수 있지만, 함수 외부에서 함수 내부의 지역변수에 접근하는 건 불가능
- 함수는 값을 반환할 수 있고, 값을 반환하지 않는 경우는 반환 값이 undefined가 된다.
- 함수 이름은 함수가 어떤 동작을 하는지 설명할 수 있도록 간결하고 명확해야 한다.
- 함수는 동작을 수행하기 때문에 이름이 주로 동사이다.
