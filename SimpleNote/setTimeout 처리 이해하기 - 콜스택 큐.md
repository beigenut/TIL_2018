Last edited May 07 2019 
---


## <strong> 1. MAIN TOPIC </strong>

- 자바 스크립트 싱글 스레드 
- 콜스택 
- 큐 
- 브라우저API의 setTimeout() 

4가지 역할 이해 -> 예상과 실제 코드 결과 확인 



<br></br>
## <strong> 2. SUB TOPICS </strong>

### <span style="color:#595EFF"> [JS] 1-1. JS 싱글스레드 때문에 생기는 일 </span>    

자바 스크립트는 `싱글 스레드` 이다. 때문에 비동기 처리에 있어서 몇가지 제약 상황이 생긴다. <br>
이를 제대로 이해하지 못하면 예상했던 방향과는 다른 순서로 결과가 나오기 때문에 주의하도록!


예시 코드 보기 앞서 짚고 넘어갈 것은

- setTimeout() 은 콜 스택에서 순차처리되는가?
- 브라우저API 에서 setTimeout()을 별개 처리된다면 예약된 시간 뒤에 콜 스택에서 처리되는가?
- setTimeout()에 for 루프를 걸면?
- 아래와 같이 선언된 함수 밖 가장 마지막에 선언된 함수의 처리는 순서는 언제인가?


```js
function taskOrder(){
  setTimeout(function(){
    console.log('1.5s passed')
  }, 1500)
  for(let i = 0; i < 3; i++){
    setTimeout(function() {
    console.log(i)
    }, 1000)
    setTimeout(function() {
      console.log('Interrupt')
    }, 2000)
  }
  console.log('is been 3s?')
}

taskOrder();

console.log('taskOrder function done')
```


해당 코드의 처리 결과는 아래와 같음 
<a href="https://repl.it/@beigenut/kyu-kolseutaeg-sestaimaus-3gaji-ceori-sunseo-bogi">코드 링크</a>


```
is been 3s?
taskOrder function done  콜스택이 싱글 스레드 이기 때문에!
                         taskOrder()보다 뒤에 후선언되었어도 먼저 처리됨
=> undefined             setTimeout() 은 브라우저API 에서 콜스택과는 별개
                         처리되므로 15 line까지 다 처리되었다는 이야기
0                        매 1초당 순차적으로 찍히는 것이 아니라 동시 다발적으로 0 1 2 찍힘
1                        setTimeout() 이 돌아가는 방식을 이해해야 하는 부분
2                        매 1초당 순차적으로 특정/반복 함수가 돌아가게 하기 위해서는 각각 비동기 처리해야함
1.5s passed
Interrupt                2초 뒤에 for 문이 0 1 2 산출 함수와는 별개로 다시 돌아간다
Interrupt
Interrupt
```




<br></br>
## <strong> 3. REFERENCES </strong>

none


<br></br>

___
___