- - - 
# May 08 2019  

____


# <strong> 1. Main Topic </strong>

- 콜백 지옥

- 콜백 지옥의 문제점 / 해결 방법

- Promise 

- Async / Await 사용 이해




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF"> [Callback] 1-1. 콜백, 그리고 콜백 지옥 </span>    


### 자바 스크립트에서 비동기 처리란?

`특정 코드의 실행이 완료될 때까지 기다리지 않고` 다음 코드를 먼저 수행하는 자바스크립트의 특성



### 콜백지옥이란, 

```js
step1(function (value1) {
    step2(function (value2) {
        step3(function (value3) {
            step4(function (value4) {
                step5(function (value5) {
                    step6(function (value6) {
                        // Do something with value6
                    });
                });
            });
        });
    });
});
```


### NESTING ! 

비동기 프로그램 작성시 위의 코드처럼 함수가 함수의 `함수의 매개 변수로 꼬리물며` 넘겨지면서 생겨나는 반복 코드. 




### 이게 왜 문제?

- 비동기 함수의 결과값을 받아 다음 함수로 넘겨줘야 하는 경우 코드가 복잡해짐. 머리가 아파짐.
  - Promise 는 return 값으로 resolved 된 결과 값을 넘겨줄 수 있고 .then() 에서 받아 쓸 수 있음
  - 다른 이야기지만, React 에서 this.state 값을 Provider 를 통해 props 으로 넘겨주고 Consumer로 받아 쓰는 느낌?

- 적힌 순서대로 코드가 작동하지 않는다는 것. 
  - 비동기 처리를 위한 콜백패턴이 처리순서를 보장하지 않는다

- 에러 처리에 한계가 있다
  - 비동기처리 함수는 콜백함수를 호출하고 그것이 완료되기 전에 바로 호출스택을 빠져나가는데 (콜백)함수를 호출한 호출자가 사라지는 경우 발생




### 콜백지옥 해결 방안?

1. `동기 함수`를 사용한다

간단하게 동기 함수들을 나열해서 프로그램을 동작하게 하면 된다. 하지만, `먼저 선언된 함수가 종료될 때까지 지체`된다.

- 용량이 큰 파일을 전송하는 함수가 먼저 있을 경우 페이지 로딩이 길어짐

- Node.js 이용 서버의 경우 한 사람의 요청이 끝날 때까지 다른 사람의 요청은 받을 수가 없음

등의 문제가 발생할 수 있다.

<br>

2. 콜백 함수를 각자 `분리, 사용`한다

꼬리에 꼬리를 무는 콜백 함수의 동작 원리는 같지만, 가독성을 높이는 방법으로 각 함수를 분리해서 따로 호출한다.

```js
step1(afterStep1);
function afterStep1(value1) {
    step2(afterStep2);
}
function afterStep2(value2) {
    step3(afterStep3);
}
// 생략..
```

단점은 

`전역(Global)/ 지역(Local) 스코프에 유의하여 변수를 정의`해줘야 한다

글로벌 스코프로 변수 정의하면 쉽게 문제는 해결되지만, 차후 코드가 길어질 경우 <br> 관리가 힘들어질 수 있으며,실수로 중복 변수 이름을 선언할 경우 에러 발생. const let var 선언 유의.




<br></br>
<!-- ***********************두번째 제목******************** -->
## <span style="color:#595EFF"> [Promise] 2-1. Promise </span>


### Promise?

```js
function delay(sec, callback) {
  setTimeout(() => {
    callback(new Date().toString())
  }, sec * 1000)
}

delay(1, (result) => {
  console.log(1, result)

  delay(1, (result) => {

    delay(1, (result) => {
      console.log(3, result)
    })
    console.log(2, result)
  })
})
```

결과는 각 1 초마다 비동기 콜백 함수를 인자로 갖는 함수들이 호출된다.

```
1 "Thu May 09 2019 01:24:20 GMT-0400 (Eastern Daylight Time)"
2 "Thu May 09 2019 01:24:21 GMT-0400 (Eastern Daylight Time)"
3 "Thu May 09 2019 01:24:22 GMT-0400 (Eastern Daylight Time)"
```

`하지만, 코드 가독성이 낮다`


<br>

이를 보안하기 위해 나온 `Promise` 를 이용해서 동일한 작동을 하는 비동기 함수를 작성하면

```js
function delayPromise(sec){
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(new Date().toString())   // {..} 가 resolved 되면 resolve 매소드 호출
    }, sec * 1000)                     // 단, reject 되면 reject() 매소드 호출
  })                                   // resolve(), reject() 모두 .then() 가능 
}

delayPromise(1).then((result) => {
  console.log(1, result)
  return delayPromise(1)
}).then((result) => {
  console.log(2, result)
  return delayPromise(1)
}).then((result) => {
  console.log(3, result)
})
```

위와 같다. 가장 마지막 콜백 함수의 return 값을 따로 넣지 않아도 된다.

이해할 부분은, then의 리턴값은 Promise 이고 resolve 된 Promise 를 지정하지 않으면<br> undefined 이 바로(return으로 비동기 Promise를 호출하지 않았을 경우) 출력된다.




<br></br>
<!-- ***********************세번째 제목******************** -->
## <span style="color:#595EFF"> [Async/Await] 3-1. Async/Await </span>


### Async 함수 이해

Async 함수의 결과 값은 Promise 이다!

즉, async 함수는 .then() 매소드를 사용할 수 있다.

```js
function func1(){
  return 'function1'
}

async function fun2() {
  return 'function2'
}
```

를 콘솔에서 입력한 출력물은 아래와 같다

```
funcion1
Promise {<resolved>: "function2"}
```


```js
async function func2() {
  return 'function2'
  // async 에서 에러 reject 처리는 차후 논의
}

func2().then((result) => {  // result의 값은 async 함수의 리턴값
  // 함수..
})
```


### Await 사용 예제

`Await 가 붙으면 이 함수 종료될 때까지 뒤에 함수는 기다려라!`


```js
function delayPromise(sec){
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(new Date().toString())
    }, sec * 1000)
  })
}

async function func2(){
  delayPromise(3).then((time) => {
    console.log(time)
  })
  return 'function2'
}

func2().then((result) => {
  console.log(result)
})
```

위 코드의 출력값을 예상해보면 

1. async 함수의 return 값을 받는 아래 func2.then()의 결과가
2. "function2" 먼저 출력되고
3. setTimeout() 함수에 의해 3초뒤 
4. Date().toString() 함수의 결과값을 console.log() 함수에 의해 호출된 시간으로 출력된다.

<br>

만약 이 함수 출력 순서를 변경하여 delayPromise() 함수 처리 뒤에 func2().then()의 결과값을 출력하고자 한다면


```js
// 동일.. 

async function func2(){
  await delayPromise(3)  // await 가 적혀진 함수 부분이 끝날 때까지 그 뒤에 함수는 대기
  return 'function2'     // await 함수가 resolved 되면
}

func2().then((result) => {// then()의 결과는 return 값을 받아온다
  console.log(result)
})
```

여기까지 고친 함수의 출력은 3초 뒤 "function2" 가 출력이 된다. 기존처럼 시간을 출력하기 위해서는 await 함수의 결과값을 받을 변수를 선언해줄 수 있는데

```js
async function func2() {
  const time = await delayPromise(3)
  console.log(time);
  return 'function2'
}

func2().then((result) => {// then()의 결과는 return 값을 받아온다
  console.log(result)
})
```

1. 출력 없음,
2. 3초 뒤에 시각이 출력되고
3. "function2" 가 콘솔에 출력된다



<br>

### Await 특성

```js
// delayPromise() 동일.. 

async function func2() {
  const result = await delayPromise(3).then((instance) => {
    return "Done"
  })
  console.log(result);   // result = Done
  return 'function2'
}

func2().then((result) => {
  console.log(result)   // result = function2
})
```

출력 결과는 3초 뒤에

```
Done
function2
```


<br>

Await 는 Promise를 반환하는 함수에만 붙는다?

```js
function nthFunction(){
  return "Yes"
}

async function func2() {
  const result = await nthFunction()   // Promise 가 아닌 일반 함수 앞에도 await을 붙일 수 있다. 
                                       // 해당 코드 경우 붙이나 안 붙이나 동일함
  console.log(result);  // 물론 nthFunction() 의 return 값이 result 변수 값이되고
  return 'function2'
}

func2().then((result) => {
  console.log(result)   // 결과는 Yes 출력 후 function2 출력
})
```



<br>

### Promise 사용처?

Async/Await 의 장점은 피라미드 Callback 함수를 계속 쓰는 것보다 `가독성이 좋다`


예를 들어, logIn 서비스를 프로그래밍 한다고 할 때

```
getData(userInfo)
  .then(parseValue)
  .then(auth)
  .then(diaplay);
```

user의 정보를 받아서 그 값이 valid 한지 확인하고 그 결과로 인증하고, 인증된 결과값을 통해 어떠한 결과를 띄운다 의 프로세스를 Promise 를 반환하는 함수를 통해 구현한다고 했을 때, 

```js
const userInfo = {
  id: 'test@abc.com',
  pw: '****'
};

function parseValue() {
  return new Promise({
    // ...
  });
}
function auth() {
  return new Promise({
    // ...
  });
}
function display() {
  return new Promise({
    // ...
  });
}
```

와 같다면, .then() 을 통해 값들을 전달받으면서 활용할 수 있다




<br></br>
# <strong> 3. References </strong>


From web sites ...

- <a href="https://velog.io/@rohkorea86/Promiseis-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%8F%99%EA%B8%B0%EC%97%90%EC%84%9C-Promise%EA%B9%8C%EC%A7%80" target="_blank">Promiseis-비동기동기에서-Promise까지</a>


From Youtube videos...

- <a href="https://www.youtube.com/watch?v=CA5EDD4Hjz4&list=WL&index=36&t=0s" target="_blank">자바스크립트 promise? 나도 써보자, 기본 개념부터</a>

- <a href="https://www.youtube.com/watch?v=JzXjB6L99N4&t=612s" target="_blank">자바스크립트 async / await? 나도 써보자, 기본 개념부터</a>