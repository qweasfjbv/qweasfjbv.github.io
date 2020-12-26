---
title: AOJ-QUADTREE
author: qweasfjbv
date: 2020-12-25 16:37:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DivideAndConquer]
toc: false
math: true
---

## AOJ QUADTREE

<https://www.algospot.com/judge/problem/read/QUADTREE>

### Answer

```cpp
#include <iostream>
#include <string>
using namespace std;

// 상하로 뒤집는건
// x(A)(B)(C)(D)를 x(C)(D)(A)(B)순으로 출력 (재귀로)

string s;
int point = 0;

void Print(bool print) {

	if ((s[point] == 'w' || s[point] == 'b') && print ) cout << s[point];

	int restart;
	int fi;

	if (s[point] == 'x') {
		restart = point;
		if (print)
			cout << 'x';
		point++;
		Print(false);
		point++;
		Print(false);
		point++;
		Print(print);
		point++;
		Print(print);
		if (print) {
			fi = point;
			point = restart;
			point++;
			Print(print);
			point++;
			Print(print);
			point = fi;
		}
	}

}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);
	int C;
	cin >> C;
	for (int i = 0; i < C; i++) {
		point = 0;
		cin >> s;
		Print(true);
		cout << "\n";
	}


	return 0;
}
```

문제의 조건중에서 "원본 그림의 크기는 \\(2^20×2^20\\)을 넘지 않는다" 고 나와있어서 2차원 배열로 원본 그림을 복원하게 되면 주어진 시간을 초과할 것 같아서 주어진 텍스트를 가지고 규칙을 통해 풀었다.
규칙은 간단했다. x(A)(B)(C)(D) 와 같은 형태에서 x(C)(D)(A)(B) 와 같은 형태로 바꿔 출력하면 되는 문제였다. 그래서 false를 통해 출력하지 않는동안 A를 출력하기 위한 시작인덱스를 저장했고, 다 출력하고 나서는 다시 돌아갈 인덱스를 저장했다.