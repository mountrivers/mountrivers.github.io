---
title: " 컴퓨터공학 취준 짤막 면접 - 싱글톤 이론, 구현"
date: 2019-06-15
categories: study
tags: 
  - singleton
  - c++
  - designpattern
  - 짤막면접준비
---

# 싱글톤 이란? 
 오직 하나만 존재하며, 후천적 정적이며, 전역적으로 사용 할 수 있다. 
 
 
# 싱글톤이 필요한 이유
 싱글톤과 비슷한 기능으로, 전역 정적 변수를 사용 할 수 있지만, 전역 정적변수는
 
 프로그램이 시작되는 것과 동시에 반드시 초기화가 진행 된다. 
 
 그러나 싱글톤을 사용하면, 나중에 필요한 값을 넣어서 고정을 시켜 줄 수 있다. 
 
 누군가가 객체를 새로 만들어도 만들어지는 것이 아니라 기존에 만들어 준 객체를 바라본다.
 
# 예시 코드
```
#include <iostream>

using namespace std;

class singleton {
public:
	static singleton* getinstance() {
		if (!one ) {
			one = new singleton;	
		}
		return one;
	}
	void set(int a, int b) {
		id = a; 
		pw = b;
	}
	void show() {
		cout << "ID : " << id << " PW : " << pw << endl;
	}
private:
	static singleton* one;
	int id;
	int pw;
	singleton() {
		id = 0;
		pw = 0;
	}
};
singleton* singleton::one = 0;


int main() {
	int a;
	singleton *test1 = singleton::getinstance();
	test1->set(123, 234);
	test1->show();

	singleton *test2 = singleton::getinstance();
	test2->show();

	cout << test1 << " " << test2;
	cin >> a;
	return 0;
}
```

# 결과

![singleton](https://user-images.githubusercontent.com/36880919/59552870-24ca1c80-8fc7-11e9-8c1b-7e135faeeef7.PNG)

객체를 하나 더 만들었는데도, id, pw 값은 동일하며

가리키는 주소 또한 같은 것을 확인 할 수 있다. 
