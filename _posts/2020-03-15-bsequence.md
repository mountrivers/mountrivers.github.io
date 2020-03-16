---
title: "[BOJ] 백준 수열 N과 M 문제 종합"
date: 2020-03-15
categories: 
  - 백준
tags: 
  - 백준
  - C++
  - 수열
---

# basic

같은수 여러번X 순서 상관 O : https://mountrivers.github.io/boj15649/

같은수 여러번X 순서 상관 X :https://mountrivers.github.io/boj15650/

같은수 여러번O 순서 상관 X : https://mountrivers.github.io/boj15651/

같은수 여러번O 순서 상관 X 무조건 오름차순 :  https://mountrivers.github.io/boj15652/

# 값이 기본으로 주어지는 

단순하게 수열을 받고, 소트 해준 다음, 위에 basic 단계에서 순서만 뽑아다 쓰면 된다. 


같은수 여러번X 순서 상관 O / 값이 주어짐  : https://mountrivers.github.io/boj15654

같은수 여러번X 순서 상관 X / 값이 주어짐  : https://mountrivers.github.io/boj15655

같은수 여러번O 순서 상관 X / 값이 주어짐  : https://mountrivers.github.io/boj15656

같은수 여러번O 순서 상관 X 무조건 오름차순/ 값이 주어짐  : https://mountrivers.github.io/boj15657

# 값이 주어지지만, 중복이 가능 한 것

unordered_set 사용 -> 결과 체크 

```
unordered_set<string> checker;

string temp;
		for (int i = 0; i < m; i++) {
			temp +=  to_string(result[v[i]]) + " ";
		}
		auto itr = checker.find(temp);
        if (itr == checker.end())
            결과
}
```
set 을 사용하여, 이미 출력한 것과 같은것이 있는지 판단하고, 

확인하고 결과를 출력하면 됩니다. 

예를들어, 1 5 9 10 을 검사하려면, 

이를 문자열로 만들어

"1 5 9 10" 으로 만듭니다. 

이걸 set 에서 "1 5 9 10"이 있는지 검사를 합니다. 

그리고 만약에 있다면 넘어가고, 

없다면 "1 5 9 10" 을 set에 넣어주는것과 동시에 

" 1 5 9 10 " 을 출력 해주면 됩니다. 

여기서, 뛰어쓰기를 넣어주는 이유는, 

1 11 111 이 있다면, 

3개가 들어갈때, 어떤 순서이든, "111111" 이 되버림으로

"1 11 111 ", "1 111 11 " 이런식으로 구분 하기 위해 중간에 띄어쓰기를 넣게 됩니다. 

N과M 9

순서 상관 O / 같은 수 여러개까지 값이 주어짐  : https://mountrivers.github.io/boj15663

N과M 10

 순서 상관 X / 같은 수 여러개까지 값이 주어짐  : https://mountrivers.github.io/boj15664
 
N과M 11

같은수 여러번O 순서 상관 X / 같은 수 여러개까지 값이 주어짐  : https://mountrivers.github.io/boj15665

N과M 12

같은수 여러번O 순서 상관 X 무조건 오름차순/ 같은 수 여러개까지 값이 주어짐  : https://mountrivers.github.io/boj15666
