- - - 
## May 10 2019  

____


# <strong> 1. Main Topic </strong>

- This

- 함수와 메소드 

- '객체'라 칭하는 범위

- This .bind() .call()

- Arrow function 

- Arrow function 이 갖는 유용성




<br></br>
# <strong> 2. Sub Topics </strong>

<!-- *********************첫번째 제목********************** -->
## <span style="color:#595EFF"> [This] 1-1. This 의 정의 This 가 가르키는 것 </span>    


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




<br>


### 함수와 메소드 차이?

자바 스크립트에서...

- 함수 : 기능
  - Global/Local 에 무관하게 독립적으로 정의되는 !객체! 선언되고 호출(invoked)되어 사용된다
  - ex) myFunction();

- 메소드 : 방법
  - 객체의 property 로 function 인 것
  - ex) obj.otherFunction();
  - ex) myFunction.bind(obj)





<br>


### 객체 포함 범위

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



<br>


### .bind() .apply() .call() 사용해서 this 조정하기

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
<!-- ***********************두번째 제목******************** -->
## <span style="color:#595EFF"> [Arrow Function] 2-1. Arrow Fuction ? </span>





<br></br>
<!-- ***********************세번째 제목******************** -->
## <span style="color:#595EFF"> [Async/Await] 3-1. Async/Await </span>





<br></br>
# <strong> 3. References </strong>


From web sites ...

- <a href="https://velog.io/@rohkorea86/Promiseis-%EB%B9%84%EB%8F%99%EA%B8%B0%EB%8F%99%EA%B8%B0%EC%97%90%EC%84%9C-Promise%EA%B9%8C%EC%A7%80" target="_blank">Promiseis-비동기동기에서-Promise까지</a>


From Youtube videos...

- <a href="https://www.youtube.com/watch?v=CA5EDD4Hjz4&list=WL&index=36&t=0s" target="_blank">자바스크립트 promise? 나도 써보자, 기본 개념부터</a>

- <a href="https://www.youtube.com/watch?v=JzXjB6L99N4&t=612s" target="_blank">자바스크립트 async / await? 나도 써보자, 기본 개념부터</a>