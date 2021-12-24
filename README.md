# 코딩 표준안

- 참고 사이트

  [node.js](https://nodejs.org/ko/)

  [express](https://expressjs.com/ko/)

  [npm](https://www.npmjs.com/)

  [npm trends](https://www.npmtrends.com/)

  [js 표준안 참고 사이트 1](https://ui.toast.com/fe-guide/ko_CODING-CONVENTION)

  [js 표준안 참고 사이트 2](https://standardjs.com/rules-kokr.html)


## 들여쓰기, 띄어쓰기, 따옴표 등

- 문단 앞 여백은 space 2칸을 사용한다. (space와 tab을 섞어서 사용하지 않는다.)
- 한 줄에 하나의 문장만 허용하며, 문장 종료 시에는 반드시 세미콜론(;)을 사용한다.
- 한줄이 80자를 넘지 않도록 한다.

```js
router.get('/:id', async (req, res, next) => {
  try {
    const [list] = await Lefts.findAll({
      where: { id: req.params.id },
      include: [{ model: User }],
    });
    res.render('chat/view', { list });
  } catch (err) {
    next(createError(err));
  }
});
```

- 쉼표 뒤에 공백을 둔다.

```js
let arr = [a, b ,c ,d]; // O
let arr = [a,b,c,d]; // X
```
- 객체 내 : (콜론) 앞은 붙이고 뒤는 띄어쓴다.

```js
let obj = { // O
  name: 'choi',
  age: '30'
}

let obj2 = { // X
  name:'choi',
  age:'30'
}
```

- ( ), [ ] 안에 내용은 시작, 끝을 띄워쓰지 않는다.

```js
function sum(x, y) {} // O
const arr = [a, b] // O

function sum( x, y ) {} // X
const arr = [ a, b ] // X
```

- { } 안에 내용은 시작, 끝을 한 칸씩 띄워쓴다.

```js
const obj = { name: 'choi' } // O
const obj2 = {name: 'choi'} // X
```

- 문자열의 표현은 작은따옴표 (' ') 를 우선 사용한다.

```js
const name = 'choi in su' // O
const name2 = "choi in su" // X
```

- 변수 등을 조합해 문자열을 생성하는 경우 템플릿 문자열을 이용한다.
```js
function sayHi(name) {  // 변수 조합 시 '' 사용 X
  return 'How are you ' + name + '?';
}

function sayHi(name) {  // 변수 조합 시 `` 사용 O
  return `How are you ${name}?`;
}
```

- 예약어 뒤에는 공백을 추가한다.

```js
if (condition) { ... }   // O
if(condition) { ... }    // X
```

- 연산자 사이는 공백을 추가한다.

```js
let x = 2 // O
let x = 2 + 4 // O
let x=2 // X
let x=2+4 // X
```

## 명명 규칙

- 한 줄에 하나의 변수를 선언한다.

```js
let a; // O
let b;

let a, b; // X
```

- 변수와 함수명은 카멜표기법을 사용한다.

```js
const moveFile;
let moveFile;
function numTeamMembers() {}
```

- 동사를 앞에 명사를 뒤에 사용한다.

```js
const moveFile; // O
const fileMove; // X
```

- 상수는 const, 재 할당 필요가 있는 변수는 let을 사용한다. (var는 사용하지 않는다.)  
[var를 사용하지 않는 이유](https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- const를 let 보다 위에 선언한다.
- 전역 변수 사용을 지양한다.
- 사용하지 않는 변수나 함수는 정의하지 않는다.

## 모듈 사용 규칙

- 외부 모듈과 내부 모듈을 구분하여 사용한다.

```js
const express = require('express');
const app = express();
const path = require('path');
const passport = require('passport'); // 외부 모듈

const method = require('./middlewares/method-mw');
const locals = require('./middlewares/locals-mw');
const session = require('./middlewares/session-mw'); // 내부 모듈
```

- 불러올땐 require, 내보낼땐 module.exports 를 사용한다

```js
const mysql = require('mysql2/promise')
const pool = mysql.createPool({
	host: process.env.DB_HOST,
	port: process.env.DB_PORT,
})

module.exports = { mysql, pool }
```

## 배열

- 배열은 리터럴로 선언한다. (생성자는 사용하지 않는다.)

```js
const arr = [1, 2, 3, 4, 5]; // 리터럴 O

const arr = new Array(1, 2, 3, 4, 5); // 생성자 X
```

- 배열 복사시 펼침 연산자를 사용한다. (순환문을 사용하지 않는다.)

```js
let arr = [1, 2, 3]; // 펼침연산자 O
let newArr = [...arr];

let arr = [1, 2, 3]; // 순환문 X
let newArr = [];
for (let i = 0; i < arr.length; i++) {
  newArr[i] = arr[i];
}
```

- 원본 배열은 항상 유지하며 필요시 deepcopy하여 사용한다.

```js
const arr = [1, 2 ,3]
const arr2 = arr.slice()
```

## 객체

- 객체는 리터럴로 선언한다. (생성자는 사용하지 않는다.)

```js
let foo = { // 리터럴 O
  name: 'foo',
  age: 30,
  gender: 'male',
};

let foo = new Object(); // 생성자 X
foo.name = 'foo';
foo.age = 30;
foo.gender = 'male';
```

- 객체에 접근할때는 구조분해할당을 사용한다.

```js
const car = {
  name: 'sonata',
  color: 'white',
};

const { name, color } = car; // 구조분해할당
console.log(name); // sonata
console.log(color); // white
```

## 함수

- 함수 선언식과 함수 표현식을 사용한다.
- 함수 표현식은 화살표 함수를 사용한다.

```js
function workTogether() {} // 함수 선언식 O

const workTogether = () => {}; // 함수 표현식 O
```

- 함수 생성자를 사용하지 않는다.
```js
const workTogether = new Function(); // 함수 생성자 X
```

- 파라미터가 하나면 괄호는 생략 가능하다.
- 화살표 함수고 { } return 이 있으면 { }와 return은 생략 가능하다.
```js
let arr = [1, 2, 3];

let result = arr.filter((v) => {
  return v >= 2;
});

let result = arr.filter(v => v >= 2;);
```

## 블록
- 한 줄짜리 블록일 경우라도 { }를 생략하지 않으며 명확히 줄 바꿈 하여 사용한다.

```js
if (true) return true;  // { } 생략 X
else return false;

if (true) {  // O
  return true;
} else {
  return false;
}
```

## 조건
- 삼중 등호 연산자인 === , !== 만 사용한다. (이중은 사용하지 않는다.)
  
```js
const num = 123
const text = '123'

console.log(num == text) // X
console.log(num === text) // O

if (num === text) {
  ...
}
```


- else 문은 중괄호와 같은 줄에 둔다.

```js
if (true) { // O
  ...
} else {
  ...
}

if (true) { // X
  ...
}
else {
  ...
}
```

- 삼항 연산자를 사용할 경우 ? 와 : 는 각각의 행으로 처리한다.

```js
let name = true ? true : false // O

let name = true // O
  ? true
  : false

let name = true ? // X
  true :
  false
```

## 주석
- 간단한 단어나 문장은 한 줄 주석을 사용한다.
- 문장 끝에 주석을 작성할 경우 공백을 추가한다.
- 여러줄 주석 사용시 첫 줄과 마지막 줄에만 * 을 사용한다.

```js
const num; // 한 줄 주석 앞에 공백 추가

/* 최인수, 21년 12월 23일 수정 할 예정

여러 줄 주석시
첫 줄과 마지막 줄에만 * 표시
특이점이 있는 내용은 첫줄에 이름, 내용 표기

*/
```

## 비동기 처리
- 통신은 axios, 처리는 async, await 를 사용한다.
- async, await 사용시 try, catch 로 에러를 관리한다.

  [axios](https://www.npmjs.com/package/axios)
```js
const getUser = async (userId) => {
  try {
    let sql = `SELECT * FROM users WHERE userid=?`;
    const result = await pool.execute(sql, [userId]);
    if (result) {
      return { success: true, result };
    } else {
      return { success: false, result: null };
    }
  } catch (error) {
    throw new Error(error)
  }
};

axios.get('URL주소').then(onSuccess).catch(onError);
function onSuccess(result) {
  getUser(result.userId);
}
function onError(error) {
  console.log(error);
}
```