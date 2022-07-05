# H-index

</br>

## 문제 설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

## 제한 사항

과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

</br>

## 입출력 예

|    citations    | return |
| :-------------: | :----: |
| [3, 0, 6, 1, 5] |   3    |

</br>

## 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

※ 공지 - 2019년 2월 28일 테스트 케이스가 추가되었습니다.
</br>

### 수도 코드 작성

```js
// h 지수 풀이과정
// 논문의 index와 피인용 횟수를 비교하여 피인용 횟수가 논문의 순번보다
// 작아지기 시작하는 직전의 순번이 연구자의 h-index가 된다.

function solution(citations) {
  let answer = 0;
  // 발표한 논문의 수
  let num = citations.length;

  // 내림차순으로 citations 배열을 먼저 정렬한 뒤, [ 6, 5, 3, 1, 0 ]
  let hIndex = citations.sort((a, b) => b - a);

  // 발표한 논문의 수(num) 만큼 for 문을 돌려서
  for (let i = 0; i < num; i++) {
    // i번째 논문이 (i + 1)회 이상 인용되었는지 확인
    // 1번째 부터 시작하는 index 가 hIndex[i]보다 작거나 같으면
    if (i + 1 <= hIndex[i]) {
      // answer에 ++을 더해준다..
      answer++;
    }
  }
  return answer;
}
```

</br>

### 풀이 코드

```js
function solution(citations) {
  let answer = 0;
  let num = citations.length;

  let hIndex = citations.sort((a, b) => b - a);

  for (let i = 0; i < num; i++) {
    if (i + 1 <= hIndex[i]) {
      answer++;
    }
  }
  return answer;
}
```

### 테스트

```js
테스트 1 〉	통과 (0.20ms, 30.2MB)
테스트 2 〉	통과 (0.29ms, 30.1MB)
테스트 3 〉	통과 (0.32ms, 30.2MB)
테스트 4 〉	통과 (0.24ms, 30MB)
테스트 5 〉	통과 (0.29ms, 29.8MB)
테스트 6 〉	통과 (0.49ms, 30.2MB)
테스트 7 〉	통과 (0.16ms, 29.9MB)
테스트 8 〉	통과 (0.09ms, 30.1MB)
테스트 9 〉	통과 (0.09ms, 30MB)
테스트 10 〉 통과 (0.25ms, 29.9MB)
테스트 11 〉 통과 (0.36ms, 30MB)
테스트 12 〉 통과 (0.09ms, 29.8MB)
테스트 13 〉 통과 (0.34ms, 30MB)
테스트 14 〉 통과 (0.50ms, 30.3MB)
테스트 15 〉 통과 (0.33ms, 30.1MB)
테스트 16 〉 통과 (0.14ms, 30.2MB)
```

### 레퍼런스

- [ 프로그래머스 문제 출처 : H-Index ](https://school.programmers.co.kr/learn/courses/30/lessons/42747)

</br>
