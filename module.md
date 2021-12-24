# 사용 예정 모듈

## [bcrypt](https://www.npmjs.com/package/bcrypt)
### 사용자 비밀번호 암호화 저장
- 비밀키(salt)를 따로 지정해 입력한 비밀번호와 조합하여 암호문으로 DB저장
- 단방향으로 암호 복호화는 불가능
- 로그인시 비밀번호 매치여부만 확인 가능

```js
let dbPassword = await bcrypt.hash(userPassword + salt, Number(round)) // 암호화
let compare = await bcrypt.compare(userPassword + salt, dbPassword) // 비밀번호 확인 (로그인)
```

## [dotenv](https://www.npmjs.com/package/dotenv)
### DB접속 정보 관리
- gitignore에 등록하여 배포시 외부 확인 불가능
- process.env 로 접근 가능

```js
PORT=3000
DB_USER=shop
DB_NAME=shop
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DIALECT=mysql
DB_TIMEZONE=+09:00
DB_PASS=dkfkek09**
```

