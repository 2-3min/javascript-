# xhr vs fetch
## 작성 계기
`fifa online 4 전적 검색 사이트` 프로젝트에서 "Fifa 데이터"는 `XmlHttpRequest`를 통해 가져왔다. `XmlHttpRequest`을 선택한 이유는 `비동기 프로그래밍`에 익숙하지 않았던 나에게 `비동기 통신 여부를 선택`할 수 있는 옵션이 있었기 때문이다.

하지만 이제 프로젝트의 기능이 점점 추가될 예정이고, `비동기 프로그래밍`이 아니기 때문에 데이터를 가져오는 동안 로직 진행이 비효율적이기 때문이다. 그래서 코드를 바꾸기 전에 `xhr`, `axios`, `fetch`에 대해 알아보고 정리하는 시간을 가져보고자 본 글을 작성했다.

## JS에서 통신 방법 3가지
* xhr(XmlHttpRequest)
* fetch
* axios

### xhr(XmlHttpRequest)
```javascript
//동기식
const USERINFO_URL = 'https://api.nexon.co.kr/fifaonline4/v1.0/users?nickname={nickname}';

const xhr = new XMLHttpRequest();

const getAccessKey = (member) => {
  const url = USERINFO_URL.replace('{nickname}', `${member}`);

  xhr.open('GET', url, true); //true : 비동기 처리 / false : 동기처리
  xhr.setRequestHeader('Authorization', API_KEY);

  xhr.onreadystatechange = function () {
    if(xhr.readyState === XMLHttpRequest.DONE) {
      var status = xhr.status;
      if (status === 0 || (status >= 200 && status < 400)) {
        console.log(xhr.responseText);
      } else {
        console.log("요청에 오류가 있습니다.");
      }
    }
  };
  xhr.send();
}

getAccessKey("짝사앙");
```

### fetch
```javascript
const USERINFO_URL = 'https://api.nexon.co.kr/fifaonline4/v1.0/users?nickname={nickname}';

const getAccessKey = (member) => {
  const url = USERINFO_URL.replace('{nickname}', `${member}`);
  fetch(url, {
    method: "GET",
    headers:{
      'Authorization': API_KEY
    }
  }).then(response => console.log(response.status))
  //Response {type: 'cors', ...}
    // body: (...)
    // bodyUsed: false
    // headers: Headers {}
    // ok: true
    // redirected: false
    // status: 200
    // statusText: ""
    // type: "cors"
    // url: "api.nexon.co.kr/..."
    // [[Prototype]]: Response
  .catch(err => console.log(err));
}

getAccessKey("짝사앙");
```

### 왜 XMLHttpRequest가 아니라 Fetch를 썼는가?
- 에러처리에서 유연하다.
- fetch가 좀 더 가독성에서 직관적이다.
- `fetch()`가 반환하는 `Promise`는 response가 HTTP 404, 500 같은 `HTTP error status`여도 거부하지 않고 다 받아온다.
  
😄 조금 더 느껴보고 쓸 예정...(2022.03.19)