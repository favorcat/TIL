# Twitter API를 이용하여 Welcome Message 설정하기
> Welcome Message는 상대방이 나의 계정으로 DM을 보내려고 할 때, 자동적으로 보내지는 메세지이다.

### [Postman 설치](https://www.postman.com/downloads/)
1. Create new HTTP Request
2. Authorization 탭 이동
    - Type : `OAuth 1.0`
    - Add authorization data to `Request Headers`
    - `Consumer Key` : Twitter API 앱의 Consumer Key
    - `Consumer Secret` : Twitter API 앱의 Consumer Key Secret
    - `Access Token` : Oauth를 통해 받아온 welcome message를 사용할 계정의 Token
    - `Access Secret` : Oauth를 통해 받아온 welcome message를 사용할 계정의 Token Secret


### 1. Welcome Message 설정    
`POST` https://api.twitter.com/1.1/direct_messages/welcome_messages/new.json    
`Body` 탭에서 `raw` `JSON` 선택
``` json
{
  "welcome_message" : {
    "name": "simple_welcome-message 01",
    "message_data": {
      "text": "Welcome!"
    }
  }
}
```
메세지 작성 방법은 [링크참조](https://developer.twitter.com/en/docs/twitter-api/v1/direct-messages/welcome-messages/api-reference/new-welcome-message)

### 2. rule 설정    
`POST` https://api.twitter.com/1.1/direct_messages/welcome_messages/rules/new.json    
`Body` 탭에서 `raw` `JSON` 선택
``` json
{
  "welcome_message_rule": {
    "welcome_message_id": "id"
  }
}
```
`id` 부분에 1번에서 message 설정을 하여 send를 한 결과에 있는 id를 입력한다.

### 3. Welcome Message 수정
`PUT` https://api.twitter.com/1.1/direct_messages/welcome_messages/update.json?id=""    
`id=""` 부분에 1번에서 message 설정을 하여 send를 한 결과에 있는 id를 입력한다.    
`Body` 탭에서 `raw` `JSON` 선택
``` json
{
  "message_data":{
    "text": "Welcome!"
  }
}
```

### 4. 설정된 Welcome Message 확인
`GET` https://api.twitter.com/1.1/direct_messages/welcome_messages/list.json

### 5. 설정된 Welcome Message 삭제
`DELETE` https://api.twitter.com/1.1/direct_messages/welcome_messages/destroy.json    
`Params` 탭에서 KEY : `id`  , VALUE : `4번에서 얻은 id`