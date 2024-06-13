---
title: "[항해99 취업 리부트 코스 학습일지][day20] 어제보단 나은 하루"
excerpt: ""
categories:
  - TIL
tags:
  - 개발자포트폴리오
  - 개발자이력서
  - 개발자취업
  - 개발자취준
  - 코딩테스트
  - 항해99
  - 취리코
  - 취업리부트코스
toc: true
toc_sticky: true
toc_label: "목차"
toc_icon: "edit"
# classes: wide
header:
  teaser: /assets/images/hanghae99-teaser.png
---
## 📍TIL
### 새로 배운 내용
- math 라이브러리 -> 한 번 쫙~ 훑어봐야겠다..!!
	- comb(), perm(), factorial()
	- 추가로, 파이썬 [주요 함수들의 시간복잡도](https://ics.uci.edu/~pattis/ICS-33/lectures/complexitypython.txt) 
- 조합 개수 구하는 공식 (이항계수) -> 몰라도 되는걸까?

#### 입력값 템플릿
백준 문제를 풀면서 입력값 처리하는게 은근 스트레스였다.<br>
그러다 다른 조원분의 코드를 보다가 깜짝 놀랐다. 이 분은 입력값을 함수로 빼서 일관되게 문제를 풀고 계셨다..!!

```python
import sys
from collections import deque

input = sys.stdin.readline


# 입력 받기
def get_input():
    params = []

    T = int(input())

    for _ in range(T):
        param = []
        for _ in range(2):
            param.append(list(map(int, input().strip().split())))

        params.append(param)
    return params


def solution(params):
    # 로직 작성...
    answer = []
    #..... 
    return answer


print("\n".join(str(x) for x in solution(get_input())))
```
좋은건지는 모르겠지만 일단 신선한 충격..!! <br>
이번에 코드를 풀면서 나도 적용해봤다.ㅋㅋ 내일 JW님한테 참고했다고, 고맙다고 말씀드려야겠다...!!!!

### 생각
- 조원분들의 코드를 볼때마다 정말정말 감탄하고 많이 배운다! 흐름이 비슷해도 디테일도 다 달라서 지문같기도 하고 보는 재미가 있다. 좋은 코드는 잘 배우고 따라해서 습득해야지!
- 팀 코드 선정하는데 이유를 작성하기로 했다. 이유를 작성하려고 하니, 내가 왜 이 코드를 좋은 코드로 추천하는지 생각해보면서 점점 나만의 좋은 코드에 대한 기준이 서는 것 같다. 한 눈에 코드 흐름이 잘 읽힌다는지, 라이브러리를 적절하게 사용했다던지, 참신한 로직을 썼다던지 등등

### 🥰 오늘의 잘한 일
- 조원분들이 추천한 스벅이 레몬 블렌디드를 마셔봤다! 원래 신 거를 잘 못 먹는데 왠열! 상큼하니 맛있잖아~!! 역시 조원분들 초이스는 믿음직해. 짱짱. 믿음으로 시키길(?!) 잘했다ㅋㅋ
- 문제를 어떻게 접근해야될지 모르겠거나, 어떻게 구현해야할지 잘 모르겠는 상황에서 블로그를 참고하는데 오늘은 전체 코드를 보지않고 **접근한 방식만 참고** 하고 코드는 내가 직접 풀어보았다.
- 기술 매니저님께 물어볼 질문.. 을 열심히 생각해서 부끄럽지만 적어 보았다. 용기있는 행동이었다...히히
- 항해 시간 끝나고도 바로 개발남노씨 무료 특강이 갑자기 있길래 부랴부랴 신청해서 시간복잡도에 대한 강의를 들었다. 대부분 아는 내용이긴 했지만 복습하고, 선생님과 다른 분들과도 교류하는 시간이었어서 너무 좋았다.

### 💪 오늘의 아쉬운 일 & Action Plan
- 문제를 더 풀 시간도 있었고 체력도 있었는데 갑자기 늘어져서 딴 짓을 하게 되었다. ➡️ 최대 15분만 늘어지고 그 담엔 끊고 일어나기! 해답을 보고 풀더라도 일단 컴터 앞에 앉자!
<br>
<br>
<br>

<p>
  <p style="color:grey">항해99 취업 리부트 코스를 수강하고 작성한 콘텐츠 입니다.</p>
  <a href="https://hanghae99.spartacodingclub.kr/reboot" target="_blank" class="img-link">
    <img src="https://github.com/grey920/grey920.github.io/assets/58028215/84b7ba76-a278-4b8c-a8af-0b0ca7da095b" alt="항해99 - 온라인 코딩 부트캠프 항해99" loading="lazy">
  </a>
</p>