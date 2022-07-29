---
title: 알고리즘 공부_KMP
author: HH KWON
date: 2022-07-29
category: Jekyll
layout: post
---

# KMP 개념

## 접두사와 접미사
 - ABCDC 에서 접두사는<br> A<br> AB<br> ABC<br> ABCD<br> ABCDC
 - ABCDC 에서 접미사는<br> C<br> DC<br> CDC<br> BCDC<br> ABCDC<br>

|길이  |접두사  |접미사  |
|:---:|:-----:|:-----:|
|1    |A      |C      |
|2    |AB     |DC     |
|3    |ABC    |CDC    |
|4    |ABCD   |BCDC   |
|5    |ABCDC  |ABCDC  |

## 일반적인 방법으로 문자열 탐색하기
<img src="../gitbook/images/kmp_1.JPG" width="300" height="70"><br>
찾으려는 문자가 CDC라고 할 때, 첫 문자를 비교하여 일치하지 않으므로 오른쪽으로 한 칸 시프트<br>
<img src="../gitbook/images/kmp_2.JPG" width="300" height="70"><br>
역시 첫 문자를 비교하여 일치하지 않으므로 한 칸 시프트<br>
<img src="../gitbook/images/kmp_3.JPG" width="300" height="70"><br>
첫 문자를 비교하여 일치하는 부분을 찾음<br>
<img src="../gitbook/images/kmp_4.JPG" width="300" height="70"><br>
이어서 바로 이웃한 옆 문자를 비교하여 일치하는 것을 확인<br>
<img src="../gitbook/images/kmp_5.JPG" width="300" height="70"><br>
바로 그 다음 문자도 비교하여 일치하는 것을 확인. 이런 과정을 통해 ABCDC에서 CDC를 찾을 수 있음<br>
   
## KMP 알고리즘 : 패턴 매칭 이용
### 패턴을 먼저 정의
- 예를 들어 문자열이 BABCDABCABCDABCDADDABCDABCEFX 이고 찾아야 할 문자열이 ABCDABCC 라고 할 때
- 처음에는 일반적인 방법으로 일치하는 문자열을 아래와 같이 ABCDABC를 찾았다고 할 때 이에 대한 패턴을 찾아줌<br>
<img src="../gitbook/images/kmp_1_1.JPG" width="500" height="70"><br>
  아래와 같이 찾은 패턴의 길이는 3인데, 위 경우와 다르게 2개 이상의 패턴을 찾는다면 가장 큰 값을 패턴 값으로 정해준다
  
|패턴길이|접두사|접미사|
|:---:|:-----:|:-----:|
|0    |A      |C      |
|0    |AB     |BC     |
|3    |ABC    |ABC    |
|0    |ABCD   |DABC   |
|0    |ABCDA  |CDABC  |
|0    |ABCDAB  |BCDABC  |

- 문자열이 일치하지 않기 때문에 다음 인덱스를 탐색해야 하는데, 이때 일반적인 방식과 다른 점은 한 칸씩 시프트 하지 않는다는 점
- 위 표와 같이 찾은 문자열의 접두사와 접미사가 *ABC*로 일치한다는 것을 찾았기 때문에 탐색 인덱스는 다음 ABC부터 탐색을 이어간다<br>
<img src="../gitbook/images/kmp_1_2.JPG" width="500" height="70"><br>
즉, *찾은 문자열의 길이* - *패턴의 길이* = 7 - 3 = 4 만큼 점프하여 탐색을 이어간다<br>


<0> 연결 리스트에 노드 간 연결 정보를 정리, 방문 순서를 저장할 리스트 P선언<br>
<1> 하나의 정점에서 시작<br>
<2> 방문 표시를 하면서 해당 노드를 Stack에 넣고, 간선을 따라 다음 정점으로 이동<br>
<3> 더 방문할 곳이 없으면 리스트 P의 **앞**에 정점을 추가<br>
<4> Stack이 비었을 경우에는 백트래킹을 통해 아직 방문하지 않은 노드를 Stack에 추가하고, <1>부터 <3>까지의 과정 반복<br><br><br>
### BFS를 이용한 구현
<0> 진입차수를 저장하기 위한 리스트를 선언하고, 연결 리스트에 노드 간 연결 정보 정리.<br>방문 순서를 저장할 리스트 P선언<br>
<1> **진입차수가 0**인 노드는 **방문한 것으로 표시**하고, 큐에 추가<br>
<2> 큐에서 가장 앞 노드를 P에 추가하고, 연결된 노드 중 방문하지 않은 노드의 진입차수를 1감소<br>
<3> 감소한 진입차수가 0인 경우 해당 노드를 큐에 넣고, 방문 표시.<br>위 <2>부터 <3>까지 과정을 큐가 빌 때까지 반복 수행<br><br>
