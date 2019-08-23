- - - 
## <strong> 1. Summary / Ref </strong>

- [SandGrid](https://sendgrid.com) : 무료 email sending API & SMTP 

  - 30,000 email First 30 day. After 100 email / day

  - Node.js 를 포함한 다양한 언어 API 제공

  - 단순 데이터 내용만 메일 전송하고 싶다면 v2 버젼을, 경우에 따라 데이터를 유동적으로 보내야한다면 (e.g. Marketing) v3 버젼.

<br>

____
____


## <strong> 2. Usage / Content </strong>


### <span style="color:#595EFF"> [Node.js] 1-1. v2 버젼 npm 설치 & 사용법 </span>    

사이트 가입 및 API 설정!

.env 파일 생성 및 API_KEY 설정 후,

```js
npm install --save @sendgrid/mail

const sgMail = require('@sendgrid/mail');
sgMail.setApiKey(process.env.SENDGRID_API_KEY);

const msg = {
  to: 'test@example.com',
  from: 'test@example.com',
  subject: 'Sending with Twilio SendGrid is Fun',
  text: 'and easy to do anywhere, even with Node.js',
  html: '<strong>and easy to do anywhere, even with Node.js</strong>',
};

sgMail.send(msg);
```

자세한 내용은 아래 

[SendGrid v2 GitHub md](https://github.com/sendgrid/sendgrid-nodejs/tree/master/packages/mail)



<br />
### <span style="color:#595EFF"> [Node.js] 2-1. v3 다이나믹 템플릿 제작 & 데이터 구조 </span>

#### 템플릿 제작

User 메뉴에서 탬플릿 제작. 이하 내용 생략.

탬플릿 제작 후, `탬플릿 ID` 확인할 것. ex) d-XXXX

템플릿에 들어갈 유동적 데이터는 dynamic_template_data 테이블에서 조정.


```js
{
  personalizations: [{
    to: [{
      email: 'test@gmail.com',
      name: 'John Doe'
    }],
    dynamic_template_data: {
      user: '1',
      language: 'en',
      age: '19',
      date: 'Jan.08.2020'
    }
  }],
  from: {
    email: 'test@gmail.com',
    name: 'Kate Doe'
  },
  template_id: 'd-xxxx'
}
```

<br />

개발 환경에 맞게 request 를 보내면 되는데, 사이트에서 제공해주는 코드 제너레이터 를 활용!

Click `"MAIL SEND"` on the `Left side`. [SendGrid v3 API Doc](https://sendgrid.com/docs/API_Reference/api_v3.html)



<br />

예시 중 하나는 `unirest` Node.js Library

```js
var unirest = require("unirest");

var req = unirest("POST", "https://api.sendgrid.com/v3/mail/send");

req.headers({
  "content-type": "application/json",
  "authorization": "Bearer <<YOUR_API_KEY>>"
});

req.type("json");
req.send({
  "personalizations": [
    {
      "to": [
        {
          "email": "john.doe@example.com",
          "name": "John Doe"
        }
      ],
      "dynamic_template_data": {
        "noun": "",
        "currentDayofWeek": ""
      },
      "subject": "Hello, World!"
    }
  ],
  "from": {
    "email": "noreply@johndoe.com",
    "name": "John Doe"
  },
  "reply_to": {
    "email": "noreply@johndoe.com",
    "name": "John Doe"
  },
  "template_id": "<<YOUR_TEMPLATE_ID>>"
});

req.end(function (res) {
  if (res.error) throw new Error(res.error);

  console.log(res.body);
});
```


___
___