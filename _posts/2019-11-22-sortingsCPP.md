---
title: "c++ 코딩테스트 유용 모음집"
date: 2019-09-22
categories: 
  - study
tags: 
  - code
  - C++
  - sort
  - 버블정렬
  - 선택정렬
  - 삽입정렬
  - 쉘 정렬
  - 퀵 정렬
  - 병합정렬
  - 힙 정렬
  - 기수정렬
---

# 어떤 정렬을 선택할까 

순서대로, 평균 시간복잡도, 최악 시간 복잡도, 순서 유지 여부
1. 버블정렬		N^2 / N^2/N^2 O
2. 선택정렬 	N^2 / N^2 / N^2 X
3. 삽입정렬 	N / N^2 / N^2 O
4. 쉘 정렬		N / N^1.5 / N^2 X 
5. 퀵 정렬		NlogN / NlogN / N^2  X
6. 병합정렬		NlogN / NlogN / NlogN  O
7. 힙 정렬		nLogN / NlogN / NlogN  X
8. 기수정렬		dN/ dN / dN   O

순서 유지 여부가 중요한 정렬은, 소팅하면서 순서가 바뀌면 안된다는것. 

예를들어 (1,50), (1,100), (2, 50) 을 앞에 만 보고 소팅했을때

(1,100), (1,50), (2,50) 이 되면 안된다는것. 

즉 일반적으로 하나만 정렬하는것에서는 크게 중요하지 않다. 

# 무슨 정렬이 좋을까? 

우선 기본적으로 cpp 의 기본 라이브러리 sort를 사용 하는 것이 좋다. 

만약 시간이 너무 오래걸릴것 같다면, 기수정렬 사용을 강력 추천한다. 

특히나 최대 자릿수가 정해져 있다면 기수정렬만큼 우수한 정렬이 없다. 

예를들어 최대 3자리 숫자로 이루어 진 것을, 100억개 정렬한다고 생각을 해보자. (과한대입)

퀵소트로 할 경우, 100억 로그 100억 이다. 

그러니 기수정렬을 사용할 경우, 3X 100억이다. 

이글을 읽고있다면 무언가 잘못된 것이 보여야한다.

바로 100억개를 소팅하고 있으면 멍청이란 것.

최대 자릿수가 3개라고 했으니, 1000칸짜리 배열을 만들어서, 입력받고, 해당 칸의 숫자를 올려주면 된다. 

물론 최대 20자리 까지 있는 기수정렬이라면 기수정렬이 유리하다. 

그러니 기수정렬이 좋아보인다면, 배열로 만들어 사용하는것은 어떨지 생각 해 보아야 한다. 

만약에 단순 숫자만 아니라 페어로 이루어져서 (최대 3자리 숫자로 이루어 진 수, 무언가 추가적인것) 처럼 추가정보가 있는거 또한 마찬가지입니다.

다만 배열 대신 멀티멥을 이용하여 사용하면 역시나 같은 방법으로 가능 합니다. 


# 다른 정렬은 ? 
 삽입정렬 또한 다양하게 응용하여 사용이 가능합니다. 무언가 계산을 하여 차근차근 정렬을 해야한다면
 
 삽입정렬도 매우 좋은 방법입니다. 
 
 삽입정렬을 보완한게 쉘 정렬이나, 삽입정렬의 이점을 살리지 못함으로, 굳이 사용 할 필요는 없다. 
 
 다만, 쉘정렬의 원리를 알아두면 언젠가 분명 도움이 될 날이 올 수 있으니 개념은 찾아보도록 하자.
 

```
#include <iostream>
#include <fstream>
#include <queue>

using namespace std;
/*
1. 버블정렬		N^2 / N^2/N^2 O
2. 선택정렬 	N^2 / N^2 / N^2 X
3. 삽입정렬 	N / N^2 / N^2 O
4. 쉘 정렬		N / N^1.5 / N^2 X 
5. 퀵 정렬		NlogN / NlogN / N^2  X
6. 병합정렬		NlogN / NlogN / NlogN  O
7. 힙 정렬		nLogN / NlogN / NlogN  X
8. 기수정렬		dN/ dN / dN   O


*/


int* buble(int* chart,int length) {
	for (int x = 0; x < length; x++) {
		for (int y = 0; y < length - x-1 ; y++) {
			if (chart[y] > chart[y + 1])
				swap(chart[y], chart[y + 1]);
		}
	}
	return chart;
}

int* select(int* chart, int length) {
	int temp;
	for (int x = 0; x < length-1; x++) {
		temp = x;
		for (int y = x+1; y < length ; y++) {
			if (chart[y] < chart[temp])
				temp = y;
		}
		if (temp != x)
			swap(chart[x], chart[temp]);
	}
	return chart;
}

int* insert(int* chart, int length) {
	for (int x = 1; x < length - 1; x++) {
		int y = x;
		while (y > 0 && (chart[y - 1] > chart[y])) {
			swap(chart[y - 1], chart[y]);
			y--;
		}
	}
	return chart;
}


void shell_insert(int list[], int first, int last, int gap) {
	int x, y, key;

	for (x = first + gap; x <= last; x = x + gap) {
		key = list[x];
		for (y = x - gap; y >= first && list[y]>key; y = y - gap) {
			list[y + gap] = list[y];
		}

		list[y + gap] = key;
	}
}
void shell(int* chart, int length) {
	int index, gap;

	for (gap = length / 2; gap>0; gap = gap / 2) {
		if ((gap % 2) == 0) {
			gap++;
		}

		for (index = 0; index<gap; index++) {
			shell_insert(chart, index, length - 1, gap);
		}
	}
}

void quick(int* chart, int left, int right) {
	int pivot = left;
	int end = right;
	left++;
	while (left < right) {
		while ((chart[left] < chart[pivot]) && (left < right))
			left++;
		while (chart[right] > chart[pivot] && (left < right))
			right--;
		swap(chart[left], chart[right]);
	}
	if (chart[pivot] < chart[left])
		left--;
	swap(chart[pivot], chart[left]);
	if(pivot < left)
		quick(chart, pivot, left-1);
if (right < end)
	quick(chart, right, end);
}

void merge(int* chart, int left, int right) {
	if (right > left) {
		int m = (right + left) / 2;

		merge(chart, left, m);
		merge(chart, m + 1, right);
		int leftPivot = left;
		int rightPivot = m + 1;
		int merged[11];
		int index = left;
		while ((leftPivot <= m) && (rightPivot <= right)) {
			if (chart[leftPivot] > chart[rightPivot]) {
				merged[index] = chart[rightPivot];
				rightPivot++;
			}
			else {
				merged[index] = chart[leftPivot];
				leftPivot++;
			}
			index++;
		}
		while (leftPivot <= m) {
			merged[index] = chart[leftPivot];
			leftPivot++;
			index++;
		}
		while (rightPivot <= right) {
			merged[index] = chart[rightPivot];
			rightPivot++;
			index++;
		}

		for (int i = left; i <= right; i++) {
			chart[i] = merged[i];
		}
	}
}

void maxHeap(int* chart, int length) {
	int pointer = length;
	int tempPointer;
	while (pointer > 0) {
		if (pointer % 2 == 0)
		{
			pointer--;
			if (chart[pointer / 2] < chart[pointer]) {
				swap(chart[pointer / 2], chart[pointer]);
				tempPointer = pointer / 2;
				while (tempPointer * 2 + 1 <= length) {
					if (chart[tempPointer * 2 + 1] > chart[tempPointer])
						swap(chart[tempPointer * 2 + 1], chart[tempPointer]);
					if ((tempPointer * 2 + 2 <= length) && (chart[tempPointer * 2 + 2] > chart[tempPointer]))
						swap(chart[tempPointer * 2 + 2], chart[tempPointer]);
					tempPointer = tempPointer * 2 + 1;
				}
				tempPointer = pointer / 2;
				while (tempPointer * 2 + 1 <= length) {
					if (chart[tempPointer * 2 + 1] > chart[tempPointer])
						swap(chart[tempPointer * 2 + 1], chart[tempPointer]);
					if ((tempPointer * 2 + 2 <= length) && (chart[tempPointer * 2 + 2] > chart[tempPointer]))
						swap(chart[tempPointer * 2 + 2], chart[tempPointer]);
					if (tempPointer == 0)
						tempPointer = 1;
					tempPointer = tempPointer * 2 + 2;
				}
			}
			pointer++;
			if (chart[pointer / 2 - 1] < chart[pointer]) {
				swap(chart[pointer / 2], chart[pointer]);
			}
			pointer -= 2;
		}

		else {
			if (chart[pointer / 2] < chart[pointer]) {
				swap(chart[pointer / 2], chart[pointer]);
			}
			pointer--;
		}
	}
}
void alterHeap(int* chart, int length) {
	int pointer = 0;
	swap(chart[pointer], chart[length]);
	while ((chart[pointer] < chart[pointer * 2 + 1]) || (chart[pointer] < chart[pointer * 2 + 2])) {
		if (pointer * 2 + 1 < length) {
			if (chart[pointer * 2 + 1] > chart[pointer * 2 + 2]) {
				swap(chart[pointer * 2 + 1], chart[pointer]);
				pointer = pointer * 2 + 1;
			}
			else if (pointer * 2 + 2 < length) {
				swap(chart[pointer * 2 + 2], chart[pointer]);
				pointer = pointer * 2 + 2;
			}
			else
				break;
		}
		else
			break;
	}
}
void heap(int* chart, int length) {
	maxHeap(chart, length);
	while (length>1) {
		alterHeap(chart, length);
		length--;
	}
}

void radix(int* chart, int length) {
	int maxMode = 10;
	queue<int> temp;
	for (int i = 0; i < length; i++) {
		while (chart[i] > maxMode)
			maxMode *= 10;
	}
	for (int mod = 10; mod <= maxMode; mod *= 10) {
		for (int num = 0; num < 10; num++) {
			for (int index = 0; index < length; index++) {
				if ((chart[index]*10/mod)%mod == num)
					temp.push(chart[index]);
			}
		}
		for (int index = 0; index < length; index++) {
			chart[index] = temp.front();
			temp.pop();
		}
	}
}


void main() {
	int chart[11] = { 3,9,3,33,21,7,4,2,8,10 };
	int chartsize = 10;
	int endtemp;
	quick(chart, 0, 9);

	 for (int i = 0; i < chartsize; i++) {
		 cout << chart[i] << " ";
	 }
	cin >> endtemp;
}
```
