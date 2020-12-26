---
title: AOJ-FENCE
author: qweasfjbv
date: 2020-12-26 17:36:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DivideAndConquer]
toc: false
---

## AOJ FENCE

<https://www.algospot.com/judge/problem/read/FENCE>

### Answer

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int fence[20000];

int Div(int a, int b) {

	int ret = 0;

	if (a == b) return fence[a];

	int mid = (a + b) / 2;
	
	ret = max(Div(a, mid), Div(mid + 1, b));

	int height = min(fence[mid], fence[mid + 1]);

	ret = max(ret, height * 2);
	int left = mid;
	int right = mid + 1;

	while (a < left || right < b) {

		if (right < b && (a == left || fence[right + 1] >= fence[left - 1])) {
			++right;
			height = min(height, fence[right]);
		}
		else {
			--left;
			height = min(height, fence[left]);
		}


		ret = max(ret, (right - left + 1) * height);
	}





	return ret;
}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	int C;
	int N;
	cin >> C;

	for (int t = 0; t < C; t++) {
		cin >> N;
		for (int i = 0; i < N; i++) {
			cin >> fence[i];
		}
		cout << Div(0, N - 1) << "\n";

	}

	return 0;
}
```

울타리를 반으로 나눠서 오른쪽과 왼쪽, 그리고 두 부분에 포함되는 경우 총 3가지를 재귀적으로 확인하는 함수를 만들었다. 어떻게 풀어야 하는지 몰라서 한참 헤맸다.