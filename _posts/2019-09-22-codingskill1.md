---
title: "c++ 코딩테스트 유용 모음집"
date: 2019-09-22
categories: 
  - study
tags: 
  - code
  - C++
---


# basic
```
#include <iostream>
#include <vector>

// 우선순위 큐 priority_queue<int,vector<int>,greater<int>> pq;
// vecotr<vector<int> a  ( , vector<int>( ) );
```


# bfs
```
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

void bfs(vector<vector<char>> &table, int x, int y, char obj, int max) {

	queue <pair<int, int>> q;
	q.push(make_pair(x, y));

	while (!q.empty()) {
		x = q.front().first;
		y = q.front().second;
		q.pop();
		table[x][y] = '0';
		if (x > 0 && table[x - 1][y] == obj)
		{
			q.push(make_pair(x - 1, y)); table[x - 1][y] = '0';
		}
		if (x < max - 1 && table[x + 1][y] == obj)
		{
			q.push(make_pair(x + 1, y)); table[x + 1][y] = '0';
		}
		if (y > 0 && table[x][y - 1] == obj)
		{
			q.push(make_pair(x, y - 1)); table[x][y - 1] = '0';
		}
		if (y < max - 1 && table[x][y + 1] == obj)
		{
			q.push(make_pair(x, y + 1)); table[x][y + 1] = '0';
		}
	}

}
```

# set map
```
/*
set<int> s;
s.insert(10);
s.insert(5);
auto itr = s.find(10);
itr == itr.end() <= 없음
itr != itr.end() <= 있음
for(auto itr = s.begin() ; itr != s.end(); itr++){
	cout << *itr
}


map<int,string> m;
m.insert(make_pair(1,"hi");  (혹은 m.insert(pair<int,string>(1,"hi")) 도 가능합니다. )
m.insert(make_pair(2,"gi");
m[3] = "oh!"   <= 이렇게도 추가가 가능합니다. 다만 권장 하지는 않습니다.
auto itr = m.find(1);
itr == itr.end <= 없음
itr != itr.end <= 있음
for(auto itr = m.begin() ; itr != m.end(); itr++){
  cout << itr->first << " " << itr->second ;
}


*/
```

# string
```
string a;
string b;
a = b;

a.compare(b) == 0 같을떄 , < 0 사전순
a.clear a비우기
if (a.empty()) 비어있는지 확인
a.substr(x,y) : x부터 y만큼 추출
x자리에 a.find("문자열") 가능
a.erase(x,y) : x부터 y만큼 삭제, y없으면 x뒤 모두 삭제
a[] , a.at() , a.front(), a.back()
a.find("") != string::npos 찾는거 없을때
여러개 찾을때는
pos = a.find("a");
while ( pos != string::npos){
	pos = a.find("a");
}
```

