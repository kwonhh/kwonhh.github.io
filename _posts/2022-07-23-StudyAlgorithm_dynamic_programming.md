---
title: 알고리즘 공부_다이나믹프로그래밍
author: HH KWON
date: 2022-07-23
category: Jekyll
layout: post
---

# BOJ15989
[문제링크](https://www.acmicpc.net/problem/15989 "문제 링크")<br>
<img src="../gitbook/images/c15989.png" width="1200" height="700"><br>
접근한 방법<br>
1. 문제에서 주어진 숫자를 각각 1로 시작하는 수의 조합, 2로 시작하는 수의 조합, 3으로 시작하는 수의 조합으로 분류
2. 위 표와 같이 1로 시작하는 숫자의 경우 바로 *1번 이전의 숫자*의 *1로 만들 수 있는 숫자 조합*에 1을 추가한 것이기 때문에 1로 시작하는 숫자의 경우의 수는 어떤 수든 1
3. 2로 시작하는 숫자의 경우 현재 숫자의 2번 이전의 숫자에 2를 더한 것으로 생각할 수 있는데, 이때 위 표에서 2로 시작하는 수의 조합과 3으로 시작하는 수의 조합이 겹치는 것을 볼 수 있음.(빨간색으로 표시된 부분)<br>
   문제에서는 같은 수로 구성되어 있고 순서만 다른 경우를 같은 경우로 본다고 했기 때문에 중복된 것을 빼줘야 하는데<br>
   이때, 2로 시작하는 숫자는 2번 이전의 숫자의 dp 중에서 1로 시작하는 숫자, 2로 시작하는 숫자의 경우만 더해주어야 중복을 피할 수 있음.
4. 즉, 1로 시작하는 숫자의 조합은 dp[n-1] 값들 중 1로 시작하는 숫자의 경우의 수만 더해주고, 2로 시작하는 숫자는 dp[n-2]의 1, 2로 시작하는 숫자, 3으로 시작하는 숫자는 dp[n-3]의 1, 2, 3으로 시작하는 숫자의 경우의 수만 더해주어야 중복을 피할 수 있음.<br>
   -> i(1<= i <= 3)로 시작하는 숫자를 만들기 위해서는 dp[n-i]의 값 중 i이하의 숫자로 만들 수 있는 경우의 수 합을 구해준다.
5. 문제에서 n은 1만 이하의 숫자라고 했으므로 dp를 [0, 0, 0, 0] * 10001개 만들어주고, dp[n][i]를 n을 i로 시작하는 숫자로 만들 수 있는 경우의 수로 정의
6. 또한, 시간초과를 막기 위해서 입력 n이 이미 계산된 dp값이라면 바로 출력하도록 tmp 변수에 n의 최대값을 저장하도록 함.<br><br>
## 정답 코드

```python
# https://www.acmicpc.net/problem/15989
def solution(n):
    for nn in range(tmp+1, n+1):
        if nn == 1:
            dp[1][1] = 1
            continue
        if nn == 2:
            dp[2][1] = 1
            dp[2][2] = 1
            continue
        if nn == 3:
            dp[3][1] = 1
            dp[3][2] = 1
            dp[3][3] = 1
            continue
        dp[nn][1] = dp[nn-1][1]
        dp[nn][2] = dp[nn-2][1] + dp[nn-2][2]
        dp[nn][3] = dp[nn-3][1] + dp[nn-3][2] + dp[nn-3][3]
    return sum(dp[n])

T = int(input().rstrip())
tmp = 0
dp = [[0, 0, 0, 0] for _ in range(10000+1)]
for _ in range(T):
    n = int(input().rstrip())

    if n > tmp:
        print(solution(n))
    else:
        print(sum(dp[n]))
    tmp = max(n, tmp)
```

<img src="../gitbook/images/c15989.JPG" width="700" height="80"><br><br>