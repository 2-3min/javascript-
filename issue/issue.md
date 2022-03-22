## ReferenceError: regeneratorRuntime is not defined 해결

`fifa online 4 전적 검색 사이트` 프로젝트에서 비동기 처리 방식인 `async`를 사용하려는데, `ReferenceError: regeneratorRuntime is not defined` 에러가 발생했다.

[parcel 공식 페이지(한국어)](https://ko.parceljs.org/assets.html)에서 `Parcel은 CommonJS 와 ES6 모듈 구문을 모두 지원합니다.`....ㅎ..
`async`, `await`은 ES2017(ES8)에 나온 구문이니 지원을 안한다고 볼 수 있다.  비동기 처리 키워드(async, await)를 사용하려면 설정을 추가해줘야한다.

*Parcel : 코드 분할 내용 중에서...*
>  만약 브라우저에서 async/await 를 사용하고 싶다면, babel-polyfill을 앱에 포함시키거나 babel-runtime + babel-plugin-transform-runtime이 라이브러리에 있어야 합니다. 그냥 사용하려고 하지 마세요. babel-polyfill와 babel-runtime를 읽어보세요.

[babel 공식 문서](https://babeljs.io/docs/en/babel-plugin-transform-runtime)
babel-polyfill 
> 🚨 Babel 7.4.0부터 이 패키지는 core-js/stable(ECMAScript 기능을 폴리필하기 위해) 및 regenerator-runtime/runtime(트랜스파일된 생성기 기능을 사용하는 데 필요) 직접 포함하기 위해 더 이상 사용되지 않습니다.

babel-runtime
```shell
npm install --save-dev @babel/plugin-transform-runtime
npm install --save @babel/runtime
```
파일 설정
```JSON
{
  "plugins": ["@babel/plugin-transform-runtime"]
}
```
또는
```JSON
{
  "plugins": [
    [
      "@babel/plugin-transform-runtime",
      {
        "absoluteRuntime": false,
        "corejs": false,
        "helpers": true,
        "regenerator": true,
        "version": "7.0.0-beta.0"
      }
    ]
  ]
}
```

app.js
```javascript
import 'regenerator-runtime/runtime';
```



