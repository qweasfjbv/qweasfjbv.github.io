---
title: AOJ-STRJOIN
author: qweasfjbv
date: 2021-01-03 20:38:00 +0900
categories: [Algorithm, Problem Solving]
tags: [Greedy]
toc: false
---

## AOJ STRJOIN

<https://www.algospot.com/judge/problem/read/STRJOIN>

### Answer

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool cmp(int& a, int& b) {
	return a > b;
}

// a, b, c를 합칠 때 (a+b) + ((a+b) + c) 가 비용이 된다.
// 먼저 합치면 여러번 중첩해서 더하므로 작을수록 먼저합쳐야 최소가 된다.
int main() {

	int c, n;
	cin >> c;

	for (int t = 0; t < c; t++) {
		cin >> n;
		int sum = 0;
		vector<int> arr(n);
		
		for (int i = 0; i < n; i++) {
			cin >> arr[i];
		}


		int tmp;
		while (arr.size() != 1) {
			sort(arr.begin(), arr.end(), cmp);
			tmp = arr[arr.size() - 1] + arr[arr.size() - 2];
			arr.pop_back(); arr.pop_back();
			arr.push_back(tmp);
			sum += tmp;

		}

		cout << sum << '\n';

	}


	return 0;
}
```

항상 배열에서 가장 작은 두 문자열을 붙이는게 최소비용을 얻기 위한 방법이었다. 가장 작은 두 문자열의 길이를 더한 값을 tmp에 저장하고 `arr.pop_back()`으로 없앴다. 그 후에 `arr.push_back()`으로 tmp를 배열에 넣어주고 다시 sort로 내림차순 정렬을 해 최솟값을 구할 수 있게 만들었다.