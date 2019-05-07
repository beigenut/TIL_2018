Last edited May 07 2019 
---


## <strong> 1. MAIN TOPIC </strong>

- JS 배열에서 쓸 수 있는 몇 가지 함수 사용 예제 JavaScript Array Methods
- filter 
- map
- forEach
- find
- some
- every
- includes
- FizzBuzz 게임 코드짜기 



<br></br>
## <strong> 2. SUB TOPICS </strong>

### <span style="color:#595EFF"> [JS] 1-1. 배열에 사용할 수 있는 함수 예제  </span>  


초기 배열 객체 선언은 아래라 가정

```js
const items = [
  {name: 'Bike', price: 100},
  {name: 'TV', price: 200},
  {name: 'Radio', price: 30},
  {name: 'Phone', price: 10},
  {name: 'Album', price: 5},
  {name: 'Keyboard', price: 500},
  {name: 'Book', price: 1000}
]
```

1. filter()     ->  반환 타입 Array

```js
const filteredItems = items.filter((item) => {
  return item.price <= 100
})

console.log(filteredItems)
```

결과

```
[ { name: 'Bike', price: 100 },
  { name: 'Radio', price: 30 },
  { name: 'Phone', price: 10 },
  { name: 'Album', price: 5 } ]
```


filter() 의 장점은 `초기 선언 배열 값의 어떠한 변경도 주지 않는다`. <br>
임시적으로 필터된 값만 불러올 때 유용하게 사용할 수 있음.


```js
console.log(items)
```

결과 

```
[ { name: 'Bike', price: 100 },
  { name: 'TV', price: 200 },
  { name: 'Radio', price: 30 },
  { name: 'Phone', price: 10 },
  { name: 'Album', price: 5 },
  { name: 'Keyboard', price: 500 },
  { name: 'Book', price: 1000 } ]
```


<br>
2. map()    ->  반환 타입 array

배열 `객체의 특정 요소를 추출`하고자 할 때 유용하게 쓸 수 있다.

```js
const itemNames = items.map((item) => {
  return item.name
})

console.log(itemNames)
```

결과 

```
[ 'Bike', 'TV', 'Radio', 'Phone', 'Album', 'Keyboard', 'Book' ]
```

map() 함수는 반드시 배열을 반환한다.

이때 반환된 배열의 특정 값들을 호출하고 싶다면 forEach() 사용한다



<br>
3. forEach()      ->  반환 타입 값/object

```js
items.forEach((item) => {
  console.log(item.name)
})
```

결과

```
Bike
TV
Radio
Phone
Album
Keyboard
Book
```

for 문을 돌리면서 하나씩 추출할 수 도 있지만, 코드가 훨씬 간결해진다.



<br>
4. find()   ->  반환 타입 object/값 

특정 값이 들어있는 (이 예제에서는) 객체를 추출한다.

```js
const foundItem = items.find((item) => {
  return item.price === 500
})

console.log(foundItem)
```

결과

```
{ name: 'Keyboard', price: 500 }
```

단, find() 함수와 filter() 함수의 차이점을 보면 만약 동일한 값을 갖는 객체가 다수 존재할 경우 <br>
find() 함수를 사용했을 때 얻을 예상과 결과가 달라질 수 있다.

초기 객체에 변화를 주어 

```js
const items = [
  { name: 'Keyboard', price: 500 },
  { name: 'Book', price: 500 } ]

  const foundItem = items.find((item) => {
  return item.price === 500
})

console.log(foundItem)
```

를 적용하여 결과를 얻으면

```
{ name: 'Keyboard', price: 500 }
```

만 도출된다. Book 에 대한 객체는 함께 반환되지 않는다. 배열 안에서 첫번째로 조건에 충족하는 값만 즉시 return 한다.



<br>
5. some()   ->  반환 타입 true/false

배열 안에서 특정 조건을 만족하는 값이 `하나라도 있는지 없는지 알고 싶을 때` 사용한다.

```js
const hasInexpensiveItems = items.some((item) => {
  return item.price <= 100
})

console.log(hasInexpensiveItems)
```

result 

```
true
```


<br>
6. every()    ->  반환 타입 true/false

배열 안의 값들이 특정 조건을 `모두 만족하는지 않은지 알고 싶을 때` 사용한다.

```js
const hasInexpensiveItems = items.every((item) => {
  return item.price <= 100
})

console.log(hasInexpensiveItems)
```

result 

```
false
```


<br>
7. reduce()     ->  반환 타입 값

배열 안에 들어 있는 값들의 `총 합(누적)을 알고 싶을 때` 사용한다.

```js
// reduce((누적에 사용될 파라미터, 아이템) => {}, 누적초기값 0) 선언 순서에 유의
const total = items.reduce((current, item) => {
  return item.price + current
}, 0)

console.log(total)
```

result 

```
1845
```


<br>
8. includes()     ->  반환 타입 true/false

배열안에 특정 값과 같은 값이 포함되어 있는지 알고 싶을 때

```js
const items = [1, 2, 4, 6, 9, 'cat', {name: 'dog', age: 10}]

console.log(items.includes(2))
console.log(items.includes('cat'))
console.log(items.includes('dog'))
console.log(items.includes(3))
```

result 

```
true
true
false
false
```

> console.log(items.includes('dog')) -> items.name 'dog' 포함여부를 알고 싶다면 some() 을 사용할 것




<br></br>
### <span style="color:#595EFF"> [JS] 2-1. FizzBuzz 게임 코드  </span>  

map() 함수 이용

```js   
let arr = [];
let newArr = [];
for(let i = 1 ; i < 101; i++ ) { arr.push(i) }

arr.map(item => {
  if(item % 3 === 0 && item % 5 === 0) {
    newArr.push('fizzbuzz')
  } else if(item % 3 === 0 ) {
    newArr.push('fizz')
  } else if(item % 5 === 0 ) {
    newArr.push('buzz')
  } else {
    newArr.push(item)
  }
})

newArr.forEach(item => {
  console.log(item)
})
```




<br></br>
## <strong> 3. REFERENCES </strong>


1. includes() 함수 MDN
  - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/includes


<br></br>

___
___