# forEach, map, filter, reduce

## forEach

> for 반복문 대신 사용하는 메소드

### forEach의 함수형 예시

```js
function forEach(predicate, thisArg) {
  for (let i = 0; i < a.length; i++) {
    predicate(a[i], i);
  }
}
let a = [10, 11, 12, 13, 14, 15];
```

- forEach 함수 (함수(필수), 콜백함수 내부에서 전달받을 인자값(생략가능))
- forEach 함수 안에서 실행되는 것은 forEach가 아니라, forEach 함수에서 실행하는 콜백 함수의 내부이다.

</br>

## map

> map은 원본 배열을 탐색하고 원본 배열의 요소들을 이용해서 '새로운 배열'을 생성해준다.

### map의 함수형 예시

```js
 function map (predicate, thisArg) {
  let list = []; => 새로운 배열을 생성해서 넣어야 하니까 빈 배열을 생성해준다.
  for (let i = 0; i < a.length; i++) {
    list.push(predicate(a[i], i))
  }
  return list;
}
```

### map의 일반적인 형태

```js
let answer = a.map(function (v, i) {
  if(v%2 === 0) return v;
}, [1, 2])

let a = [10, 11, 12, 13, 14, 15];
console.log(answer) => [10, undefined, 12, undefined, 14, undefined]
```

- 새로운 배열을 생성할지라도, 원본 배열과 새로운 배열의 길이는 동일하기 때문에, '짝수에 해당되지 않는 값'은 그냥 undefined로 return 된다.

</br>

### filter

> 새로운 배열을 생성해서 Return 받는다. 원본 배열에 있는 요소들 중에서 특정 값들만 filtering 하는 것을 의미.

### filter의 함수형 예시 1

```js
       function filter (predicate, thisArg) {
          let list = []; => 새로운 배열을 생성해서 넣어야 하니까 빈 배열을 생성해준다. (map과 동일)
          for (let i = 0; i < a.length; i++) {
            if(predicatea[i], i) {
              list.push(predicate(a[i]))
            }
          }
          return list;
        }
```

### filter의 일반적인 형태

```js
        let answer = a.filter(function (v, i) {
          if (v%2 === 0) return v;
        }, [1, 2]);

        let a = [10, 11, 12, 13, 14, 15];
        console.log(answer) => [10, 12, 14]
```

- 원본 배열의 길이와 상관없이 filter에 해당되는 조건식에 맞는 값만 return 해준다.
- '짝수에 해당되지 않는 값'은 새로운 answer 배열 값에 저장되지 않는다.

</br>

### map 과 filter 의 차이점

- map은 원본 배열과 길이를 동일하게 새로운 배열로 만들어서 return 한다.
- filter는 원본 배열과 길이가 동일하지 않아도 되며, 원본 배열의 요소들 중 특정 값들만 필터링해서 새로운 배열로 만들어 return 한다.

</br>

### reduce

> reduce 는 원본 배열의 요소를 이용해서 새로운 값을 return 한다. reduce 는 map, filter처럼 배열을 새로 생성하지 않는다. 배열이 아니라, 어떤 값을 생성해서 리턴한다.

### reduce의 함수형 예시

```js
function reduce(acc, value) {
  let result = value; // value 값으로 초기화
  for (let i = 0; i < a.length; i++) {
    result = acc(result, a[i]);
  }
  return result;
}
```

### reduce의 일반적인 형태

```js
       let answer = a.reduce(function (acc, v) {
         return v%2 === 1; => 홀수만 구하는 조건식
       }, 0);
       console.log(answer);


      let a = [10, 11, 12, 13, 14, 15];

```

</br>

## forEach, map, filter, reduce 비교

### forEach

```js
let answer = a.forEach(function (iOfA, index) {
  console.log(`forEach : ${iOfA}, ${index}`);
});
```

#### forEach 의 결과값

10 0 => a의 요소 i, index 번호
11 1 => a의 요소 i, index 번호
12 2 => a의 요소 i, index 번호
13 3 => a의 요소 i, index 번호
14 4 => a의 요소 i, index 번호
15 5 => a의 요소 i, index 번호

</br>

### map

```js
let answer1 = a.map(
  function (iOfA, index) {
    return iOfA * iOfA;
  },
  [1, 2]
);
```

#### map 결과값

```js
(6)[(100, 121, 144, 169, 196, 225)];
```

</br>

### filter

```js
let answer2 = a.filter(
  function (iOfA, index) {
    return iOfA % 2 === 0; // 짝수 일 때만
    // true or false 중에 리턴 => 'true' 일때만 return
  },
  [1, 2]
);
```

#### filter 결과값

```js
(3)[(10, 12, 14)];
```

</br>

### reduce

> 누적값을 구하고자 할 때 사용한다. 때때로 최소값이나 최대값을 구할 때도 사용

```js
let answer3 = a.reduce(function (acc, value) {
  return acc + value;
}, 0); // 0은 두번째 인자인 value 값을 초기화하는 역할을 해준다.
```

#### reduce 결과값

```js
75;
```

#### reduce 정리

첫번째로 a 라는 배열을 reduce를 사용해서 반복하여 돌면 콜백함수가 돌면서
acc 는 0(초기값) 일 테고, value는 원본 배열 a의 첫번째 값인 10(a[0])일 것이다. => 값 10
두번째로 a 라는 배열을 reduce를 사용해서 반복하여 돌면 콜백함수가 돌면서
acc 는 10(처음 돌면서 얻은 값)일 테고, value는 원본 배열 a의 첫번째 값인 11(a[1])일 것이다. => 값 21
이렇게 원본 배열의 요소의 갯수만큼 반복하여 돌아서 acc + value 한 새로운 값을 return 한다.
최종적으로 나온 값은 75이 된다.
결과적으로 원본 배열의 요소들을 전부 더한 값(acc + value)이 리턴된다고 보면 된다.
acc 는 누적값, value 는 원본 배열의 요소
보통 reduce는 원본배열의 합을 구할 때 사용한다.

</br>