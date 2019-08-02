- - - 
# AUG 1 2019  

____


# <strong> 1. Main Topic </strong>

- [함수 선언식](#1)

- [함수 표현식](#2)

- [구글 함수 선언 가이드](#3)




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF" id="1"> [함수] 1-1. JS 에서 함수 선언식 </span>    

### 함수 선언식 FUNCTION DECLARATION 

```js
function declaration() {
  console.log("Declaration")
}

declaration();  // Declaration
```

일반적으로 function .... 으로 시작하는 함수 선언 방법

함수 선언식을 이용하면 `호이스팅` 이 가능하다

```js
declaration();  // Declaration

function declaration() {
  console.log("Declaration")
}
```

<br></br>


### 호이스팅은 함수일 때 가능하다

```js
const person = "Kate"

function declaration() {
  console.log("Declaration", person)
}

declaration();  // Declaration Kate  정상 작동
```

그러나 선언 순서를 변경하면

```js
declaration();  // Declaration

const person = "Kate"

function declaration() {
  console.log("Declaration", person)  // Error
}
```

아래 declaration() 함수의 경우 호이스팅이 가능하지만, 변수 person 에 대해서는 가능하지 않다.

함수가 시작될 때, person 에 대한 선 정의가 이루어지지 않았으므로 에러 발생.

<br>

## <span style="color:#595EFF" id="2"> [함수] 1-2. JS 에서 함수 표현식 </span>     

### 함수 표현식 FUNCTION EXPRESSTION 

함수 표현식으로 함수를 정의해주는 방법은 두 가지.

```js
const expression = function() {
  console.log("Expression")
} 

expression() // Expression
```

또는 화살표 함수를 사용한

```js
const expression = () => {
  console.log("Expression")
}

expression() // Expression
```


### 함수 표현식 호이스팅

함수 선언식으로 정의된 함수와는 다르게 `함수 표현식`으로 정의된 함수의 경우 `호이스팅이 일어나지 않는다.`

```js
expression() // Error -> Cannot access 'expression' before initialization

const expression = () => {
  console.log("Expression")
}
```

<br>

## <span style="color:#595EFF" id="3"> [함수] 1-3. 구글 함수 선언 가이드 </span>     

### 구글에서 말하는 함수 선언시 가이드 정책

#### 1. Use named function expressions instead of function declarations.

`함수 호이스팅에 의해 원치 않는 동작을 할 가능성`이 있으므로, 일반적으로 함수를 선언할 경우에는

`함수 표현식`을 기본으로 하자.

```js
// bad
function foo() {
  // ...
}

// bad
const foo = function () {
  // ...
};

// good
// lexical name distinguished from the variable-referenced invocation(s)
const short = function longUniqueMoreDescriptiveLexicalFoo() {  // 단 함수의 이름을 부여하도록 하자
  // ... 
};
```



<br></br>
# <strong> 3. References </strong>


From web sites ...

- 

From Youtube videos...

- <a href="https://www.youtube.com/watch?v=VAYIPSNXHhw" target="_blank">Function Declarations vs Function Expressions</a>
