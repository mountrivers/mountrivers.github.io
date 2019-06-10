---
title: " base64 디코딩 소스 C++, 마스크 " 
date: 2019-06-08
categories: study
tags:
- c++
- base64
- mask
--- 

# 설명
base 64 란 암호 체계의 일종입니다. 

방법 자체는 따로 크게 설명 할 피요는 없다고 생각합니다..

요구하는 거 자체가 그렇게 어려운 건 아니거든요. 

중간에 들어간 코딩 방법에 대하여만 설명 하도록 하겠습니다.

우선 마스크가 무엇인가? 에 대하여는 추후에 기회가 된다면

상세하게 따로 포스팅을 하고

여기서는 간단하게 짚고만 넘어 가겠습니다. 

마스크란 특정수의 비트를 따오기 편합니다.

예를들면 8비트는 0000 0000 처럼 2진수로 나누면 총 8자리로 나뉩니다.

이떄 각 자리 수가 1인지 0인지, 혹은 일정 범위가 1인지 0인지 알려면 

마스크 없이는 기존에 나눗셈을 하며 하나하나 분리 해야 합니다.

그러나 필요한 영역을 마스크로 만들어서

0011 1100 이렇게 만들면 어떨까요?

수 & 마스크 로 비트 연산을 하게 되어 0011 1100 의 1부분이 일치 하는 것만을 얻어 낼 수 있습니다.

이 문제에서는 마스크로 엄청난 성능 향상을 하진 못했고

2로 나누어 쪼개주는 것은 역순으로 쪼개지기 때문에 8xn 만큼의 시간이 줄어 들게 되겠죠

자세한 내용은 코드에 주석에 최대한 상세하게 적으려고 노력 했으니 

코드로 확인 해주세요.

# 코드
```
/*
	file : Base64Decoding.cpp
	lastChange : 10/31
	remain problem:
		- 아스키 코드 외 한글,중국어,일본어 등 유니코드 불가능
		- 뛰어쓰기와 엔터에 대하여 처리가 불가능 => UI를 만들어 TextBox 채로 값을 넘겨받거나 데이터 파일을 만들어 불러 오는식이 필요
	time complexity big(o) = n
*/

   

#include <iostream>
#include <cmath>
#include <string>
#include <queue>

#define zero 0
#define one 1
#define two 2
#define three 3
#define five 5
#define six 6
#define eight 8

using namespace std;

void main() {
	static const int mask_seven = pow(two, 6);
	static const int mask_six = pow(two, 5);
	static const int mask_five = pow(two,4 );
	static const int mask_four = pow(two,3 );
	static const int mask_three = pow(two,2 );
	static const int mask_two = pow(two,1 );
	static const int mask_one = pow(two,0 );

	int queueSize = zero;
	int remain = zero;
	int numOfResult = zero;
	int sum = zero;
	
	queue<int> bitQueue;

	string base64_Requset;

	static const string base64_chars =
		"ABCDEFGHIJKLMNOPQRSTUVWXYZ"
		"abcdefghijklmnopqrstuvwxyz"
		"0123456789+/";

	cout << "Enter the input ->>";
	cin >> base64_Requset;

	queueSize = base64_Requset.length() * eight;

	remain = (queueSize%six) / two;
	numOfResult = (queueSize / six);

	// 맨앞글자를 8bit로 쪼개며 큐에 넣고 맨앞글자를 지움. 글자수가 0이될때까지 진행
	// 속도를 더 빠르게 만드려면 아스키코드 표 자체를 2차원 배열로 미리 쪼개 놓아 자료를 저장해놓고
	// 불러오는게 훨씬 빠른 속도
	// ex ) abcd 입력 -> echart[a][0]~echart[a][7] 이런식으로 
	// 아스키 코드만으로는 페리티비트 한개 제외 127개밖에 없기 때문
	

	while (base64_Requset.length()) {
		char temp = base64_Requset.at(zero);
		cout << temp << "loaded" << endl;
		bitQueue.push(zero);	// 패리티 비트
		bitQueue.push(temp&mask_seven);
		bitQueue.push(temp&mask_six);
		bitQueue.push(temp&mask_five);
		bitQueue.push(temp&mask_four);
		bitQueue.push(temp&mask_three);
		bitQueue.push(temp&mask_two);
		bitQueue.push(temp&mask_one);
		base64_Requset.erase(zero, one);
	}

	// 6비트씩 나눠지는 완전한 갯수만 실행 ( 입력받은 글자수 * 8비트 / 6비트)
	for (int searchQueue = 0; searchQueue < numOfResult; searchQueue++) {
		sum = zero;

		// 6비트씩 묶어서 진행
		for (int que = five; que >=zero; que--) {
			int temp = bitQueue.front();
			if (temp != zero)
				sum += pow(two, que);
			bitQueue.pop();
		}
		cout << base64_chars[sum];
	}
	
	sum = zero;

	// 6bit 씩 완전히 채우고 남은 것 (입력받은 글자수 * 8비트 % 6비트)
	switch (remain) {
	case zero:
		break;
	case one:
		for (int que = five; que >= 4; que--) {
			int temp = bitQueue.front();
			if (temp != zero)
				sum += pow(two, que);
			bitQueue.pop();
		}
		cout << base64_chars[sum] << "==";
		break;
	case two:
		for (int que = five; que >= 2; que--) {
			int temp = bitQueue.front();
			if (temp != zero)
				sum += pow(two, que);
			bitQueue.pop();
		}
		cout << base64_chars[sum] << "=";
		break;
	}

	// end
	int blank;
	cin >> blank;

	

}
```
