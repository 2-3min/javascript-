# JS 문제 풀기
> 참고 사이트 : <https://github.com/lydiahallie/javascript-questions>

Thank you! lydiahallie😍

## 1번문제
```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}

sayHi();
```
* A: `Lydia` and `undefined`
* B: `Lydia` and `ReferenceError`
* C: `ReferenceError` and `21`
* D: `undefined` and `ReferenceError`

<details>
<summary>My Answer</summary>
<p>정답은 <code>D</code></p>
<ol>
  <li>함수 선언과 호출</li>
  <li>var와 let의 차이</li>
  <li>변수 호이스팅</li>
  <li>코드 평가와 실행</li>
</ol>
  <p>1. 전역에서 sayHi함수가 선언문으로 정의했다. "전역 코드 평가" 시 전역 객체 프로퍼티가 된다. 평가 후 "전역 코드 실행" 때 함수 호출을 실행한다.</p>
  <p>2. 함수 호출 실행 시 "전역 코드 실행"을 멈추고 "함수 코드 평가" 에 들어간다. <code>var name</code>와 <code>let age</code>이 <code>function Env.Record</code>에 등록이 되는데 <code>var</code>는 "선언단계"와 "초기화 단계"가 동시에 이루어져 "undefined"가 할당이 된다. let은 선언단계만 진행이 되므로 "uninitialized"이고, 초기화 단계는 "함수 코드 실행" 시 할당문('=')을 만났을 때 초기화가 이루어진다. </p>
  <p>3."함수 코드 실행" 단계에서 "console" 이라는 함수를 찾기 위해 <code>스코프 체이닝</code> 과정으로 "window" 전역 객체의 프로퍼티에 접근하여 console.log를 실행한다. 참조하는 변수의 name은 위에서처럼 "undefined", age는 "Reference Error" 가 발생한다. 선언 전에 밑에 있는 변수를 위에 끌어다 쓰는 것처럼 보여 이를 <code>변수 호이스팅</code>이라 한다.</p>
  <p> → let으로 선언한 변수의 경우 초기화 전 참조를 하여 이를 <code>TDZ(일시적 사각지대)</code>라고 한다.</p>
  <details>
    <summary>그림</summary>
    <img src="../img/problem1/answer1-1.PNG" width="800px" height="450px" alt="window"></img><br/>
    <img src="../img/problem1/answer1-2.PNG" width="800px" height="450px" alt="window"></img><br/>
    <img src="../img/problem1/answer1-3.PNG" width="800px" height="450px"alt="window"></img><br/>
    <img src="../img/problem1/answer1-4.PNG" width="800px" height="450px" alt="window"></img><br/>
    <img src="../img/problem1/answer1-5.PNG" width="800px" height="450px" alt="window"></img><br/>
  </details>
</details>

## 2번문제
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```
* A: `0 1 2` and `0 1 2`
* B: `0 1 2` and `3 3 3`
* C: `3 3 3` and `0 1 2`
<details>
  <summary>My Answer</summary>
  <p>정답은 <code>C</code></p>
  <ol>
    <li>블록레벨 스코프(for)</li>
    <li>var와 let,const의 차이</li>
    <li>렉시컬 환경, 스코프</li>
    <li>콜백함수</li>
    <li>클로저</li>
    <li>이벤트 루프 그리고 콜 스택과 테스트 큐</li>
  </ol>
  <p><code>(Javascript DeepDive p.387 참조)</code><strong>for문의 변수 선언문에 let 키워드를 사용한 for문은 코드블록이 반복해서 실행될때마다 코드블록을 위한 새로운 렉시컬 환경을 생성</strong>한다. 만약 for문의 코드 블록 내에서 정의된 함수가 있다면 이 함수의 상위스코프는 for문의 코드 블록이 생성한 렉시컬 환경이다.</p>
  <p>외부 렉시컬 환경 참조는 <strong>자신이 정의된 환경(상위 스코프)</strong>을 가리킨다.</p>
  <p>[[Enviroment]]도 <strong>자신이 정의된 환경(상위스코프)</strong>을 가리킨다.</p>
  <p><code>(Javascript DeepDive p.386 참조)</code><code>var</code>키워드로 선언한 변수는 오로지 함수의 코드 블록만 지역 스코프로 인정(이걸 함수레벨 블록이라 한다), <code>let</code>, <code>const</code>는 모든 코드 블록을 지역스코프로 인정한다.(블록레벨스코프)</p>
  <p>setTimeout 함수의 렉시컬 환경은 <code>익명함수(anonymous function)</code>의 [[Enviroment]] 내부 슬롯에 의해 참조되고 있어 가비지 컬렉터가 해제하지 않는다. 외부함수(setTimeout)보다 중첩함수(anonymous function)이 더 오래 유지 되었으며, 외부 함수의 변수를 참조할 수 있다. 이러한 중첩 함수를 클로저(closure)라 한다.</p>
  <p>콜백함수는 매개변수로 넘겨지는 함수를 콜백함수라고하고, 매겨변수를 받는 함수를 고차함수라 한다.</p>
  <p>setTimeout, setInterval 같은 함수들은 호출한 후 delay(ms) 후에 Task Queue에 들어가 대기한다. 그리고 실행컨텍스트 스택(콜 스택)이 비워졌을 때 선입선출방식으로 함수가 실행된다.</p>

  <details>
    <summary>그림</summary>
    <img src="../img/problem2/answer2-1.PNG" width="800px" height="450px" alt="window"></img><br/>
    <img src="../img/problem2/answer2-2.PNG" width="800px" height="450px" alt="window"></img><br/>
    <img src="../img/problem2/answer2-3.PNG" width="800px" height="450px"alt="window"></img><br/>
    <img src="../img/problem2/answer2-4.PNG" width="800px" height="450px" alt="window"></img><br/>
  </details>
</details>

## 3번문제
```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius
};

console.log(shape.diameter());
console.log(shape.perimeter());
```
* A: `20` and `62.83185307179586`
* B: `20` and `NaN`
* C: `20` and `63`
* D: `NaN` and `63`
<details>
<summary>My Answer</summary>
<p>정답은 <code>B</code></p>
<p></p>
<ol>
  <li>일반함수와 화살표함수의 this</li>
</ol>
<p>객체<code>메서드</code>의 <code>this</code>는 객체를 바인딩하고, 객체 프로퍼티에 할당된 <code>arrow function</code>의 <code>this</code>는 해당 코드에서의 상위 컨텍스트인 전역객체를 가리킨다.</p>
<code>
*자세한 내용은 6. this : 핵심 부분에서
</code>
</details>

## 6번문제
```javascript
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```
* A: `Hello`
* B: `Hey!`
* C: `undefined`
* D: `ReferenceError`
* E: `TypeError`

<details>
<summary>My Answer</summary>
<p>정답은 <code>A</code></p>
<ol>
  <li>참조에 의한 전달</li>
</ol>
<p>c의 참조 값(객체의 메모리 주소 값)을 복사하여 전달하기 때문에, 두개의 식별자(c, d)가 하나의 객체를 공유하여 값이 같다.</p>
<code>
*자세한 내용은 5. 원시타입과 객체(참조)타입에서
</code> 
</details>

## 8번문제
```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
console.log(freddie.colorChange('orange'));
```
* A: `orange`
* B: `purple`
* C: `green`
* D: `TypeError`

<details>
<summary>My Answer</summary>
<p>정답은 <code>D</code></p>
<ol>
  <li>생성자, 인스턴스</li>
  <li>static(정적) 메서드</li>
</ol>
<p>static(정적) 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드이다.</p>
<p>정적 메서드는 클래스로 호출한다.(인스턴스로는 호출할 수 없다.)</p>
<code>
*자세한 내용은 7. 클래스에서
</code> 
</details>

## 10번문제
```javascript
function bark() {
  console.log('Woof!');
}

bark.animal = 'dog';

```
* A: Nothing, this is totally fine!
* B: SyntaxError. You cannot add properties to a function this way.
* C: "Woof" gets logged.
* D: ReferenceError

<details>
<summary>My Answer</summary>
<p>정답은 <code>A</code></p>
<ol>
  <li></li>
</ol>
<p>원시 값(숫자, 문자열)을 제외한 Javascript의 거의 모든 것은 객체다. 코드평가 중 정의된 함수가 등록이 되면 함수객체가 만들어진다는 점에서 알 수 있다. 실제로 위 코드처럼 작성하지는 않겠지만, <code>함수객체.animal = 'dog'</code>이 실행되면 함수객체.animal에 dog가 할당된다.</p>
</details>

## 11번문제
```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Lydia', 'Hallie');
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```
* A: `TypeError`
* B: `SyntaxError`
* C: `Lydia Hallie`
* D: `undefined undefined`

<details>
<summary>My Answer</summary>
<p>정답은 <code>A</code></p>
<ol>
  <li></li>
</ol>
<p>생성자(new)를 통해 인스턴스(memeber)를 생성하였다. Person에 getFullName 메서드를 할당하는데, 인스턴스가 getFullName 함수를 호출하고 있다. Person 객체의 메서드이지, 인스턴스의 메서드가 아니다.</p>
<p>인스턴스가 <code>getFullName</code> 메서드를 호출하려면 <code>Person.prototype.getFullName</code>에 함수를 할당해야한다.(답: 'C' 출력)</p>
<p>답 'D' 가 나오는 경우는 <code>member.constructor.getFullName()</code>으로 호출했을 경우이다.</p>
</details>

## 12번문제
```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person('Lydia', 'Hallie');
const sarah = Person('Sarah', 'Smith');

console.log(lydia);
console.log(sarah); //undefined

//내가 추가한 코드
console.log(window.firstName); //Sarah
console.log(window.lastName); //Smith

```
* A: Person `{firstName: "Lydia", lastName: "Hallie"}` and `undefined`
* B: Person `{firstName: "Lydia", lastName: "Hallie"}` and Person `{firstName: "Sarah", lastName: "Smith"}`
* C: Person `{firstName: "Lydia", lastName: "Hallie"}` and `{}`
* D: Person `{firstName: "Lydia", lastName: "Hallie"}` and `ReferenceError`

<details>
<summary>My Answer</summary>
<p>정답은 <code>A</code></p>
<ol>
  <li>클래스</li>
  <li>this</li>
</ol>
<p>"lydia"는 new 생성자로 인해 this는 <code>인스턴스 "lydia"</code>를 가리킨다.
<p>"sarah"는 할당이 아니라 함수 호출이다. Person 함수는 return 값이 없으므로, "sarah"는 <code>undefined</code>이다.</p>
<p>Person의 "this"는 전역객체를 참조하므로, <code>window.firstName</code>과 <code>window.lastName</code>은 각각 <code>Sarah</code>, <code>Smith</code>를 출력한다.</p>
<code>
*자세한 내용은 7. 클래스에서
</code> 
</details>
