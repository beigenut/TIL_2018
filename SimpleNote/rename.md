- - - 
# May 13 2019  

____


# <strong> 1. Main Topic </strong>

- [전역 스코프](#1)

- [지역 스코프: 함수 스코프, 블록 스코프](#2)
  - function(){}  +subset  //  {}

- [함수 선언식 vs 함수 표현식 그리고 함수 호이스팅](#3)
  - function f_Declaration(){}  // const f_Expression = function(){} 

- [네스티드 스코프](#4)
  - function() { functio() {} }
  
- [렉시컬 스코핑(lexical scoping)](#4-1)
  - 변수의 유효 범위(scope)는 함수의 실행단이 아닌 선언단부터 정의된다
  - 유효 범위는 즉, 변수의 참조가 어디를 가르키는지

- [클로져](#6)
  - 고차 함수 내부의 함수
  - 클로져는 자신을 감싸는 외부 함수의 변수에 접근할 수 있다 

- [스코프 디버깅](#7)
  - debugger 코드 삽입 
  - 개발자 도구 breakpoint 추가




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF" id="1"> [스코프] 1-1. 전역(Global) 스코프 </span>    


### 전역 변수 : A Declared variable outside of {} or a function 

전역 스코프에 속하는 `전역 변수`는 코드 어느부분에서도 접근 가능하며 <br> 함수 안에서도 접근 가능하다

하지만, 전역 변수로 선언을 자제하는 것이 좋다. 

> 변수 중복 선언 가능성 때문에



<br>

## <span style="color:#595EFF" id="2"> [스코프] 1-2. 지역(local) 스코프 </span>     

JS 에는 2가지 지역 스코프가 존재; 함수 스코프, 블록 스코프


### 함수 스코프 

함수 내부에 선언된 변수. 이때 선언된 변수는 함수 안에서만 접근 가능하다.

```js
function sayHello () {
  const hello = 'Hello CSS-Tricks Reader!'
  console.log(hello)
}
sayHello() // 'Hello CSS-Tricks Reader!'
console.log(hello) // Error, hello is not defined
```


### 블록 스코프 

{}: curly bracket 안에서 선언된 변수. 해당 블록 안에서만 변수의 접근이 가능.

```js
{
  const hello = 'Hello CSS-Tricks Reader!'
  console.log(hello) // 'Hello CSS-Tricks Reader!'
}
console.log(hello) // Error, hello is not defined
```

* 표현 유의,

함수를 선언할 때, 중괄호를 사용하게 되는 경우가 대부분 있는데 이때 스코프를 정의할 때에는 <br>
함수 스코프안에 블록 스코프에 감싸져 있다고 보면된다.

즉, (이 경우) 블록 스코프는 함수 스코프의 `서브셋(subset)` 이다

```js
function func(){
  // 블록 스코프 = func() 함수의 서브셋
  ...
}
```




<br>

## <span style="color:#595EFF" id="3"> [스코프] 2-1. 함수 호이스팅 </span> 

함수가 `함수 선언식 (function declaration)`으로 선언되면, 현재 스코프의 최상단으로 호이스팅 된다.

```js
sayHello()
function sayHello () {
  console.log('Hello CSS-Tricks Reader!')
}
// This is the same as the code above
function sayHello () {
  console.log('Hello CSS-Tricks Reader!')
}
sayHello()
```

함수 호출이 먼저 일어나든 함수가 선언된 이후에 일어나든 문제없이 동작한다.

<br>

but, 

함수가 `함수 표현식 (function expression)`으로 선언되면 호이스팅 되지 않는다.

```js
sayHello() // Error, sayHello is not defined
const sayHello = function () {
  console.log(aFunction)
}
```


<br>

### 각 함수 스코프에서 선언된 변수에 서로 접근할 수 없다

당연하다.

혼동하지 말아야 할 점은 이전에 선언된 (전역)함수를 후반 선언될 함수에서 호출하는 것은 가능하다.

```js
function first () {
  const firstFunctionVariable = 'I’m part of first'
  console.log(firstFunctionVariable)
}
function second () {
  first()
}

second()   // I’m part of first 출력
```



<br>

## <span style="color:#595EFF" id="4"> [스코프] 3-1. 네스티드 스코프 </span> 

함수가 다른 함수 내부에서 정의되었다면, 내부 함수는 외부 함수의 변수에 접근할 수 있습니다. 

```js
function outerFunction () {
  const outer = 'I’m the outer function!'
    
  function innerFunction() {
     const inner = 'I’m the inner function!'
     console.log(outer) // I’m the outer function!
  }
    
  console.log(inner) // Error, inner is not defined
}

console.log(outer)  // Error
```

<br>

## <span style="color:#595EFF" id="4-1"> [스코프] 3-2. 렉시컬 스코핑 </span> 

네스티드 스코프에서 알아야 할 `렉시컬 스코핑(Lexical scope) 한:어휘적 유효 범위` 이 있다.

렉시컬 스코핑이란 `Scope가 함수 실행 시점이 아닌 함수 정의 시점에 정해진다는 의미`


> 함수 실행 시점에서 그 함수의 스코프가 정해지는 것이 아니라 선언 시점부터 이미 함수의 스코프가 정해져 있다는 의미

라고 해석하면 되나?

```js
let name = "zero"
function log() {
  console.log(name)
}
function wrapper() {
  name = "nero"
  log()
}
wrapper()     // nero
```

```js
let name = "zero"
function log() {
  console.log(name)
}
function wrapper() {
  let name = "nero'
  log()
}
wrapper()    // zero
``` 

log() 함수는 선언 시점부터 전역 변수 name을 참조하고 있다

위의 함수는 전역 변수로 선언된 name(log()가 참조하고 있는) 변수에 새로운 값을 할당하고 그 값을 호출을<br>
아래 함수는 전역 변수 name 과는 별개로 함수 스코프 안에서 새로운 name 변수가 선언되었을 뿐, (log() 함수가 참조하고 있는)전역 변수 name의 새로운 할당은 없었다.

이와 같이 `변수의 선언 시점부터 이미 그 변수의 유효 범위는 지정`되어 버린다는 의미? 그리고 <br> 
함수가 실행되는 순간 변수를 참조하는 것이 아니라 `정의될 때부터 변수를 이미 참조`하고 있다

<br>

함수가 실행되는 순간의 변수를 참조한다면 아래 예제에서 wrapper() 가 실행된 후 <br>
log() 의 name 참조가 wrapper()에서 새로 선언된 name 이 되어버린 다는 것 같은<br>
억지 상황이 발생하게 된다.


<br>


### 그림으로 스코프 이해하기

스코프를 취조실(시각의 단방향)이라 생각하면.. 

[<img src="https://cdn-images-1.medium.com/max/1200/1*94wTu61tmltShnyb5U0kgw.png">]()



<br></br>
## <span style="color:#595EFF" id="6"> [클로져] 4-1. 클로져 </span> 

클로져 : 네스티드된 함수 스코프에서 존재하는 내부 함수

이때 클로져는 `외부 함수의 변수를 참조`한다

```js
function outerFunction () {
  const outer = 'I see the outer variable!'
  
  return function innerFunction() {    // 내부 함수를 외부 함수의 return 으로 넘겨준다
    console.log(outer)                 // innerFunction() 이 클로저 
  }
}
// 클로져를 이용해 외부 함수의 변수 outer 를 참조하여 값을 호출할 수 있다
outerFunction() // I see the outer variable!
```

### 클로져로 private 변수 선언하기

클로져의 성질을 이용해 가장 유용하게 사용하는 방법은 

`밖에서 접근할 수 없고`, `정해진 방법을 통해서만 데이터에 접근`할 수 있도록 `제한`하는 것이다.


여기서 `private 변수`란 외부 함수가 종료되고 접근할 수 없는 내부 함수의 변수를 말한다 


```js
function makeCounter(x = 1) {
  return function() {
    return x++;
  }
}
// `x`를 직접 변경할 수 있는 방법이 없다
const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

코드가 2차 배포되고 누군가 코드를 수정하면서 실수로 `변경되지 말아야 할 변수의 값`을 변경하는 

실수를 방지할 수 있다. 



<br></br>
## <span style="color:#595EFF" id="7"> [디버깅] 5-1. 스코프 디버깅 </span> 

개발자 도구를 사용해서 클로저 안에 들어잇는 변수들을 알아낼 수 있다.

원하는 함수 내부에 `debugger` 코드를 삽입한다

```js
function prepareCake(flavor) {
  return function () {
    debugger
    setTimeout(_=>console.log(`Make a ${flavor} cake!`), 1000)
  }
}
const makeCakeLater = prepareCake('banana')
```

개발자 도구를 열고 `source` 탭을 확인하면 

[<img src="https://cdn-images-1.medium.com/max/1200/1*Si3yT9ln7dOuuzNuwEGFaA.png">]()



<br>

디버거 코드를 삽입하는 방법 이외에도 `breakpoint`를 추가하는 방식이 있는데,

개발자 도구 - source 탭에서 디버깅을 할 원하는 코드 부분에 `breakpoint` 를 추가한다.

[<img src="https://cdn-images-1.medium.com/max/1200/1*qtVfWXZ3jgDIOu5ZId6PQQ.png">]()


> 이미지 출처 [링크]("https://medium.com/@khwsc1/%EB%B2%88%EC%97%AD-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80-javascript-scope-and-closures-8d402c976d19")






<br></br>
# <strong> 3. References </strong>


From web sites ...

- <a href="https://fullest-sway.me/blog/2017/11/13/js-closure/" target="_blank">클로져란? - 스코프, 렉시컬 스코프</a>


- <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures" target="_blank">MDN - 실용적인 클로져, 프라이빗 메소드 생성, 클로져 스코프 체인</a>


From Youtube videos...

- <a href="https://www.youtube.com/watch?v=CA5EDD4Hjz4&list=WL&index=36&t=0s" target="_blank">자바스크립트 promise? 나도 써보자, 기본 개념부터</a>

- <a href="https://www.youtube.com/watch?v=JzXjB6L99N4&t=612s" target="_blank">자바스크립트 async / await? 나도 써보자, 기본 개념부터</a>