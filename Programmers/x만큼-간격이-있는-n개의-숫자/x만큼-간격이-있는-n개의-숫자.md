# x만큼 간격이 있는 n개의 숫자

</br>

## 문제 설명

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

</br>

## 제한 사항

x는 -10000000 이상, 10000000 이하인 정수입니다.
n은 1000 이하인 자연수입니다.
</br>

## 입출력 예

|  x  |  n  |    answer    |
| :-: | :-: | :----------: |
|  2  |  5  | [2,4,6,8,10] |
|  4  |  3  |   [4,8,12]   |
| -4  |  2  |   [-4, -8]   |

</br>

### 풀이 코드

```js
function solution(x, n) {
  let answer = Array(n)
    .fill(1)
    .map((item, i) => item * (x * (i + 1)));
  return answer;
}
```

### 테스트

```js
테스트 1 〉	통과 (0.05ms, 33.4MB)
테스트 2 〉	통과 (0.05ms, 33.4MB)
테스트 3 〉	통과 (0.06ms, 33.5MB)
테스트 4 〉	통과 (0.07ms, 33.5MB)
테스트 5 〉	통과 (0.06ms, 33.5MB)
테스트 6 〉	통과 (0.04ms, 33.4MB)
테스트 7 〉	통과 (0.09ms, 33.6MB)
테스트 8 〉	통과 (0.06ms, 33.4MB)
테스트 9 〉	통과 (0.09ms, 33.5MB)
테스트 10 〉	통과 (0.04ms, 33.5MB)
테스트 11 〉	통과 (0.08ms, 33.5MB)
테스트 12 〉	통과 (0.07ms, 33.5MB)
테스트 13 〉	통과 (0.11ms, 33.7MB)
테스트 14 〉	통과 (0.11ms, 33.8MB)
```

</br>

### 레퍼런스

- [ MDN 참조 : Array.prototype.fill() ](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)
- [ 프로그래머스 문제 출처 : x만큼 간격이 있는 n개의 숫자 ](https://school.programmers.co.kr/learn/courses/30/lessons/12954)

</br>
