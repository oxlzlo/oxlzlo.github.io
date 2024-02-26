---
title: 10. if와 ‘?’를 사용한 조건 처리
description: "if와 ‘?’를 사용한 조건 처리"
date: 2024-02-15
update: 2024-02-15
tags:
  - 패스트캠퍼스
  - 부트캠프
  - 프론트엔드 부트캠프
  - 국비지원교육
  - 내일배움카드
  - KDT
series: "study"
---


## if와 ‘?’를 사용한 조건 처리

### ‘if’문

- if(…)문은 괄호 안에 들어가는 조건이 참(true)일 경우 코드 블록이 실행된다.

```jsx
let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');

if (year == 2015) alert ('정답입니다!');
```

- 위의 예시는 조건(year == 2015)이 간단한 경우인데, 실제 조건문은 더 복잡할 수 있다.
    - if문을 쓸 때는 조건이 참일 경우 실행되는 구문이 단 한 줄이더라도 중괄호 ‘{ }’를 사용해 코드를 블록으로 감싸는 것을 추천
    - 코드 가독성 증가

```jsx
if (year == 2015) {
	alert ('정답입니다!');
	alert ('아주 똑똑하시네요!');
}
```

- 위처럼 중괄호를 사용해 코드를 블록으로 감싼다.

### 불린형으로 변환

- if(…)문은 괄호 안의 표현식을 평가하고 그 결과를 불린값(true, false)로 변환
- 형 변환 규칙에 따라 숫자 0, 빈 문자열 ‘ ’, null, undefined, NaN은 불린형으로 변환 시 모두 false가 된다.
- 이 외의 값은 불린형으로 변환 시 true가 된다.

위 규칙에 따르면 아래 코드 블록은 절대 실행되지 않는다.

```jsx
if (0) { // 0은 falsy
	...
}
```

아래 코드 블록은 항상 실행된다.

```jsx
if (1) { // 1은 truthy
	...
}
```

또는 아래와 같이 평가를 통해 확정된 불린값을 if문에 전달할 수 있다.

```jsx
let cond = (year == 2015); // 동등 비교를 통해 true/false 여부를 결정한다.

if (cond) { // true일 경우 실행
	...
}
```

### ‘else’절

- if문엔 else절을 붙일 수 있으며, else 뒤에 이어지는 코드 블록은 조건이 거짓일 때 실행된다.

```jsx
let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');

if (year == 2015) {
	alert ('정답입니다!');
} else {
	alert ('오답입니다'); // 2015 이외의 값을 입력했을 경우 
}
```

### ‘else if’로 복수 조건 처리하기

- 조건 여러 개를 처리해야 할 때 else if를 사용한다.

```jsx
let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');

if (year < 2015) {
	alert ('숫자를 좀 더 올려보세요.');
} else if (year > 2015) {
	alert ('숫자를 좀 더 내려보세요.');
} else {
	alert ('정답입니다!');
}
```

1. 위 예시에서, 자바스크립트는 조건 ‘year < 2015’ 를 먼저 확인한다.
2. 만약 이 조건이 거짓이라면, 다음 조건 ‘year > 2015’를 확인한다.
3. 이 조건 또한 거짓이라면 else절 내의 alert를 실행한다.

- else if 블록을 더 많이 붙이는 것도 가능하며, 마지막에 붙는 else는 필수가 아닌 선택 사항이다.

### 조건부 연산자 ‘?’

```jsx
let accessAllowed;
let age = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');

if (age > 18) {
	accessAllowed = true;
} else {
	accessAllowed = false;
}

alert (accesseAllowed);
```

- ‘물음표(question mark) 연산자’ 라고도 불리는 ‘조건부(conditional) 연산자’를 사용하면 위의 예시를 더 짧고 간결하게 변형할 수 있다.
- 조건부 연산자는 물음표 ‘?’로 표시한다.
- 자바스크립트에서 피연산자를 3개나 받는 연산자는 조건부 연산자가 유일하다.

```jsx
let result = condition ? value1 : value2;
```

평가 대상인 condition이 true라면 value1이 반환되고, false라면 value2가 반환된다.

```jsx
let accessAllowed = (age > 18) ? true : false;

// 연산자 우선순위 규칙에 따라, 비교 연산 'age > 18'이 먼저 실행된다.
// 조건문을 괄호로 감쌀 필요가 없다. 따라서 위의 코드는 아래와 같다.
let accessAllowed = age > 18 ? true : false;
```

괄호가 있으나 없으나 차이는 없지만, 코드의 가독성 향상을 위해 괄호를 사용할 것을 권유한다.

**⚠️주의 : 비교 연산자 자체가 true 혹은 false를 반환하기 때문에 위의 예시에서 물음표 연산자를 사용하지 않아도 된다.**

```jsx
// 동일하게 동작함
let accessAllowed = age > 18;
```

### 다중 ‘?’

- 물음표 연산자 ?를 여러 개 연결하면 복수의 조건을 처리할 수 있다.

```jsx
let age = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');

let message = (age < 3) ? '아기야 안녕?' :
	(age < 18) ? '안녕!' :
	(age < 100) ? '환영합니다!' :
  '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';

alert( message );
```

1. 첫 번째 물음표에서 조건문 age < 3을 검사
2. 결과가 참이면 '아기야 안녕?' 반환, 거짓이면 첫번째 콜론 ‘:’에 이어지는 조건문 age < 18 검사
3. 그 결과가 참이면 '안녕!' 반환, 거짓이면 다음 콜론에 이어지는 조건문 age < 100 검사
4. 그 결과가 참이면 '환영합니다!' 반환, 거짓이면 마지막 콜론 이후의 표현식인 '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!' 반환

if..else를 사용하면 위 예시를 아래와 같이 변형할 수 있다.

```jsx
if (age < 3) {
  message = '아기야 안녕?';
} else if (age < 18) {
  message = '안녕!';
} else if (age < 100) {
  message = '환영합니다!';
} else {
  message = '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';
}
```

### 부적절한 ‘?’

```jsx
let company = prompt('자바스크립트는 어떤 회사가 만들었을까요?', '');

(company == 'Netscape') ?
   alert('정답입니다!') : alert('오답입니다!');
```

위의 예시처럼 물음표 ? 를 if 대용으로 쓰는 경우가 종종 있다.

조건 compay == ‘Netscape’의 검사 결과에 따라 ? 뒤에 이어지는 첫 번째 혹은 두 번째 표현식이 실행되어 alert 창이 뜨게 된다.

위 예시에선 평과 결과를 변수에 할당하지 않고, 결과에 따라 실행되는 표현식이 달라지도록 했다.

그런데 이런 식으로 물음표 연산자를 사용하는 것은 좋지 않다.

물음표 ? 를 if문을 대용으로 사용하는 게 코드 길이가 짧아진다는 점에서 개발자 입장에선 매력적일 수 있지만, 이렇게 코드를 작성할 경우 가독성이 떨어진다.

```jsx
let company = prompt('자바스크립트는 어떤 회사가 만들었을까요?', '');

if (company == 'Netscape') {
  alert('정답입니다!');
} else {
  alert('오답입니다!');
}
```

위는 if를 사용해 변형한 코드다.

코드를 읽을 때 우리의 눈은 수직으로 움직이기 때문에, 수평으로 길게 늘어진 코드보단 여러 줄로 나뉘어 작성된 코드 블록이 더 읽기 쉽다.

물음표 연산자 ? 는 조건에 따라 반환 값을 달리하려는 목적으로 만들어 졌기 때문에, 여러 분기를 만들어 처리할 때에는 if문을 사용한다.

---

## 과제

### if와 문자열 0

아래 코드에서 alert는 실행될까요?

```jsx
if ("0") {
	alert ('Hello');
}
```

: 실행된다.

비어있는 문자열을 제외한 모든 문자열은 논리 평가 시 true를 반환하기 때문에 문자 “0”은 비어있지 않은 문자열이다.

### 자바스크립트의 공식 이름

if..else 구조를 이용해 “자바스크립트의 ‘공식’이름은 무엇일까요?” 라는 질문을 하는 코드를 작성해 보세요.

사용자가 'ECMAScript’를 입력했다면 ‘정답입니다!’, 아니라면 ‘모르셨나요? 정답은 ECMAScript입니다!’라는 메시지를 보여주세요.

![Untitled](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/2c9f3503-05a0-4968-b0b4-ca33a0db4624)


: 

```jsx
let answer = prompt ('자바스트립트의 공식 이름은 무엇일까요?', '');

if (answer == 'ECMAScript') {
	alert ('정답입니다!');
} else {
	alert ('모르셨나요? 정답은 ECMAScript입니다!');
}
```

위의 코드를 실행하면 아래 그림과 같은 결과가 나온다.

![2](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/706b3e78-4779-4f8a-932f-a7e2191f7867)


코드 출력

![3](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/ffbbe982-0b27-4875-94bb-466aa9db77df)


ECMAScript 입력

![4](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/fff0c717-3568-4162-8c1c-05f808ce098c)


123 입력

### 입력받은 숫자의 부호 표시하기

if..else와 프롬프트 대화상자를 사용해 사용자로부터 숫자 하나를 입력받고, 아래 조건에 따라 그 결과를 alert 창에 출력해 보세요.

- 입력받은 숫자가 0보다 큰 경우 1을 출력
- 입력받은 숫자가 0보다 작은 경우 -1을 출력
- 입력받은 숫자가 0인 경운 0을 출력

(사용자는 항상 숫자를 입력한다고 가정)

: 

```jsx
let userNumber = prompt('숫자를 입력해 주세요.', '');

if (userNumber > 0) {
	alert (1);
} else if (userNumber < 0) {
	alert (-1);
} else if (userNumber == 0) { // else if(조건)가 아닌 else를 사용해도 된다
	alert (0);
}
```

위의 코드를 실행하면 아래 그림과 같은 결과가 나온다.

![5](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/45e79204-0950-4bb8-b95c-ea54ebdc74fb)


코드 출력

![6](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/03447c41-1470-4ea1-8e39-5db6fd1464f2)


3 입력

![7](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/a0c5a442-f74c-4786-b697-4f520472035b)


-3 입력

![8](https://github.com/oxlzlo/oxlzlo.github.io/assets/140046183/90627b4d-cf90-4514-9843-60dc838b43f3)


0 입력

### ‘if’를 ‘?’로 교체하기

조건부 연산자 ‘?’를 이용해 if문이 사용된 아래 코드를 변형해보세요. 동작 결과는 동일해야 합니다.

```jsx
// 문제 코드
let result;

if (a + b < 4) {
	result = '미만';
} else {
	result = '이상';
}

// 정답 코드
let result = (a + b < 4) ? '미만' : '이상'
```

### ‘if..else’를 ‘?’로 교체하기

조건부 연산자 ‘?’를 사용해 if..else문이 사용된 아래 코드를 변형해보세요.

동작 결과는 동일해야 합니다.

가독성을 위해 표현식을 여러 줄로 분할해 작성해 보시길 바랍니다.

```jsx
// 문제 코드
let message;

if (login == '직원') {
  message = '안녕하세요.';
} else if (login == '임원') {
  message = '환영합니다.';
} else if (login == '') {
  message = '로그인이 필요합니다.';
} else {
  message = '';
}

// 정답 코드
let message = (login == '직원') ? '안녕하세요.' :
	(login == '임원') ? '환영합니다.' :
	(login == '') ? '로그인이 필요합니다.' :
	'';
```

---

### <소감>

if와 '?'를 사용한 조건 처리를 다시 공부하면서, 내가 코드를 작성할 때 간혹 부적절한 물음표 ‘?’ 연산자를 사용하고 있다는 사실을 알게 되었다.

나 또한 물음표 연산자가 코드의 길이가 줄어든다는 이유로 if..else문보다 선호했다.

하지만 이 때문에 코드의 가독성이 떨어진다는 것을 알게 되었고,

특히 코드를 읽을 때 우리의 눈이 수직으로 움직이기 때문에 수평으로 늘어진 코드보단 여러 줄로 나뉘어 작성된 코드 블록이 더 읽기 쉽다는 것을 알게 된 점이 인상적이다.
