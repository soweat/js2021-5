# 서민석 [202030215]

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
