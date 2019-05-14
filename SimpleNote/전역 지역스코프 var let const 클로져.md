- - - 
# May 13 2019  

____


# <strong> 1. Main Topic </strong>

- 전역 스코프

- 지역 스코프 : 함수 스코프, 블록 스코프
  - function(){}  +subset  //  {}

- 함수 선언식 vs 함수 표현식 그리고 함수 호이스팅
  - function f_Declaration(){}  // const f_Expression = function(){} 

- 네스티드 스코프
  - function() { functio() {} } ; 렉시컬 스코핑(lexical scoping)

- Var vs Const vs Let

- 클로져

- 스코프 디버깅




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF"> [스코프] 1-1. 전역(Global) 스코프 </span>    


### 전역 변수 : A Declared variable outside of {} or a function 

전역 스코프에 속하는 `전역 변수`는 코드 어느부분에서도 접근 가능하며 <br> 함수 안에서도 접근 가능하다

하지만, 전역 변수로 선언을 자제하는 것이 좋다. 

> 변수 중복 선언 가능성 때문에



<br>

## <span style="color:#595EFF"> [스코프] 1-2. 지역(local) 스코프 </span>     

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

## <span style="color:#595EFF"> [스코프] 2-1. 함수 호스팅 </span> 

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


### 네스티드 스코프 

함수가 다른 함수 내부에서 정의되었다면, 내부 함수는 외부 함수의 변수에 접근할 수 있습니다. 

다른말로 `렉시컬 스코핑(lexical scoping)`이라 칭한다.

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


### 그림으로 스코프 이해하기

스코프를 취조실(시각의 단방향)이라 생각하면.. 

[<img src="https://cdn-images-1.medium.com/max/1200/1*94wTu61tmltShnyb5U0kgw.png">]()




<br></br>
## <span style="color:#595EFF"> [변수] 3-1. Var vs Let vs Const </span>    

### var

ES6 이전에 사용되던 var 의 경우, 

중복 선언되는 경우 에러를 발생시키지도 않고, 선언 `덮어쓰기`가 가능해진다.

실수로 중복 선언하는 경우에 결과가 꼬일 수 있으니 사용하지 않도록 한다.

```js
var foo = "stupid"
var foo = "smart"  // 에러 없음
```

var 로 선언된 변수는 `호이스팅` 메커니즘에 의해 `끌어올려진다`. 

```js
console.log(bar)
var bar = "let's go"  // 에러 없이 "let's go" 출력됨
```

var 변수 호이스팅 방지를 위해서는 매 스코프마다 엄격 모드 사용을 지정해줘야 한다. `use strict`

<br>

결론적으로 `var 쓰지말자`



### const

딱 한번만 선언될 수 있으며, 같은 이름을 같는 변수를 중복 선언할 경우 에러가 난다.

어떠한 이유에도 한번 정의된 값은 변경되지 않는다.

변수의 선언과 값의 할당이 동시에 이루어져야 한다.

```js
const b = 200;
```

블록 스코프 {} / 함수 스코프 안에 선언된 const 변수는 글로벌 스코프에서 선언된 변수에 영향을 미치지 않는다.

```js
const run = 1;

function work() {
  const run = 2;
  console.log(run)   // 2 
}

work();
console.log(run)   // 1

{
  const run = "It works?"  // 서로 다른 스코프에 속한 변수들
  console.log(run)         // It works? 출력
}
```


### let

선언은 딱 한번만 할 수 있지만, 값을 경우에 따라 변경할 수 있다. 즉, 값 재할당이 가능하다.

변수의 선언과 값의 할당은 따로 이루어질 수 있다.

```js
let a;
a = 100;
```



<br></br>
## <span style="color:#595EFF"> [스코프] 4-1. 클로져 </span> 

클로져 : 네스티드된 함수 스코프에서 내부 함수

```js
function outerFunction () {
  const outer = 'I see the outer variable!'
  
  return function innerFunction() {    // 내부 함수를 외부 함수의 return 으로 넘겨준다
    console.log(outer)                 // innerFunction() 이 클로저 
  }
}
outerFunction()() // I see the outer variable!
```

외부 함수의 변수에 접근할 수 있는 `클로져의 목적`은 

- 사이드 이펙트 제어하기

- private 변수 선언하기


### 클로져로 사이드 이펙트 제어하기




### 클로져로 private 변수 선언하기


<br></br>
# <strong> 3. References </strong>


From web sites ...

- <a href="https://velog.io/@rohkorea86/Promiseis-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%8F%99%EA%B8%B0%EC%97%90%EC%84%9C-Promise%EA%B9%8C%EC%A7%80" target="_blank">Promiseis-비동기동기에서-Promise까지</a>


From Youtube videos...

- <a href="https://www.youtube.com/watch?v=CA5EDD4Hjz4&list=WL&index=36&t=0s" target="_blank">자바스크립트 promise? 나도 써보자, 기본 개념부터</a>

- <a href="https://www.youtube.com/watch?v=JzXjB6L99N4&t=612s" target="_blank">자바스크립트 async / await? 나도 써보자, 기본 개념부터</a>