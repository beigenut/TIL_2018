- - - 
## May 16 2019  

____


# <strong> 1. Main Topic </strong>

- [This](#1)
  - `생성자 함수와 객체의 매소드`를 제외한 모든 함수(화살표, 내부, 콜백을 포함) 내부의 this 는 전역 객체를 참조한다

- [함수와 메소드](#2)
  - 메소드 : 객체의 속성(Property)이 함수인 것

- ['객체'는 어디까지 포함인가](#3)
  - 배열 함수 값 메소드 ..

- [This 그리고 .bind() .call()](#4)
  - func.bind(object)

- [Arrow function ](#5)
  - 익명함수 || 생성자X || 콜백함수 || No this || 제너레이터X || .bind() X
  - 화살표 함수의 this 는 lexical this => 상위 스코프의 this 를 참조 

- [Arrow function 이 갖는 유용성](#6)
  - 함수를 다른 함수의 인스턴스로 넘겨줄 때 유용
  - 일반 함수 선언식보다 간결, 특히 콜백 함수로 사용할 때
  - lexical scoping 은 binding 의 번거로움을 없애줌
  - 화살표 함수를 포함하는 함수 스코프(context)의 this 를 이어 받는다

- [매계변수의 기본값](#7)
  - function callMe(name = 'mary'){console.log(name)} ... callMe()




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF" id="1"> [This] 1-1. This 의 정의 This 가 가르키는 것 </span>    


### This 

This 를 사용하면 `메소드 !호출! 시`에 해당 `메소드를 갖고 있는 객체`에 접근

* `메소드` => 데이터와 그 데이터와 관련한 동작(함수)를 객체 라는 하나의 단위로 묶어 다룰 수 있다 
          => 객체 안에는 값도 함수도 포함될 수 있으니까

```js
function test(x, y) {  // 일반적인 함수
  return x+y;
}

const person = {       // 하나의 객체
  name: '윤아준',       // name, age 라는 파라미터와 introduce() 라는 함수 파라미터
  age: 19,
  introduce() {        // 객체 안에 정의된 함수 = 메소드
    return `안녕하세요, 제 이름은 ${this.name}입니다. 제 나이는 ${this.age}살 입니다.`
                      // 여기서의 this. 는 이 메소드를 포함하고 있는 객체 즉, person 이다
  }
};
```




<br></br>
## <span style="color:#595EFF" id="2"> [This] 2-1. 함수와 메소드의 차이</span>  

자바 스크립트에서...

- 함수 : 기능
  - Global/Local 에 무관하게 독립적으로 정의되는 !객체! 선언되고 호출(invoked)되어 사용된다
  - ex) myFunction();

- 메소드 : 방법
  - 객체의 property 로 function 인 것
  - ex) obj.otherFunction();
  - ex) myFunction.bind(obj)





<br></br>
## <span style="color:#595EFF" id="3"> [This] 3-1. 객체 포함 범위</span>  

객체 안에는 다양한 Property(변수/요소)들이 존재할 수 있고 그 프로퍼티들은

- 값

- 배열 (배열 내부의 값들을 `요소`라 칭하지만 JS에서 배열 = 객체. 요소/변수 구분하지 않는다)

- 함수

- 객체 안에서 정의된 메소드

등이 될 수 있다 



<br>

### This는 생성자 혹은 메소드에서 어떤 "객체"를 가리킬 때 사용하는 키워드이다

하지만, 생성자나 메소드가 아닌 곳에서 This 키워드를 사용한다고 에러는 나지 않는다

`주인없는 this`

```js
function printThis() {
  console.log(this); // this 는 윈도우 = 브라우저 를 가르킨다
                     // 왜? function 자체가 전역 객체이기 때문에
}

printThis(); // Window { ... } 객체가 결과로 나온다 this.name 하면 undefinded.. 
```

정확하게 프로그래머가 원하는 객체를 this 가 포인팅 하지 않으면 의도치 않은 결과가 <br>
나올 수 있으니 반드시 유의하도록 한다

예방책으로 쓸 수 있는 방법은 

`use strict` 를 함수 안에 넣어주는 방법이 있다.

```js
function Person(name) {
  'use strict';  // 엄격 모드를 활성화합니다.
  // `undefined`의 속성을 변경하려고 하고 있기 때문에, 에러가 납니다.
  this.name = name;
}

// new 를 빼고 생성자를 '호출'하면 this 는 전역 객체를 포인팅한다 따라서
Person('john'); // TypeError: Cannot set property 'name' of undefined

function person(name) {  // 일반 함수도 마찬가지로 use strict 사용가능
  'use strict'
  this.name = name; 
  }
  
  person('kate') // TypeError: Cannot set property 'name' of undefined
}
```

`Babel과 TypeScript같은 트랜스파일러를 사용하면 항상 엄격 모드로 동작`하고 있다고 생각해도 무방하다




<br>

### 서로 다른 객체, 하나의 메소드로 서로 다른 두 개의 동작 구현하기

```js
function introduce() {
  return `안녕하세요, 제 이름은 ${this.name}입니다.`;
}

const person1 = {    // 객체 1
  name: '윤아준',
  introduce
};

const person2 = {    // 객체2
  name: '신하경',
  introduce
};

person1.introduce(); // 안녕하세요, 제 이름은 운아준입니다.
person2.introduce(); // 안녕하세요, 제 이름은 신하경입니다.
```

`화살표 함수`를 사용하여 introduce() 함수를 정의할 경우 위의 코드처럼 `절대 동작하지 않는다`

(위의 코드처럼 전역 스코프에서 작성된 화살표 함수의) this 는 전역, window 를 가르키게 된다



<br></br>
## <span style="color:#595EFF" id="4"> [This] 4-1. .bind() .apply() .call() 사용해서 this 조정하기 </span>    

함수 객체의 bind 메소드를 호출하면, 메소드의 인수(인스턴스)로 넘겨준 값이 this가 되는 새로운 함수를 반환

`.bind()`

```js
function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
}

const student = {name: 'Mary'};
const printGradeForMary = printGrade.bind(student); // 함수 객체에 bind() 메소드 + 특정 객체 
                                                    // bind 해준 객체로 this 포인팅

printGradeForMary(100); // Mary 님의 점수는 100점입니다.
```

`.call()`

```js
printGrade.call(student, 100); // Mary 님의 점수는 100점입니다.
```

`.apply()`

```js
printGrade.apply(student, [100]); // .apply()의 경우 반드시 배열을 넘겨줘야 한다.
```




<br></br>
## <span style="color:#595EFF" id="5"> [Arrow Function] 5-1. Arrow Fuction ? </span>

화살표 함수는..

- 익명 함수이다. 물론 새로운 변수에 대입하는 방식으로 이름을 부여할 수 있다
  - const func = x=> x+2

- 화살표 함수는 `생성자로 사용될 수 없다`. 
  - prototype 속성을 갖고 있지 않다.

- 화살표 함수는 `스스로의 this, arguments, super`를 가지지 않는다. 
  - 화살표 함수 안에서 this 를 쓸 수 없는 것은 절대 아니다. 
  - this 를 사용하면 `함수 스코프에 존재하는 this` 를 가르킬 뿐이다.
  - this = this

- 화살표 함수 내부에서 `yield 키워드를 사용할 수 없다`.
  - `제너레이터` 로 사용될 수 없다.

- 콜백 함수로 사용될 수 있다
  - const pow = arr.map(x => x + 2)



<br>

### 화살표 함수 정의시 유의할 점

```js
function Person(name) {
  this.name = name;   // 바로 이 name 속성
  this.getName = () => {
    // 여기에서 사용된 `this`는 '함수가 정의된 스코프', 
    // 즉 'Person 함수 스코프'에 존재하는 `this`를 가리킨다.
    return this.name;
  }
}

const mary = new Person('mary');
mary.getName(); // 'mary'
```

생성자 함수 내부에서 정의된 화살표 함수의 경우, <br>
return 값으로 받는 this.name은 Person 생성자를 통해 생성된 객체의 name 속성의 값을 참고한다


<br>


```js
const mary = {
  name: 'mary',
  getName: () => {
    return this.name;
  }
};
// 위의 화살표 함수는 전역 스코프에서 정의 ->`this`는 전역 객체
// `mary`의 메소드로 사용된다고 해도, 전역 객체 즉, window.
// `window.name` = undefined
mary.getName(); // undefined ''
```

this 가 있는 함수 내부에서 선언된 화살표 함수의 this 는 같은 this 를 참조

그외 대부분의 화살표 함수는 객체 메소드로 직접 정의되었다 하더라도 전역 스코프에 속한다


<br>



### 일반 함수의 this, 화살표 함수의 this

일반 함수의 this 는 함수가 `호출`이 될 때 어떻게 호출되는가에 따라 `동적으로 지정`된다.

생성자 함수와 객체의 매소드를 제외한 모든 함수(화살표, 내부, 콜백을 포함) 내부의 this 는 전역 객체를 참조한다





<br></br>
## <span style="color:#595EFF" id="6"> [Arrow Function] 5-2. Arrow function 이 갖는 유용성</span>

화살표 함수의 `this 가 어디를 참고`하는지는 `어떻게 정의되었는지` 에 따라 결정된다

<br>

화살표 함수 => `함수를 다른 함수의 인수로 넘겨야 할 때 사용하자`

```js
function Person(name) {
  this.name = name;
  this.getName = () => {
    return this.name;
  }
}

const mary = new Person('mary');

function printResult(func) {
  console.log(func());
}

// 화살표 함수로 정의된 메소드는 다른 함수의 인수로 넘겨도 아무런 문제가 없습니다!
printResult(mary.getName);   // mary
```



<br></br>
## <span style="color:#595EFF" id="7"> [Arrow Function] 5-3. Arrow function 쓰지 말자</span>

객체의 메소드로 선언할 땐 화살표 함수를 쓰지말자

```js
const person = {
  name: 'john',
  greeting: () => console.log(`hello, ${this.name}.`)  // 객체 안 메소드지만 전역 객체
}

person.greeting()  // hello, undefinded
```

객체의 메소드로 넘길 때는 선언식으로!

```js
const person = {
  name: 'john',
  greeting() {
    console.log(`hello, ${this.name}`)
  }
}

person.greeting()  // hello, john
```


<br>

화살표 함수로 정의된 메소드를 prototype 에 할당하는 경우에도 선언식으로

```js
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

// DO NOT Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi Lee
```


<br>

화살표 함수는 prototype 을 가지지 않는다. 즉, 생성자 함수로 쓰일 수 없다

```js
const Foo = () => {};

console.log(Foo.hasOwnProperty('prototype')); // false
const foo = new Foo(); // TypeError: Foo is not a constructor
```



<br></br>
## <span style="color:#595EFF" id="7"> [Default Parameter] 6-1. 매계변수의 기본값</span>

JS 기본적으로 변수의 초기값을 지정해주지 않으면 `undefined` 으로 지정된다.

```js
function hello(name = 'Mary') {
  console.log(`Hello, ${name}!`);
}

hello('John'); // Hello, John!
hello(); // Hello, Mary!
hello(undefined); // Hello, Mary!
```




<br></br>
# <strong> 3. References </strong>


From web sites ...

- <a href="https://velog.io/@rohkorea86/Promiseis-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%8F%99%EA%B8%B0%EC%97%90%EC%84%9C-Promise%EA%B9%8C%EC%A7%80" target="_blank">Promiseis-비동기동기에서-Promise까지</a>

- <a href="https://poiemaweb.com/es6-arrow-function" target="_blank">화살표 함수 이해하기</a>
From Youtube videos...

- <a href="https://www.youtube.com/watch?v=CA5EDD4Hjz4&list=WL&index=36&t=0s" target="_blank">자바스크립트 promise? 나도 써보자, 기본 개념부터</a>

- <a href="https://www.youtube.com/watch?v=JzXjB6L99N4&t=612s" target="_blank">자바스크립트 async / await? 나도 써보자, 기본 개념부터</a>