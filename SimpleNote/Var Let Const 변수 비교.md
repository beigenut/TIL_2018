- - - 
# May 14 2019  

____


# <strong> 1. Main Topic </strong>

- [Var vs Const vs Let](#1)



<br></br>
# <strong> 2. Sub Topics </strong>

## <span style="color:#595EFF" id="1"> [변수] 1-1. Var vs Let vs Const </span>    

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
# <strong> 3. References </strong>

