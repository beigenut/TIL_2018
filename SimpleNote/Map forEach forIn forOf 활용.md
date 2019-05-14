- - -
# May 14 2019 
---


## <strong> 1. MAIN TOPIC </strong>

객체에서 원하는 속성 정보만 담겨있는 새로운 배열을 만들기

- [Map](#1)

- [forEach](#2)

- [for..in](#3)

- [for..of](#4)

- [find 와 filter 차이](#5)
  - find 함수 활용 예제



<br></br>
# <strong> 2. Sub Topics </strong>

```js
const items = [
  {name:"car", price: 200},
  {name:"book", price: 300},
  {name:"computer", price: 500},
  {name:"house", price: 1300}
]
```
를 활용하여 items.name 만 들어있는 새로운 배열을 반환하자 

<br>

## <span style="color:#595EFF" id="1"> [map] 1-1. map 메소드 </span>    

메소드 사용 목적 : 

객체 안에서 원하는 객체 속성만 뽑아서 새로운 배열을 반환하고 싶다

```js
let arr_map = items.map(i => {
  return i.name     // for 문 돌리면서 push 해줄 필요 없음
})

console.log(arr_map)   // ["car", "book", "computer", "house"]
```

map() 메소드는 자동으로 배열을 반환한다. 

유의, return 지정하지 않으면 undefined 배열이 반환된다.





<br></br>
## <span style="color:#595EFF" id="2"> [forEach] 1-2. forEach </span>     

forEach 를 사용할 경우,

```js
let arr_forEach = [];

items.forEach(i => {
  arr_forEach.push(i.name)
})

console.log(arr_forEach)
```




<br></br>
## <span style="color:#595EFF" id="3"> [for..in] 1-3. for...in </span> 

```js
let arr_forIn = [];

for(i in items){    // for ... in 는 인덱스를 
  arr_forIn.push(items[i].name)
}

console.log(arr_forIn)
```


<br></br>
## <span style="color:#595EFF" id="4"> [for..of] 1-4. for...of </span> 

```js
let arr_forOf = [];

for(i of items){    // for ... of 배열의 값을
  arr_forOf.push(i.name)
}

console.log(arr_forOf)
```



<br></br>
## <span style="color:#595EFF" id="5"> [find / filter] 1-4. find 함수 예제 </span> 

[배열에 사용할 수 있는 여러 매소드](https://github.com/beigenut/todayILearned/blob/master/SimpleNote/Array%20method%20functions%20-%20map%20forEach%20filter%20etc.md)

이전 마크다운에서 다뤘듯이 find() 메소드의 경우, 

조건을 충족하는 하나 이상의 값이 있더라도 가장 첫번째로 만족하는 값만 반환하는 반면에

filter() 메소드의 경우 조건을 만족하는 다수의 값들을 모두 반환시킨다는 것이 다름.

<br>

find() 메소드를 활용하면 어떤 조건을 만족하는 결과가 있는지/없는지 단순 사실만

알고 싶을 때 사용하면 유용할 것 이다.


```js
let isTrue = items.find(i => {
  return i.price > 1000
})

isTrue ? console.log("yes") : console.log("no")    // yes
```




<br></br>
# <strong> 3. References </strong>

