# 서민석 [202030215]

## [05월 25일]

### 요청과 응답

* 요청 메세지 : 클라이언트가 서버로 보내는 편지
* 응답 메세지 : 서버가 클라이언트로 보내는 편지


###### 10-2

```
// 모듈을 추출
const express = require('express');

// 서버를 생성
const app = express();

// request 이벤트 리스너 설정
app.get('/page/:id', (request, response) => {
    // 토큰을 꺼냅니다.
    const id = request.params.id;

    // 응답합니다.
    response.send(`<h1>${id} Page</h1>`);
});

// 서버를 실행
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

## response 객체

메소드|설명
-|-
send()|데이터 본문을 제공합니다.
status()|상태 코드를 제공합니다.
set()|헤더를 설정합니다.

* send() 메소드 : 사용자에게 데이터 본문을 제공
* send() 메소드는 가장 마지막에 실행해야 하며, 두 번 실행할 수 없음

### Content-Type
* 서버가 Content-Type을 제공 : 웹 브라우저는 헤더를 확인, 제공된 데이터의 형태를 확인(MIME라는 문자열로 제공)

###### MIME 형식
MIME 형식|설명
-|-
text/plain|기본적인 텍스트를 의미합니다.
text/html|html 데이터를 의미합니다.
image/png|png 데이터를 의미합니다.
audio/png|png 데이터를 의미합니다.
video/mpeg|MPEG 비디오
application/json|json 데이터를 의미합니다.
multipart/form-data|입력 양식 데이터를 의미합니다.

* MIME 형식을 지정:type() 메소드 사용
###### Content-Type 지정 메소드

메소드|설명
-|-
type()|Content-Type을 MIME 형식으로 지정합니다.

<hr>


### HTTP 상태 코드 : 404 Not Found
* 상태 코드 : 서버가 클라이언트에 '해당 경로는 이러한 상태'라고 알려 주는 용도

###### HTTP 상태 코드의 예

HTTP 상태 코드|설명|예
-|-|-
1XX|처리 중|100 Continue
2XX|성공|200 OK
3XX|리다이렉트|300 Multiple Choices
4XX|클라이언트 오류|400 Bad Request
5XX|서버 오류|500 internal Server Error

* 상태 코드를 지정 : status () 메소드 사용

###### status()메소드
메소드|설명
-|-
status()|상태 코드를 지정합니다.

###### 상태코드
```
// 모듈을 추출합니다.
const express = require('express');

// 서버를 생성합니다.
const app = express();

// request 이벤트 리스너를 설정합니다.
app.get('*', (request, response) => {
    response.status(404);
    response.send('해당 경로에는 아무것도 없습니다.');
});

// 서버를 실행합니다.
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

### 리다이렉트 : 3XX, 특수한 상태 코드
* 웹 브라우저가 리다이렉트를 확인하면 화면을 출력하지 않고, 응답 헤더에 있는 Location 속성을 확인해서 해당 위치로 이동
* 특정 경로로 웹 브라우저를 인도 할 때 사용

```
// 모듈을 추출합니다
const express = require('express');

// 서버를 생성합니다.
const app = express();

// request 이벤트 리스너를 설정합니다.
app.get('*', (request, response) => {
    response.redirect('http://hanbit.co.kr');
});

// 서버를 실행합니다.
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

### request 객체
* 요청 매개 변수

##### ↓ https://search.naver.com/search.naver?where=nexearch&query=초콜릿&sm=top_hty&fbm=0&ie=utf8

분류|값|설명
-|-|-
프로토콜|HTTPS|통신에 사용되는 규칙을 의미합니다.
호스트|(search.)naver.com|애플리케이션 서버(또는 분산 장치 등)의 위치를 의미합니다.
URL|search.naver|애플리케이션 서버 내부에서 라우트 위치를 나타냅니다.
요청 매개 변수|?where=nexearch&query=초콜릿&sm=top_hty&fbm=0&ie=utf8|추가적인 정보를 의미합니다

```
// 모듈을 추출합니다.
const express = require('express');

// 서버를 생성합니다.
const app = express();

// request 이벤트 리스너를 설정합니다.
app.get('*', (request, response) => {
    console.log(request.query);
    response.send(request.query);
});

// 서버를 실행합니다.
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

### 미들웨어

메소드|설명
-|-
use()|미들웨어를 설정합니다.

* #### 정적 파일 제공
###### 웹 페이지에서 변경되지 않는 요소(이미지,음악,자바스크립트 파일,스타일시트 파일 등)를 쉽게 제공

```
// 모듈을 추출합니다.
const express = require('express');

// 서버를 생성합니다.
const app = express();
app.use(express.static('public'));

// request 이벤트 리스너를 설정합니다.
app.get('*', (request, response) => {
    response.send(404);
    response.send('해당 경로에는 아무것도 없습니다.');
});

// 서버를 실행합니다.
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

### morgan 미들웨어
* express 모듈의 미들웨어로 사용할 수 있는 외부 모듈을 확인

```
// 모듈을 추출합니다.
const express = require('express');
const morgan = require('morgan');

// 서버를 생성합니다.
const app = express();
app.use(express.static('public'));
app.use(morgan('combined'));

// request 이벤트 리스너를 설정합니다.
app.get('*', (request, response) => {
    response.send('명령 프롬프트를 확인해주세요.');
});

// 서버를 실행합니다.
app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```
<hr>

### body-parser 미들웨어
* 클라이언트 서버로 데이터 전송 

MIME 형식|설명
-|-
application/x-www-form-urlencoded|웹 브라우저에서 입력 양식을 POST, PUT, DELETE 방식 등으로 전달
application/json|JSON 데이터로 요청하는 방식입니다.
multipart/form-data|대용량 파일을 전송할 때 사용하는 요청 방식입니다.
```
// 모듈을 추출합니다.
const express = require('express');
const morgan = require('morgan');
const bodyParser = require('body-parser');

// 서버를 생성합니다.
const app = express();
app.use(express.static('public'));
app.use(morgan('combined'));
app.use(bodyParser.urlencoded({ extended: false}));

// request 이벤트 리스너를 설정합니다.
app.get('/', (request, response) => {
    // html 형식의 문자열을 생성합니다.
    let output = '';
    output += '<form method="post">';
    output += ' <input type="text" name="a" />';
    output += ' <input type="text" name="b" />';
    output += ' <input type="submit" />;
    output += '</form>';

    // 응답합니다.
    response.send(output);
});

app.post('/', (request, response) => {
    // 응답합니다.
    response.send(request.body);
});

// 서버를 실행합니다.
    app.listen(52273, () => {
    console.log('Server running at http://127.0.0.1:52273');
});
```

<hr>

속성 정리|클라이언트가 서버로 데이터를 전송하는 세 가지 방법
-|-
params 객체|URL의 토큰. 보기가 간편
query 객체|URL의 요청 매개 변수.토큰보다 많은 데이터를 전달할 수 있으며, 주소로 어떤 데이터가 오고 가는지 확인가능
body 객체|대용량 문자열 등을 전송할 때 사용. 주소에 데이터를 기록하지 못하므로 새로고침이나 즐겨찾기 기능 등을 활용할 수 없음


## [05월 18일]

### 전역변수
* 전역변수,전역 함수,전역 개체 : 모든 곳에서 사용할 수 있는 것들

###### 문자열 자료형의 전역 변수

변수|설명
-|-
__filename|현재 실행 중인 코드의 파일 경로를 나타냅니다.
__dirname|현재 실행 중인 코드의 폴더 경로를 나타냅니다.

<hr>

### process 객체의 속성과 이벤트

* Node.js는 process 전역 객체를 제공
* process 객체는 프로세스 정보를 제공하며, 제어할 수 있게 하는 객체

###### process 객체의 속성
속성|설명
-|-
env|컴퓨터 환경 정보를 나타냅니다.
version|Node.js 버전을 나타냅니다.
versions|Node.js와 종속된 프로그램 버전을 나타냅니다.
arch|프로세서의 아키텍처를 나타냅니다.
platform|플랫폼을 나타냅니다.

###### process 객체의 메소드
메소드|설명
-|-
exit([exitCode=0])|프로그램을 종료합니다.
memoryUsage()|메모리 사용 정보 객체를 리턴합니다.
uptime()|현재 프로그램이 실행된 시간을 리턴합니다.

<hr>

### os 모듈
* os 모듈 추출

```
// 모듈을 추출합니다.
const os = require('os');
```

###### os 모듈의 메소드
메소드|설명
-|-
hostname()|운영체제의 호스트 이름을 리턴합니다.
type()|운영체제의 이름을 리턴합니다.
platform()|운영체제의 플랫폼을 리턴합니다.
arch()|운영체제의 아키텍처를 리턴합니다.
release()|운영체제의 버전을 리턴합니다.
uptime()|운영체제가 실행된 시간을 리턴합니다.
totalmem()|시스템의 총 메모리를 리턴합니다.
freemem()|시스템의 사용 가능한 메모리를 리턴합니다.
cpus()|CPU의 정보를 담은 객체를 리턴합니다.
getNetworkInterfaces()|네트워크 인터페이스의 정보를 담은 배열을 리턴합니다.

<hr>

### url 모듈
* url 모듈 추출

```
// 모듈을 추출합니다.
const url = require('url');
```

###### url 모듈의 메소드
메소드|설명
-|-
parse(urlStr[.parseQueryString = false,slashesDenoteHost = false])|URL 문자열을 URL 객체로 변환해 리턴합니다.
format(urlObj)|URL 객체를 URL 문자열로 변환해 리턴합니다.
resolve(from,to)|매개 변수를 조합하여 완전한 URL 문자열을 생성해 리턴합니다.

<hr>

### File System 모듈

* fr.readFileSync() 메소드를 사용해 동기적으로 파일을 읽음
```
// 모듈을 추출합니다.
const fs = require('fs');
// 파일을 읽어들이고 출력합니다.
const file = fs.readFileSync('textfile.txt');
console.log(file);
console.log(file.toString());
```
* fs.readFile() 메소드를 사용해 비동기적으로 파일을 읽음
```
// 모듈을 추출합니다.
const fs = require('fs');
// 파일을 읽어들입니다.
fs.readFile('textfile.txt', (error, file) => {
    // 출력합니다.
    console.log(file);
    console.log(file.toString());
});
```
* 동기와 비동기의 실행 결과는 같지만 내부 실행 구조는 다름

<hr>

### 비동기 처리의 장점
* 웹 서버를 C++ 프로그래밍 언어로 만들면 무척 빠르지만, 개발과 유지 보수는 어려움
* 전 세계 웹 서비스 기업(페이스북, 트위터 등)도 C++로 웹 서버를 개발하지 않고 PHP, 자바, 루비, 파이썬, Node.js 등 프로그래밍 언어로 개발
* 프로그래밍 언어 자체는 느리지만 큰 의미가 없다고 판단해 개발 속도와 유지 보수성이 좋은 프로그래밍 언어를 사용
* 자바스크립트 프로그래밍 언어는 C++, 자바보다 느리지만 Node.js를 사용하면 손쉽게 비동기 처리를 구현하여 빠른 처리가 가능

<hr>

###  노드 패키지 매니저
* npm을 이용한 외부 모듈 설치

```
> npm install <모듈 이름>
예> npm install express
```

<hr>

### request 모듈
* 웹 요청을 쉽게 만들어주는 모듈로 외부 모듈이다.

```
// 설치
> npm install request
```

###### request 모듈 추출

```
// 모듈을 추출합니다.
const request = require('request');
```

<hr>

### cheerio 모듈

* request 모듈로 가져온 웹 페이지는 단순한 HTML 문자열이다.

```
// cheerio 모듈 설치
> npm install cheerio
```

###### cheerio 모듈 추출

```
// 모듈을 추출합니다.
const cheerio = require('cheerio');
```

<hr>

### async 모듈

* 비동기 처리를 많이 하면 ‘콜백 지옥’이 발생 (콜백 지옥은
콜백 함수를 여러 개 들여쓰기 하여 코드를 보기 힘든 상태를 의미)

```
// async 모듈 설치
> npm install async
```

###### async 모듈 추출
```
// 모듈을 추출합니다.
const async = require('async');
```

## [05월 11일]
### Date 객체

###### 7-5
생성자 함수|설명
--|--
new Date()|현재 시간으로 Date 객체를 생성합니다.
new Date(유닉스 타임)|유닉스 타임(1970년 1월 1일 00시 00분 00초부터 경과한 밀리초)으로 Date 객체를 생성합니다.
new Date(<시간문자열>)|문자열로 Date 객체로 생성합니다.
new Date(<년>,<월-1>,<일>,<시간>,<분>,<초>,<밀리초>)|시간 요소(년,월-1,일,시간,분,초,밀리초)를 기반으로 Date 객체를 생성합니다.
* Month를 나타내는 '월'은 0부터 시작,
0 →1월, 11 → 12월

<hr>

* [예제 7-5] Date 객체 생성

###### code7-18

```
// 현재 시간을 기반으로 Date 객체를 생성합니다.
let dateA = new Date();
console.log(dateA);

// 유닉스 타임(1970년 1월 1일 00시 00분 00초부터 경과한 밀리초)
let dateB = new Date(692281800000);
console.log(dateC);

// 문자열을 기반으로 Date 객체를 생성합니다.
let dateC = new Date("December 9, 1991 21:30:00")
console.log(dateC);

// 시간 요소(년, 월 - 1, 일, 시간, 분, 초, 밀리초)를 기반으로 Date 객체를 생성합니다.
let dateD = new Date(1991, 12 - 1, 9, 21, 30, 0, 0);
console.log(dateD);
```

### *메소드 활용*

###### Date 객체
* getOO() 형태 메소드, setOO() 형태 메소드 : FullYear, Month, Day, Hours, Minutes, Seconds 등 사용

<hr>

###### [예제 7-6] 시간 더하기
* 현재 시간에 1년, 11월, 7일을 더해 출력. (현재 시간:2016년 8월 16일)

###### code 7-19

```
// 현재 시간을 구합니다.
let date = new Date();

// 출력1
console.log(date);

// 시간을 더합니다.
date.setFullYear(date.FullYear() + 1);
date.setMonth(date.getMonth() + 11);
date.setDate(date.getDate() + 3);

// 출력2
console.log(date);
```

<hr>

### *Array 객체*

#### Array 객체의 기본 메소드

* 대부분 파괴적 메소드로 자기 자신을 변경

###### 표 7-6
메소드|설명
-|-
concat()|매개 변수로 입력한 배열의 요소를 모두 합쳐 배열을 만들어 리턴합니다.
join()|배열 안의 모든 요소를 문자열로 만들어 리턴합니다.
pop()*|배열의 마지막 요소를 제거하고 리턴합니다.
push()*|배열의 마지막 부분에 새로운 요소를 추가합니다.
reverse()*|배열의 요소 순서를 뒤집습니다.
slice()|배열 요소의 지정한 부분을 리턴합니다.
sort*|배열의 요소를 정렬합니다.
splice()*|배열 요소의 지정한 부분을  삭제하고 삭제한 요소를 리턴합니다.
* 표시된메소드는 자기 자신을 변화시킵니다.

<hr>

* [예제 7-8] 배열 가공

###### code 7-21

```
// 배열을 선언합니다.
let array = [{
    name: '고구마',
    price: 1000
}, {
    name: '감자',
    price: 500
}, {
    name: '바나나'
    price: 1500
}];
// 배열의 요소를 꺼냅니다.
let popped = array.pop();
console.log('- 배열에서 꺼낸 요소');
console.log(popped);
console.log('- pop() 메소드를 호출한 이후의 배열');
console.log(array);

// 배열에 요소를 넣습니다.
array.push(popped);
array.push({
    name: '사과',
    price: 2000
});
console.log('- push() 메소드를 호출한 이후의 배열');
console.log(array);
```

<hr>

### *ECMAScript5에서 추가된 메소드*

* 모질라 레퍼런스 - Array

###### 표 7-7
메소드|설명
-|-
forEach()|배열의 요소를 하나씩 뽑아 반복을 돌립니다.
map()|콜백 함수에서 리턴하는 것을 기반으로 새로운 배열을 만듭니다.
filter()|콜백 함수에서 true를 리턴하는 것으로만 새로운 배열을 만들어 리턴합니다.

* 콜백 함수를 매개 변수로 받음

<hr>

* [예제 7-10] ECMAScript5에서 추가된 Array 객체의 메소드

###### code 7-24

```
// 배열을 선언합니다.
let array = [52, 273, 32, 64, 72];

// forEach() 메소드
console.log('--- for Each() 메소드 ---');
array.forEach((item, index) => {
    console.log(`-${index}번째 요소는 ${item}입니다.`);
});

// map() 메소드
console.log();
console.log('--- map() 메소드 ---');
let outputA = array.map((item, index) => {
    // 배열의 모든 요소를 제곱해서 새로운 배열을 만듭니다.
    return item * item;
});
console.log(outputA);

// filter() 메소드
console.log();
console.log('--- filter() 메소드 ---');
let outputB = array.filter((item, index) => {
    // 짝수만 추출합니다.
    return item % 2 == 0;
});
console.log(outputB);
```

### *프로토타입에 메소드추가*
* 프로토타입에 메소드를 추가하면 해당 자료형 전체에 추가 가능
* String 생성자 함수의 prototype 속성에 contain ()메소드를 추가

```
// 프로토타입에 메소드를 추가합니다.
String.prototype.contain = function (input) {
    return this.index0f(input) >= -1;
    };

    // 메소드를 활용합니다.
    console.log('안녕하세요',contain('안녕'));
    console.log('안녕하세요',contain('데굴데굴'));
}
```

<hr>



## [05월 04일]
### *프로토타입*
* 생성자 함수로 만든 객체는 프로토타입 공간에 메소드를 지정해서 <br>모든 객체가 공유 하도록 함, 해당 함수를 생성자 함수로 사용했을 때만 의미가 있음

###### code 6-15 프로토타입을 사용한 메소드 생성
```
// 생성자 함수
function Product(name, price) {
    this.name = name;
    this.price = price;
}

// 프로토타입에 메소드를 선언합니다.
Product.prototype.print = function () {
    console.log(`${this.name}의 가격은 ${this.price}원입니다.`);
};

// 객체를 생성합니다.
let product = new Product("바나나", 1200);

// 메소드를 호출합니다.
product.print();
```

* 객체 지향적으로 구성한 객체 배열

```
// 생성자 함수
function  Product(name, price) {
    this.name = name;
    this.price = price;
}
// 프로토타입에 메소드를 선언합니다.
Product.prototype.print = function () {
    console.log(`${this.name}의 가격은 $(this.price)원입니다.`);
};

// 상품 목록을 선언합니다.
let products = {
    new Product(`바나나`, 1200),
    new Product(`사과`, 2000),
    new Product(`배`, 3000),
    new Product(`고구마`, 700),
    new Product(`감자`, 600),
    new Product(`수박`, 5000)
};

// 반복해서 출력합니다.
for (let product of products) {
    product.print();
}
```
<hr>

### null의 값과 자료형
###### code 6-17 null의 값과 자료형
```
console.log(null);
console.log(typeof(null));
```

### 기본 자료형과 객체 자료형의 차이

* 객체 숫자, 문자열, 불

```
// 객체 자료형
let number = new Number(273);
let string = new String('안녕하세요');
let boolean = new Boolean(true);

// 자료형을 출력합니다
console.log(typeof number);
console.log(typeof string);
console.log(typeof boolean);
```

* 기본 자료형의 속성 또는 메소드를 사용할 때 기본 자료형이 자동으로<br>객체로 변환이 됨. 즉, 기본 자료형과 객체 자료형 모두 속성과 메소드를 사용함

* 차이점 : 기본 자료형은 객체가 아니므로 속성과 메소드를 추가할 수 없음

<hr>

* 기본 자료형에 프로토타입으로 메소드 추가

###### code 7-5 프로토타입에 메소드 추가

```
// 변수를 생성합니다.
let primitiveNumber = 273;

// 메소드를 추가합니다.
Number.prototype.method = function () {
    return 'Primitive Method';
};

// 메소드를 실행합니다.
console.log(primitiveNumber.method());
```

<hr>

### Number 객체

* [예제 7-1] Number 객체의 메소드
* Number 객체 생성

###### code 7-6

```
let numberFromLiteral = 273;
let numberFromConstructor = new Number(273);
```

#### 메소드

###### 표 7-1

메소드|설명
----|----
toExponential()|숫자를 지수 표시로 나타낸 문자열을 리턴합니다.
toFixed()|숫자를 고정소수점 표시로 나타낸 문자열을 리턴합니다.
toPrecision()|숫자를 길이에 따라 지수 표시 또는 고정소수점 표시로 나타낸 문자열을 리턴합니다.

### 생성자 함수의 속성
* 생성자 함수에 속성과 메소드 추가

###### code 7-8

```
// 생성자 함수를 생성합니다
function Constructor() { }
Constructor.property = 273;
Constructor.method = function () { };

// 생성자 함수의 속성과 메소드를 출력합니다.
console.log(Constructor.property);
console.log(Constructor.method);
```

###### 표7-2

속성|설명
-|-
MAX_VALUE|자바스크립트의 숫자가 나타낼 수 있는 최대 숫자
MIN_VALUE|자바스크립트의 숫자가 나타낼 수 있는 최소 숫자
NaN|자바스크립트의 숫자로 나타낼 수 없는 숫자
POSITIVE_INFINITY|양의 무한대 숫자
NEGATIVE_INFINITY|음의 무한대 숫자





## [04월 27일]
### *타이머 함수*
* '특정 시간 후에' 또는 '특정 시간마다' 어떤 일을 할 때 사용
* 시간을 밀리초로 지정. 1초를 나타내려면 1000(밀리초)을 입력



함수|설명 
---|---
setTimeout(함수, 시간)| 특정 시간 후에 함수를 실행합니다.
setinterval(함수, 시간)|특정 시간마다 함수를 실행합니다.
```
ex)
// 1초 후에
setTimeout(function() {
    console.log("1초가 지났습니다.");
}, 1000); 

// 1초마다
setInterval(function() {
    console.log("1초마다 호출됩니다.");
}, 1000);
```
* 종료 : Ctrl + C
* 실행화면에서 ^C는 Ctrl + C를 눌렀다는 의미임
<hr/>

### 타이머 제거 함수
함수|설명
---|---
clearinterval(아이디)|특정 시간마다 실행하던 함수 호출을 정지합니다.
```
code 5-17 clearinterval()함수 예시
// 1초마다
let id = setInterval(function() {
    console.log("출력합니다.");
}, 1000);
// 3초후에
setTimeout(function() {
    // 타이머를 제거합니다.
    clearinterval(id);
}, 3000);
```
<hr/>

### 객체
* 배열
```
code 6-1 배열
// 배열을 선언합니다.
let array = ['사과', '바나나', '망고', '딸기'];
```
* 배열 접근
```
array[0] -> '사과'
array[1] -> '망고'
```
###### 표 6-1 배열
인덱스|요소
---|---
0|사과
1|바나나
2|망고
3|딸기
* 배열은 요소에 접근할 때 인덱스를 사용하고, 객체는 키를 사용함
<hr/>

###### code 6-2 객체 선언
```
// 객체를 선언합니다.
let product = {
    제품명: '7D 건조 망고',
    유형: '당절임'
    성분: '망고, 설탕, 메타중아황산나트륨, 치자황색소',
    원산지: '필리핀'
};

// 출력합니다.
console.log(product);
```
###### 표 6-2 객체
키|속성
---|---
제품명|7D 건조 망고
유형|당절임
성분|망고, 설탕, 메타중아황산나트륨, 치자황색소
원산지|필리핀
<hr/>


* 요소 : 배열 내부에 있는 값 하나하나
* 속성 : 객체 내부에 있는 값 하나하나
* 메소드 : 객체의 속성 중 자료형이 함수인 속성


## [04월 13일]
### 익명 함수
* 이름이 없는 함수
* 함수를 호출하면 함수 내부의 코드 덩어리가 모두 실행
```
// code5-1 익명 함수
let foo = function () {
    console.log("함수의 첫 번째 줄");
    console.log("함수의 두 번째 줄");
};

foo();
console.log(foo);
/// 함수의 첫번째 줄
    함수의 두번째 줄
    [function: foo]
```

### 선언적 함수
* 이름이 있는 함수
```
// code5-2 선언적 함수
function foo () {
    console.log("함수의 첫 번째 줄");
    console.log("함수의 두 번째 줄");
};

foo();
console.log(foo);

/// 함수의 첫번째 줄
    함수의 두번째 줄
    [function: foo]
```

### 화살표 함수[ECMAScript6]
* '하나의 표현식을 리턴하는 함수’를 만들 때는 중괄호 생략 가능

```
let foo = () => {
    console.log("함수의 첫 번째 줄");
    console.log("함수의 두 번째 줄");
};

foo();
console.log(foo);
/// 함수의 첫번째 줄
    함수의 두번째 줄
    [function: foo]
```

### github clone
$ github clone ("주소")

### 리턴 없는 함수
```
/// 5-6 리턴 없는 함수
function print(message) {
    console.log(`"${message}"라고 말했습니다`);
}

print("안녕하세요");
print("안녕히계세요");
```

### 함수 매개 변수 초기화

* 매개 변수를 입력하지 않고 함수 호출
``` 
ex)
function print(name, count) {
    if (!count) {
        count = 1;
    }
    console.log(`${name}이/가 ${count}개 있습니다.`);
}
print("사과", 10);
print("사과");
/// "사과"이/가 "10"개 있습니다.
    "사과"이/가 "undefined"개 있습니다.
```

### 조건문을 활용한 매개 변수 초기화
* 조건문으로 매개 변수를 확인, count가 undefined일 때 1로 초기화

``` 5-11
ex)
function print(무명, 1) {
    if (!count) {
        count = 1;
    }
    console.log(`${name}이/가 ${count}개 있습니다.`);
}

print("사과", 10);
print("사과");
print();
/// "
    "사과"이/가 "10"개 있습니다.
    "사과"이/가 "1"개 있습니다.
    "무명"이/가 "1"개 있습니다.
```

### 콜백 함수

* 함수의 매개 변수로 전달되는 함수

```
function tentimes(foo) {
    for (let i = 0; i < 10; i++) {
        foo();
    }
}
tentimes 

```
### 표준 내장 함수
```
ex)5-15
let inputA = "52";
let inputB = "52.273";
let inputC = "1401동"

console.log(parseInt(inputA));

console.log(parseInt(inputB));
console.log(parseFloat(inputC));

console.log(parseInt(inputC));


// 52
   52
   52.273
   1401
```

### 타이머 함수
* '특정 시간 후에' 또는 '특정 시간마다' 어떤 일을 할 때 사용
* 시간은 밀리초로 지정. 1초를 나타내려면 1000(밀리초)을 입력

## [04월 06일]
### 역 for 반복문

* for in 반복문(index값을 가져옴)
```
for (let 인덱스 in 배열) { 

}
```
* for of 반복문(요소값을 가져옴)
```
for (let 요소 of 배열) {

}
```

### 중첩 반복문
* 별 피라미드 예시
```
let output = "";

for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10 - i; j++){
        output += '*';
    }
    output += `\n`;
}

console.log(output);
```
### break 키워드
* 반복문에서 벗어날때 사용(switch문에서 많이 사용)
```
let i = 0;
let array = [1, 31, 273, 57, 8, 11, 32];
let output;

while (true) {
    if (array[i] % 2 == 0) {
        output = array[i];
        break;
    }

    i = i + 1;
}

console.log('처음 발견한 짝수는 ${output}입니다.')
```

### push
* 배열의 끝에 원하는 값을 추가해주는 함수.
```
bar = [0];
console.log("\n push");
foo.push("자료구조",1, 0.5);
bar.push(1, 2, 3);
console.log(foo);
```
### pop
* 배열의 마지막 주소에 있는 값을 제거해주는 함수.
```
console.log("\n pop");
foo.pop();
console.log(foo);
```
### shift
* 배열의 첫번째 주소에 있는 값을 제거한 후에 반환해주는 함수.

### continue 키워드
* 반복문 내부에서 현재 반복을 멈추고 다음 반복을 진행

```
for (let i = 1; i < 10; i++){
    if (i % 2 == 0) {
        continue;
    }

    console.log(i)
}
```
### Scope
* 변수를 사용할 수 있는 범위
* 스코프 == 블록

## [03월 30일]
### *중첩 조건문*
* 중첩 조건문이란, A->(B->C)나 (A->B)->C처럼 조건문의 전건이나 후건이 조건문인 조건문을 뜻합니다.
```javascript
if (불 표현식) {
    if (불 표현식) {
        문장;
    } else {
        문장;
    }
} else {
    if (불 표현식) {
        문장;
    } else {
        문장;
    }
}
```
###  *if else if*
```javascript
if (<불 표현식>) {
    // 불 표현식이 참일 때 실행할 문장
} else {
    // 불 표현식이 거짓일 때 실행할 문장
}
```


### *switch 조건문*
```javascript
switch (<비교할 값>) {
    case <값>:
        <문장>
        break;
    case <값>:
        break;
    default:
        <문장>
        break;
}
```
### *삼항 연산자*
```javascript
<불 표현식> ? <참> : <거짓>
```

```javascript
// 참과 거짓 위치에 불 자료형
console.log(number % 2 == 0 ? true : false);

// 참과 거짓 위치에 문자열 자료형
console.log(number % 2 == 0 ? "짝수" : "홀수");
```
### *짧은 초기화 조건문*
* || 연산자를 불이 아닌 자료에 사용할 경우
> A || B에서 A가 참이라면 A로 대치 <br>
> A || B에서 A가 거짓이라면 B로 대치

예시
```javascript
// 변수를 선언합니다.
let test;

// 짧은 초기화 조건문1
test = test  || "초기화합니다_1"
console.log(test);

// 짧은 초기화 조건문2
test = test  || "초기화합니다_2"
console.log(test);
```

## [03월 23일]

# 기본 자료형

### 피제수 
* 나누어지는 수(음수일때만 영향을 미침)

### 문자열
* ' 를 출력하고 싶다면 문자열을 " 로 잡아주면 된다.

### 이스케이프 문자 
* ' , " 를 문자 그대로 사용 가능
* 문자열 줄바꿈시 사용
* \t = 수평탭
* \n = 줄바꿈
* \' = 작은따옴표
* \" = 큰따옴표
* `\\` = 역슬래시

### 문자열 합하기
* "abc" + "def" = abcdef


### 문자열[숫자]
* 문자열에서 문을 출력하려면 문자열[1]이 아닌 문자열[0]을 입력해야한다.
* let a = "Hello World!"; - > a[4]; -> o

### 템플릿 문자열
* '안녕하세요'와 `안녕하세요`는 서로 다름
* 문자열과 숫자를 더하면 문자열이 되어버린다.
* '올해는' + new Date().getFullYear(); = '올해는 2021'

### 불(참 혹은 거짓)
* true(참)
* false(거짓)

<br>  23 < 250  (true)

### 비교 연산자
* `==` 같다
* `!=` 다르다
* `>` 왼쪽 피연산자가 크다
* `<` 오른쪽 피연산자가 크다
* `>=` 왼쪽 피연산자가 크거나 같다
* `<=` 오른쪽 피연산자가 크거나 같다

### 논리 연산자
* ! : 논리 부정 연산자
* || : 논리합 연산자
* && : 논리곱연산자

### 증감 연산자
* 변수++ 기존 변수 값에 1을 더합니다(후위).
* ++변수 기존 변수 값에 1을 더합니다(전위).
* 변수-- 기존 변수 값에서 1을 빼줍니다(후위).
* --변수 기존 변수 값에서 1을 빼줍니다(전위).

### 자료형 검사
* typeof : 해당 변수의 자료형을 추출합니다.(보통 연산자 뒤에 괄호를 붙임)

### 변수 선언
* let 식별자;

### 복합 대입 연산자
* += 숫자 덧셈 후 대입 연산자
* -= 숫자 뺄셈 후 대입 연산자
* *= 숫자 곱셈 후 대입 연산자
* /= 숫자 나눗셈 후 대입 연산자

### 자바 스크립트의 여섯 가지 자료형
```javascript
// 문자열
 typeof('String')
'string'
```
```javascript
 // 숫자
 typeof(273)
'number'
```
```javascript
> // 불
> typeof(true)
'boolean'
```
```javascript
> // 함수 
> typeof(function) () { })
'function'
 ```
 ```javascript
> // 객체
> typeof({})
'object'
```
```javascript
> // undefined 
> typeof(alpha)
'undefined'
```
### undefined 자료형
* 변수를 선언했으나 초기화하지 않은 자료형
```javascript
> let a 
undefined
```
### NaN(Not a Number)
* '숫자 자료형이지만 숫자가 아닌 것'을 의미
* NaN은 무조건적으로 다름
* NaN인지 확인할 때는 isNaN() 함수를 사용

### 일치 연산자
* === 자료형과 같은지 비교합니다
* !== 자료형과 값이 다른지 비교합니다.

## [03월 16일]

# 자바 스크립트

## 웹 클라이언트 APP 개발

* 웹 브라우저에서 실행되는 웹 클라이언트 애플리케이션 개발이 목적
* 웹 브라우저에서 실행할 수 있는 유일한 프로그래밍 언어


## 게임 개발
* 서버와 클라이언트 모두 C++로 제작(속도가 빠름)
* 한 번에 여러 스마트폰 운영체제에서 실행할 수 있는 <br>앱을 개발하는 것이 경제적으로 이득이 됨(스마트폰)

## Node.js
* 데이터 처리와 예외 처리가 복잡하나 빠름
* 웹 서버도 자바 스크립트로 개발 가능
* 초보자도 쉽게 프로그램을 만들 수 있음

> ### 식별자
> * 키워드 사용 금지
> * 특수 문자는 _와 $만 허용
> * 숫자로 시작 X
> * 공백 입력 X
> * 생성자 함수의 이름은 항상 대문자로 시작
> * 여러 단어로 된 식별자는 각 단어의 첫 글자를 대문자로 함
