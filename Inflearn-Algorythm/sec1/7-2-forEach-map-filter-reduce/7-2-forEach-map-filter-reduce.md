# forEach, map, filter, reduce

## forEach

> for 반복문 대신 사용하는 메소드

### forEach의 함수형 예시

- 아래는 forEach 메소드가 어떻게 작동하는지에 대해서 함수를 이용해 설명한 예시이다.

```js
function forEach(predicate, thisArg) {
  for (let i = 0; i < a.length; i++) {
    predicate(a[i], i); // 첫 번째 인자는 arr의 [i]번째 값, 두 번째 인자는 index의 i 이다.
  }
}
```

- forEach 함수 (함수(필수), 콜백함수 내부에서 전달받을 인자값(생략가능))

```js
a = [10, 11, 12, 13, 14, 15];
a.forEach(function(v, i));
```

- forEach 함수 내부에서 실행되는 것은 forEach가 아니라, forEach 함수에서 실행하는 콜백 함수의 내부이다.

### forEach의 일반적인 형태

```js
a = [10, 11, 12, 13, 14, 15];
a.forEach(function (v, i) {
  // 콜백함수
  // 콜백 함수의 첫 번째 인자인 v는 arr의 [i]번째 값, 두 번째 인자인 i는 index의 i 이다.
  console.log(v, i);
  /**
   * 10, 0
   * 11, 1
   * 12, 2
   * 13, 3
   * 14, 4
   * 15, 5
   */
});
```

- forEach는 배열 요소 하나하나를 탐색하면서, 탐색 할 때마다 콜백 함수를 호출한다.

### 📌 forEach 메소드의 Point

```js
a = [10, 11, 12, 13, 14, 15];
a.forEach(function (v, i) {
  console.log(v, i);
});
```

- `forEach` 메소드에서 잊지 말아야할 사실은 `forEach`가 실행하고 있는 함수가 `forEach`의 내부가 아니라는 것이다.

```js
function (v, i) {
  console.log(v, i);
}
```

- `forEach()`가 호출하는 것은 콜백 함수이지, `forEach()`의 내부 그 자체가 아니다! 위의 코드는 `forEach()` 함수에 첫 번째 인자로 넘기는 콜백 함수일 뿐이다!

```js
a = [10, 11, 12, 13, 14, 15];
a.forEach(
  function (v, i) {
    console.log(v, i);
  },
  [1, 2]
);
```

- 만약 콜백 함수 뒤에 두 번째 인자로 배열([1, 2])를 넘겨준다는 건 무슨 의미일까? `forEach()` 함수에 두 번째 인자로 넘기는 index 번호가 된다는 뜻이다.

```js
a = [10, 11, 12, 13, 14, 15];
a.forEach(
  function (v, i) {
    console.log(v, i, this);
  },
  [1, 2]
);
```

- console.log에 `this`를 추가하여 출력해보면

![image](https://user-images.githubusercontent.com/53133662/174542435-2135d23d-0d62-44c7-91b8-a4a620e1b72f.png)

- this가 어떻게 출력되고 있는지 확인할 수 있다.

</br>

## map

> map은 원본 배열을 탐색하고 원본 배열의 요소들을 이용해서 '새로운 배열'을 생성해준다.

### map의 함수형 예시

- 아래는 map 메소드가 어떻게 작동하는지에 대해서 함수를 이용해 설명한 예시이다.

```js
function map(predicate, thisArg) {
  let list = []; // => 새로운 배열을 생성해서 넣어야 하니까 빈 배열을 생성해준다.
  for (let i = 0; i < a.length; i++) {
    // for 문을 통해 전달받은 배열 arr 요소들을 하나씩 돌면서 새로운 배열 안에 push 한다.
    list.push(predicate(a[i], i)); //  predicate(a[i], i); // 첫 번째 인자는 arr의 [i]번째 값, 두 번째 인자는 index의 i 이다.
  }
  return list;
}
```

- `map`에서 실행하는 콜백 함수 내부를 살펴보자. (이것은 `map` 내부가 아니라는 것을 명심하자.)

### map의 일반적인 형태 1

```js
let a = [10, 11, 12, 13, 14, 15];
let answer = a.map(
  function (v, i) {
    return v * v; // [100, 121, 144, 169, 196, 225]
  },
  [1, 2]
);
console.log(answer);
```

- `map`에서 호출하는 콜백 함수(`predicate`) 내부에서 매개변수로 전달 받은 `v`와 `i`를 (`predicate(a[i], i)`) 이용해서 실행 되고 있음을 알 수 있다.

### map의 일반적인 형태 2

```js
let answer = a.map(
  function (v, i) {
    if (v % 2 === 0) return v; //  [10, undefined, 12, undefined, 14, undefined]
  },
  [1, 2]
);

let a = [10, 11, 12, 13, 14, 15];
console.log(answer); // => [10, undefined, 12, undefined, 14, undefined]
```

- `map`은 새로운 배열을 생성할지라도, "원본 배열과 새로운 배열의 길이는 동일"하기 때문에, '짝수에 해당되지 않는 값'은 그냥 undefined로 return 된다.

</br>

### filter

> 새로운 배열을 생성해서 Return 받는다. 원본 배열에 있는 요소들 중에서 특정 값들만 filtering 하는 것을 의미.

### filter의 함수형 예시

- 아래는 filter 메소드가 어떻게 작동하는지에 대해서 함수를 이용해 설명한 예시이다.

```js
function filter(predicate, thisArg) {
  let list = []; // => 새로운 배열을 생성해서 넣어야 하니까 빈 배열을 생성해준다. (map과 동일)
  for (let i = 0; i < a.length; i++) {
    if ((predicatea[i], i)) {
      // 조건을 걸어주고,
      list.push(predicate(a[i])); // 해당 조건에 일치하는 값(true 일 때)만 새로운 배열에 push 해준다.
    }
  }
  return list;
}
```

### filter의 일반적인 형태

```js
let answer = a.filter(
  // 콜백 함수
  function (v, i) {
    if (v % 2 === 0) return v; // [10, 12, 14]
  },
  [1, 2]
);

let a = [10, 11, 12, 13, 14, 15];
console.log(answer); // => [10, 12, 14]
```

- 원본 배열의 길이와 상관없이 filter에 해당되는 조건식에 맞는 값만 return 해준다.
- '짝수에 해당되지 않는 값'은 새로운 answer 배열 값에 저장되지 않는다.

</br>

### 📌 map 과 filter 의 차이점

- ⚡️ `map`은 원본 "배열과 길이를 동일"하게 새로운 배열로 만들어서 return 한다.
- ⚡️ `filter`는 "원본 배열과 길이가 동일하지 않아도 되며", 원본 배열의 요소들 중 특정 값들만 필터링해서 "새로운 배열"로 만들어 return 한다.

</br>

### reduce

> reduce 는 원본 배열의 요소를 이용해서 새로운 값을 return 한다. reduce 는 map, filter처럼 배열을 새로 생성하지 않는다. 배열이 아니라, 어떤 값을 생성해서 리턴한다.

### reduce의 함수형 예시

- 아래는 reduce 메소드가 어떻게 작동하는지에 대해서 함수를 이용해 설명한 예시이다.

```js
function reduce(predicate, value) {
  let result = value; // value 값으로 초기화
  for (let i = 0; i < a.length; i++) {
    result = predicate(result, a[i]); //
  }
  return result;
}
```

- `predicate` 에서 값을 넘겨줄 때 첫 번째 인자로 결과 값(`result`)을 넘겨주고, 두 번째 인자로는 원본 배열 요소(`a[i]`)를 전달한다.

### reduce의 일반적인 형태

```js
let a = [10, 11, 12, 13, 14, 15];
let answer = a.reduce(function (acc, v) {
  // acc 는 누적 값, v 는 원본 배열의 요소
  return acc + v; // => 75
}, 0);

console.log(answer); // => 75
```

- `reduce`에서 호출하는 함수의 첫 번째 인자는 콜백 함수이고, 두 번째는 초기화하는 초기 값이다.

```js
function (acc, v) {
  return acc + v;
}
```

- 콜백 함수를 살펴보면, 첫 번째로 받는 인자(`acc`)는 누적 값이고, 두 번째로 받는 인자(`v`)는 원본 배열의 요소이다.

### 📌 reduce 메소드의 Point

- `reduce` 는 `map`이나 `filter`처럼 배열을 생성하는 것이 아니라 "결과 값을 생성"해서 return 한다.
- 보통 `reduce`는 원본 배열 요소의 누적 값(합)을 구할 때 사용하게 된다.

</br>

## forEach, map, filter, reduce 비교

### forEach

```js
let answer = a.forEach(function (iOfA, index) {
  console.log(`forEach : ${iOfA}, ${index}`);
});
```

#### forEach 의 결과값

```js
10 0 // => a의 요소 i, index 번호
11 1 // => a의 요소 i, index 번호
12 2 // => a의 요소 i, index 번호
13 3 // => a의 요소 i, index 번호
14 4 // => a의 요소 i, index 번호
15 5 // => a의 요소 i, index 번호
```

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

- 첫번째로 a 라는 배열을 reduce를 사용해서 반복하여 돌면 콜백함수가 돌면서
  acc 는 0(초기값) 일 테고, value는 원본 배열 a의 첫번째 값인 10(a[0])일 것이다. => 값 10
- 두번째로 a 라는 배열을 reduce를 사용해서 반복하여 돌면 콜백함수가 돌면서 acc 는 10(처음 돌면서 얻은 값)일 테고, value는 원본 배열 a의 첫번째 값인 11(a[1])일 것이다. => 값 21
- 이렇게 원본 배열의 요소의 갯수만큼 반복하여 돌아서 acc + value 한 새로운 값을 return 한다.
- 최종적으로 나온 값은 75이 된다.
- 결과적으로 원본 배열의 요소들을 전부 더한 값(acc + value)이 리턴된다고 보면 된다.
- acc 는 누적값, value 는 원본 배열의 요소
- 보통 reduce는 원본배열의 합을 구할 때 사용한다.

</br>
