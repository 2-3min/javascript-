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
정답은 `D`
<ol>
  <li>함수 선언과 호출</li>
  <li>var와 let의 차이</li>
  <li>변수 호이스팅</li>
  <li>코드 평가와 실행</li>
</ol>
  <p>1. 전역에서 함수가 선언문으로 정의했다. 전역 코드 평가 시 전역 객체 프로퍼티가 된다. 평가 후 전역 코드 실행 때 함수 호출을 실행한다.</p>
  <p>2. 함수 호출 실행 시 전역 코드 실행을 멈추고 <strong>함수 코드 평가</strong>에 들어간다. <strong>var</strong>와 <strong>let</strong>이 <strong>function Env.Record</strong>에 등록이 되는데 <strong>var</strong>는 "선언단계"와 "초기화 단계"가 동시에 이루어져 "undefined"가 할당이 된다. let은 선언단계만 진행이 되므로 "<uninitialized>"이고, 초기화 단계는 함수 코드 실행 시 할당문('=')을 만났을 때 초기화가 이루어진다. </p>
  <p>3.함수 코드 실행 단계에서 "console" 이라는 함수를 찾기 위해 <strong>스코프 체이닝</strong> 과정으로 "window" 전역 객체의 프로퍼티에 접근하여 console.log를 실행한다. 여기서 name은 위에서처럼 "undefined", age는 "Reference Error" 가 발생한다. 이를 <strong>변수 호이스팅</strong>이라 한다.</p>
  <p> → let으로 선언한 변수의 경우 초기화 전 참조를 하여 이를 <strong>TDZ(일시적 사각지대)</strong>라고 한다.</p>
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
