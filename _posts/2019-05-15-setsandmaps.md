---
title: " C++ 셋(set) 과 멥(map) 간단하게 "
date: 2019-05-03 -0400
categories: 지식
tags: 
  - 셋
  - 멥
  - set
  - map
  - multimap
  - multiset
  - unordered_set
  - unordered_map
  - 멀티셋
  - C++
  - 멀티맵
---

이번 포스팅은 앞으로도 셋,멥 관하여 쓸일이 종종 있을 거 같기에..

정리 하는겸, 저도 참고 하기 위해서 작성 하게 되었습니다.

우선 간단하게 SET 과 MAP 이 무엇인지 확인하고 넘어가볼께요

SET : 해당 데이터가 있나? 없나 확인
MAP : 해당 번호에 뭐가 들어있나? 

# SET

## 추가 방식
```
set<int> s;
s.insert(10);
s.insert(5);
```
## 데이터 있는지 확인하는 방법
```
auto itr = s.find(10);
itr == itr.end() <= 없음
itr != itr.end() <= 있음
```

## 전체 출력
```
for(auto itr = s.begin() ; itr != s.end(); itr++){
    cout << *itr
}
```

## 특징
- 자동으로 정렬됨
- 탐색시 O(LogN) 보장 ( 트리 형식으로 데이터를 저장합니다. 단순 트리보다는 보정이 있어서 한쪽으로 쏠리는걸 방지해줍니다.)
- 중복을 허용하지 않습니다. ( 다만 insert 시 컴파일 환경에 따라서 자동으로 insert처리 안하는 곳이 있는 반면
  이미 있는값을 insert 시 런타임 에러 나는 환경이 있을 수 있습니다. 중복값이 올 수 있다면 find 로 확인을 하고 넘어가야합니다.)
  
# unordered_set
## 작동 방식 
 - 기본적으로 사용 방법은 위의 SET과 완전히 동일합니다.
 - 다른점은 정렬을 해주지 않습니다. 해시를 사용하여 데이터 값이 순서대로 저장 되지 않습니다.
 - 해시를 사용하는 만큼 탐색시 O(1) 을 보장합니다. 
   => 즉 데이터가 있는지 없는지만 판단 하려 한다면 unordered_set 이 제일 빠릅니다.
   => 반면 데이터의 추가,삽입 시 해시이기 때문에, 재해싱이 일어 날 수 있으며, 재해싱 하게 된다면
    모든 데이터를 다시 복사 해서 옮겨야 하기 때문에 그 과정에서 O(N)의 시간이 소요됩니다.
    (즉 find = O(1) , insert = O(1) or O(N))
    
# multi_set
## 작동 방식
 - 기본적으로 사용 방법은 위의 SET과 완전 동일 합니다.
 - 중복으로 값이 들어가는 것을 허용 해줍니다. 
 
 
 
# MAP
## 추가 방식
```
map<int,string> m;
m.insert(make_pair(1,"hi");  (혹은 m.insert(pair<int,string>(1,"hi")) 도 가능합니다. )
m.insert(make_pair(2,"gi");
m[3] = "oh!"   <= 이렇게도 추가가 가능합니다. 다만 권장 하지는 않습니다.
```
## 데이터 있는지 확인하는 방법
```
auto itr = m.find(1);
itr == itr.end <= 없음
itr != itr.end <= 있음
```

## 전체 출력
- 첫값은 itr->first , 두번쨰 값은 itr->second
```
for(auto itr = m.begin() ; itr != m.end(); itr++){
    cout << itr->first << " " << itr->second ;  
}
```

## 특징
- 자동으로 정렬됨
- 탐색시 O(LogN) 보장 ( 트리 형식으로 데이터를 저장합니다. 단순 트리보다는 보정이 있어서 한쪽으로 쏠리는걸 방지해줍니다.)
- 중복을 허용하지 않습니다. ( 다만 insert 시 컴파일 환경에 따라서 자동으로 insert처리 안하는 곳이 있는 반면
  이미 있는값을 insert 시 런타임 에러 나는 환경이 있을 수 있습니다. 중복값이 올 수 있다면 find 로 확인을 하고 넘어가야합니다.)
 
 # multi_map
 ## 작동 방식
  - 기본적으로 사용 방법읜 위의 SET과 거의 동일합니다.
  - 중복으로 값이 들어가는 것을 허용 해 줍니다.
  - 다만 set처럼 있는지 없는지가 아닌 Pair 형태임으로 탐색시 특별한 방법으로 탐색을 해야 합니다.
  - 위의 이유와 마찬가지로 [] 를 사용하여서 호출 할 수 없습니다.
  - sql기능 없이 두 표를 합하거나 할때 등 있으면 꼭 유용한 사항이 있기에 연습 해보시는걸 추천드립니다.
  
 ## 특정 데이터의 pair 값 찾기
 ```
 auto range = m.equal_range(1);
  for (auto itr = range.first; itr != range.second; ++itr) {
    cout << itr->first << " : " << itr->second << " " << endl;
  }
  ```
  - 위와 같이 행하면 range 는 새로운 pair<int,int> range 로 만들어지며, range->first 는 equal_range(x) 에서 x와 동일한 값의 처음을,
     range->second 는 equal_range(x) 에서 x 와 동일한 값의 마지막을 불러오게 됩니다. 
     ```
     // 현재 m 에 들어있는 것 => (1,a), (2,b), (3,d), (3,f), (3,g), (4,h)
     auto range = m.equal_range(3)
     // range->first => (3,d) 가 저장된 위치, range->second = (3,g) 가 저장된 위치
     ```
     
  # unordered_map
  ## 작동 방식 
 - 기본적으로 사용 방법은 위의 MAP과 완전히 동일합니다.
 - 다른점은 정렬을 해주지 않습니다. 해시를 사용하여 데이터 값이 순서대로 저장 되지 않습니다.
 - 해시를 사용하는 만큼 탐색시 O(1) 을 보장합니다. 
   => 즉 데이터가 있는지 없는지만 판단 하려 한다면 unordered_map 이 제일 빠릅니다.
   => 반면 데이터의 추가,삽입 시 해시이기 때문에, 재해싱이 일어 날 수 있으며, 재해싱 하게 된다면
    모든 데이터를 다시 복사 해서 옮겨야 하기 때문에 그 과정에서 O(N)의 시간이 소요됩니다.
    (즉 find = O(1) , insert = O(1) or O(N))
    
    
    
# 개인적인 중요도 순서
- map > set > multi_map > unodered_set  = unodered_map = multi_set 이라고 생각 합니다. 
범용성 기준으로 저의 주관적인 생각입니다. 뒤에 3개에 다 동일을 준 이유는 너무 특수한 상황에서만 쓰기 때문에 
이렇게 점수를 줬습니다. 



  
     
