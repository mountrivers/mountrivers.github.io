---
title: "Edge Case: Nested and Mixed Lists"
categories:
  - Edge Case
tags:
  - content
  - css
  - edge case
  - lists
  - markup
---



```
/*
Problem : 백준 10814 나이순 정렬
작성자 : 이산하
작성 일시 : 2019 / 05 / 03

Version 1.0
- 최초 작성 2019/ 05 / 03

*/

#include <string>
#include <iostream>
#include <map>

using namespace std;

int main() {
	int N;
	multimap <int, string> mm;
	int n;
	string temp;
	cin >> N;
	for (int i = 0; i < N; i++) {
		cin >> n >> temp; 
		mm.insert(make_pair(n, temp));
	}
	/*
		대표적으로 C++ 의 멀티맵을 사용하면 매우 편한 문제입니다. 
		멀티맵은 설명하기에는 너무 길어서 검색으로 따로 확인 해
		보시는 걸 추천합니다.

		map, multimap, set, unorderdset 은 자주 쓰일일이 많으니
		꼭 숙지 해 주시는게 좋아요.
	*/
	for (auto a = mm.begin(); a != mm.end(); a++) {
		cout << a->first << " " << a->second << "\n";
		// cout << endl <= 하면 시간 초과납니다. 
	}
	return 0; 
}
```
