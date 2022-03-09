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
  <li>변수 선언과 함수 선언</li>
  <li>var와 let의 차이</li>
  <li>변수 호이스팅</li>
  <li>코드 평가와 실행</li>
</ol>
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
