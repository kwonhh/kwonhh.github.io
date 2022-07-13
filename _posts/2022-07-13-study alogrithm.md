---
title: How to Generate TOC
author: Tao He
date: 2019-04-28
category: Jekyll
layout: post
---

The jekyll-gitbook theme leverages [jekyll-toc][1] to generate the *Contents* for the page.
The TOC feature is not enabled by default. To use the TOC feature, modify the TOC
configuration in `_config.yml`:

```yaml
toc:
    enabled: true
```

프로그래머스 Lv3 단어 변환
-------------

```python
def solution(begin, target, words):
    answer = 0
    stack = [begin]
    visit = []
    while len(stack) != 0:
        tmp = stack.pop()
        if tmp == target:
            break
        answer += 1
        for w in words:
            for l in range(len(tmp)):
                if w[:l] + w[l+1:] == tmp[:l] + tmp[l+1:]:
                    if w not in visit:
                        visit.append(w)
                        stack.append(w)
    if tmp == target:
        return answer
    else:
        return 0
```

파이썬 Lv2 타겟넘버
-------------

```python
def solution(numbers, target):
    answer = 0
    graph = []
    num = len(numbers)
    for n in range(num):
        if n == 0:
            tmp = []
            tmp.append(numbers[0])
            tmp.append(numbers[0] * (-1))
            graph.append(tmp)
            continue
        order = []
        for gg in graph[n - 1]:
            order.append(gg + numbers[n])
            order.append(gg - numbers[n])
        graph.append(order)
    # print(graph)
    for a in graph[-1]:
        if a == target:
            answer += 1

    return answer
```

Why this repo3
-------------

long contents .....

1. e
2. f
3. g
4. h

Why this repo4
-------------

+ 5
+ 6
+ 7
+ 8

Why this repo5
-------------

long contents .....

1. a
2. b
3. c
4. d

Why this repo6
-------------

long contents .....

+ 1
+ 2
+ 3
+ 4

Why this repo7
-------------

long contents .....

1. e
2. f
3. g
4. h

Why this repo8
-------------

+ 5
+ 6
+ 7
+ 8

Why this repo9
-------------

long contents .....

1. a
2. b
3. c
4. d

Why this repo10
-------------

long contents .....

+ 1
+ 2
+ 3
+ 4

Why this repo11
-------------

long contents .....

1. e
2. f
3. g
4. h

Why this repo12
-------------

+ 5
+ 6
+ 7
+ 8

Why this repo13
-------------

long contents .....

1. a
2. b
3. c
4. d

Why this repo14
-------------

long contents .....

+ 1
+ 2
+ 3
+ 4

Why this repo15
-------------

long contents .....

1. e
2. f
3. g
4. h

Why this repo16
-------------

+ 5
+ 6
+ 7
+ 8

[1]: https://github.com/allejo/jekyll-toc
