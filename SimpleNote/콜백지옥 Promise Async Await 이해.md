- - - 
# May 08 2019  


## <strong> 1. References </strong>

- 시멘틱 마크업에 대해서 그리고 마크업 방법에 대한 설명 en ver.

> https://internetingishard.com/html-and-css/ 

- comments

> url





<br>

____
____


## <strong> 2. Today I learned </strong>


<!-- *********************첫번째 제목********************** -->
### <span style="color:#595EFF"> [Callback] 1-1. 콜백, 그리고 콜백 지옥 </span>    


#### 자바 스크립트에서 비동기 처리란?

`특정 코드의 실행이 완료될 때까지 기다리지 않고` 다음 코드를 먼저 수행하는 자바스크립트의 특성



<br>

#### 콜백지옥이란, 

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

비동기 프로그램 작성시 위의 코드처럼 함수가 함수의 `함수의 매개 변수로 꼬리물며` 넘겨지면서 생겨나는 반복 코드. 

이 과정에서 `에러 처리를 위한 코드까지 합쳐진다면` 꽤 많이 가독성 떨어지고 복잡한 프로그램이 탄생.


#### 콜백지옥 해결 방안?

1. `동기 함수`를 사용한다

간단하게 동기 함수들을 나열해서 프로그램을 동작하게 하면 된다. 하지만, `먼저 선언된 함수가 종료될 때까지 지체`된다.

- 용량이 큰 파일을 전송하는 함수가 먼저 있을 경우 페이지 로딩이 길어짐

- Node.js 이용 서버의 경우 한 사람의 요청이 끝날 때까지 다른 사람의 요청은 받을 수가 없음

등의 문제가 발생할 수 있다.

<br>

2. 콜백 함수를 각자 분리, 사용한다

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
### <span style="color:#595EFF"> [Promise] 2-1. Promise </span>


#### Promise?




<br></br>
<!-- ***********************세번째 제목******************** -->
### <span style="color:#595EFF"> [whatAbout] 3-1. title/comments </span>

comments

> comments



<br></br>
## <strong> 3. Today I found out </strong>

1. `comments`

> @import "comments"

<br>

2. comments comments



<br></br>

___
___