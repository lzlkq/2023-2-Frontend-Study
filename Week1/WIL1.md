# 1장~7장

**웹 브라우저에서의 콘솔**

| Enter | 프로그램 실행 |
| --- | --- |
| “” or ‘’  | 문자열 |
| Shift + Enter | 줄 바꿈 |
| ⬆️ or Ctrl + P | 코드 다시 불러오기 |
| Ctrl + L or clear( ) | 코드 삭제 |
| ⬆️ → Enter | ⬆️ 눌러 코드 다시 호출하고 오류 수정 후 Enter |

**HTML문서에 삽입하여 웹 브라우저로 실행**

순수 js : script 요소를 body  요소에 배치

HTML 요소, CSS 스타일 제어 : script 요소를 head 요소의 자식 요소로 배치

```jsx
+ “<br />” //줄 바꿈
<script scr="다른 파일의 경로"></script> //다른 js 파일에 작성하기
```

**Node.js로 파일을 읽어 들여 실행하기**

| cd | 디렉터리로 이동 |
| --- | --- |
| dir | 파일 목록 보기 |
| node 파일의 경로 | Node.js에서 파일을 읽어 들여 실행 |

js에서 변수 선언자는 **var** 하나!

변수 선언 끌어올림(hoisting) but 선언과 대입을 동시에 하는 코드는 제외(undefined)

**데이터 타입**

- 심벌

```jsx
var sym1 = Symbol() // 호출할 때마다 새로운 값 만듦
var sym1 = Symbol.for("club"); //Symbol.for() 문자열과 연결된 심벌
```

- 템플릿 리터럴

```jsx
var t = 'Man errs as long as
he strives.'
// var t = "Man errs as long as\nhe strives.";
```

플레이스 홀더 : ${…} → … 부분에 변수나 표현식의 결과값을 삽입할 수 있다.

```jsx
var a = 2. b = 3;
console.log('${a} + ${b} = ${a+b}'); // 2 + 3 = 5
```

### 객체

객체 생성 방법 → 객체 리터럴, 생성자 함수 사용

**객체 리터럴로 객체 생성**

```jsx
var card = { suit: "하트", rank: "A" };
var card = { "suit": "하트", "rank": "A"};

/* 프로퍼티 값을 읽거나 쓸 때는 마침표나 대괄호 연산자 사용 */
card.suit // 하트
card["rank"] // A

/* 프로퍼티 추가 삭제 */
var obj = {};
console.log(obj); // Object{} // 빈 객체 생성

card.value = 14; // 추가
console.log(card); // Object {suit: "하트" , rank: "A", value: "14"}

delete card.rank; // 삭제
console.log(card); // Object {suit: "하트" , value: "14"}
```

**in 연산자로 프로퍼티 있는지 확인**

```jsx
var card = { suit: "하트", rank: "A" };
console.log("suit" in card); // true
console.log("color" in card); // false
```

**생성자로 객체 생성**

첫글자 대문자로 

객체를 생성하고 초기화하는 역할

```jsx
function Card(suit, rank) {
	this.suit = suit;
	this.rank = rank;
}
var card = new Card("하트". "A"); // 생성자로 객체 생성 -> new 연산자
console.log(card); // Card { suit: "하트", rank: "A" }

```

**내장 객체**

- Date 생성자

```jsx
var now = new Date();
console.log(now);

var then = new Date(2008, 5, 10);
console.log(then);
```

- Function  생성자

```jsx
var square = new Function("x", "return x * x");
// var 변수 이름 = new Function(첫 번째 인수, ..., n 번째 인수, 함수 몸통);
```

### 함수

```jsx
function square(x) { return x * x; } // return 문 담에는 줄 바꿈 넣지X
square(3) // 9 -> 함수 호출

console.log(square(5)); // 25
function square(x) { return x * x; } // 함수 선언문의 호이스팅

/* 함수 안에서의 변수 선언 생략 */
function f() {
	a = "local";
	console.log(a); // local
	return a;
}
f();
console.log(a); // local
```

**let 선언자**

블록 유효 범위를 갖는 지역 변수 선언

```jsx
let x; // var문과 같다.

let x = "outer x"; {
	let x = "inner x";
	let y = "inner y";
	console.log(x); // inner x
	console.log(y); // inner y
}
console.log(x) // outer x
console.log(y) // y is not defined
```

**const 선언자**

블록 유효 범위를 가지면서 한 번만 할당 할 수 있는 변수(상수) 선언 → 반드시 초기화!

```jsx
const c = 2;
c = 5; // 오류

const origin = {x:1, y:2};
origin.x = 3;
console.log(origin); // Object {x:3, y:2} 
//const문으로 선언한 값은 수정 할 수 없지만 프로퍼티로 수정 가능
```

**함수 리터럴로 함수 정의하기**

함수 리터럴 → 익명 함수, 무명 함수

```jsx
var square = function(x) { return x * x; }; // 함수 리터럴로 정의 할 때는 끝에 세미콜론 
```

**객체의 메서드**

함수 객체의 참조를 값으로 담고 있는 프로퍼티

프로퍼티 값으로 함수 리터럴 대입

메서드가 속한 객체의 프로퍼티 값 상태를 바꾸는 용도로 사용

```jsx
var circle = {
	center: { x:1.0, y:2,0 },
	radius: 2.5,
	area: function() {
		return Math.PI * this.radius * this.radius; // this -> 그 함수를 메서드로 갖고 있는 객체
	}
};
circle.area() 

circle.translate = function(a, b) {
	this.center.x = this.center.x + a;
	this.center.y = this.center.y + b;
}; // 추가 -> translate 메서드
```

**메서드를 가진 객체를 생성하는 생성자**

```jsx
function Circle(center, radius) {
	this.center = center;
	this.radius = radius;
	this.area = function() {
		return Math.PI * this.radius * this.raidus;
	};
}
var p = {x:0, y:0};
var c = new Circle(p, 2.0);
console.log("넓이 = " + c.area());
```

### 배열

**배열 리터럴로 생성**

쉼표로 구분한 값을 대괄호로 묶어서 표현

```jsx
var evens = [2, 4, 6, 8]; // [...] -> 배열 리터럴
```

**length 프로퍼티**

배열 요소의 최대 인덱스 값 + 1

```jsx
var evens = [2, 4, 6, 8];
evens.length // 4
```

**Array 생성자로 생성**

```jsx
var evens = new Array(2, 4, 6, 8);

var x = new Array(3); // 이때 인수는 배열 길이
console.log(x.length); // 3

evens[2] // 6

var a = ["A", "B", "C", "D"];
console.log(a["2"]); // C

var a = ["A", "B", "C"];
a[3] = "D"; // a.push("D"); -> 배열 요소 추가
delete a[1]; // ["A", undefined, "C", "D"]

a[4] = "E";
console.log(a); // ["A", "B", "C", undefined, "E"]; -> 희소 배열 (length = 5)
```

희소배열의 길이는 배열 요소의 개수보다 크다!

### **대화상자**

- alert(경고 대화상자)

```jsx
alert("안녕하세요!");
```

- prompt(입력 대화상자)

```jsx
var name = prompt("이름을 입력하시오");
var age = parseInt(prompt("나이를 입력하시오"));
var height = parseFloat(prompt("키를 입력하시오")); // 숫자 값
```

- confirm(확인 대화상자)

```jsx
var ret = confirm("링크를 표시하시겠습니까?"); // 확인 -> true, 취소 -> false 반환
```

### **이벤트 처리기**

이벤트가 발생했을 때 실행되는 함수  

- HTML 요소의 속성에 이벤트 처리기 등록하기

HTML 코드와 JS 코드가 뒤섞이는 단점이 있음 → DOM에서 가져온 HTML 요소에 이벤트 처리기 지정 사용 or addEventListener 메서드 사용

- DOM에서 가져온 HTML 요소에 이벤트 처리기 지정하기
    - DOM : JS를 사용하여 HTML 문서 조작

이벤트 처리기 제거 → null 대입

### **타이머**

- 지정된 시간이 흐른 후에 함수 실행 : setTimeout
- 지정된 시간마다 반복해서 실행 : setInterval

### 제어구문

**조건문** : if/else 문, switch 문

**반복문** : while 문, do/while 문, for 문

for/in 문 : for (변수 in 객체 표현식) 문장

**점프문** : break 문, continue 

라벨문 : 라벨이름 : 문장