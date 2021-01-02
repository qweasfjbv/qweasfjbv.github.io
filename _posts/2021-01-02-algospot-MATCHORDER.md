---
title: AOJ-MATCHORDER
author: qweasfjbv
date: 2021-01-02 21:30:00 +0900
categories: [Algorithm, Problem Solving]
tags: [Greedy]
toc: false
---

## AOJ MATCHORDER

<https://www.algospot.com/judge/problem/read/MATCHORDER>

### Answer

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int rus[100];
int kor[100];
int N;

void swap(int& a, int& b) {
	int tmp;
	tmp = a;
	a = b;
	b = tmp;
}

int main() {

	int C;

	cin >> C;
	for (int t = 0; t < C; t++) {

		cin >> N;
		for (int i = 0; i < N; i++) {
			cin >> rus[i];
		}
		for (int i = 0; i < N; i++) {
			cin >> kor[i];
		}

		int m, index;
		int tmp;
		int cnt = 0;
		for (int i = 0; i < N; i++) {
			m = 4001;
			tmp = 4001;
			for (int j = i; j < N; j++) {
				if (rus[i] <= kor[j] && m > kor[j]) {
					m = kor[j];
					index = j;
				}
			}

			if (m == 4001) {
				for (int j = i; j < N; j++) {
					if (tmp > kor[j]) {
						index = j;
						tmp = kor[j];
					}
				}
			}
			swap(kor[i], kor[index]);


		}

		for (int i = 0; i < N; i++) {
			if (rus[i] <= kor[i]) cnt++;
		}

		cout << cnt << '\n';

	}


	return 0;
}
```

간단한 그리디 문제였다. i부터 N 사이에 rus[i] 보다 큰 kor[j] 가 없다면 가장 작은 값을, 있다면 그 중에서 가장 작은 값을 찾아서 swap함수로 바꿔준 후에 다시 처음부터 승수를 하나씩 셌다.