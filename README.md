# 서민석 [202030215]

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
