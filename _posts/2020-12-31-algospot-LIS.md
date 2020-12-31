---
title: AOJ-LIS
author: qweasfjbv
date: 2020-12-31 22:03:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DynamicProgramming]
toc: false
---

## AOJ LIS

<https://www.algospot.com/judge/problem/read/LIS>

### Answer-1

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int arr[500];
int cnt[500];

int findMax(int l) {

	int m = -1;
	for (int i = 0; i < l; i++) {
		if (arr[i] < arr[l]) {
			m = max(m, cnt[i]);
		}
	}
	
	return m;

}

int main() {
	
	cin.tie(0);
	ios::sync_with_stdio(0);

	int C, N;
	cin >> C;
	for (int t = 0; t < C; t++) {
		cin >> N;

		for (int i = 0; i < N; i++) {
			cnt[i] = -1;
		}

		for (int i = 0; i < N; i++) {
			cin >> arr[i];
			int m = 100001;
			for (int j = 0; j < i; j++) {
				m = min(arr[j], m);
			}
			if (m >= arr[i]) {
				cnt[i] = 1;
			}
			else {
				cnt[i] = findMax(i) + 1;
			}
		}

		int maxx = -1;
		for (int i = 0; i < N; i++) maxx = max(maxx, cnt[i]);

		cout << maxx << "\n";


	}

	return 0;
}
```

### Answer-2
```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;

int arr[500];
int cache[500];

int n, C;

int lis(int start) {
	int& ret = cache[start];

	if (ret != -1) return ret;

	ret = 1;
	for (int i = start + 1; i < n; i++) {
		if (arr[start] < arr[i])
			ret = max(ret, lis(i) + 1);
	}

	return ret;
}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> C;

	for (int t = 0; t < C; t++) {
		cin >> n;
		for (int i = 0; i < n; i++) {
			cin >> arr[i];
		}

		int m = -1;
		for (int i = 0; i < n; i++) {
			memset(cache, -1, 500 * sizeof(int));
			m = max(lis(i), m);
		}

		cout << m << "\n";
	}




	return 0;
}
```

바로 전에 풀었던 AOJ-TRIANGLEPATH 문제와 같이 반복문과 재귀함수 두 가지 방법으로 풀 수 있었다.

첫 번째 방식은 반복문을 사용한 방식이다. arr[i]의 값이 0부터 i-1까지의 최솟값보다 작거나 같다면 순증가하는 수열을 만들 수 없기 때문에 1을 넣어주고, 그렇지 않다면 findmax함수를 통해서 arr[i]는 arr[l]보다 작고 0과 i-1사이에 가장 긴 증가수열을 찾아서 1을 더한 후에 저장한다.

두 번째 방식은 재귀함수를 이용한 방식이다. 첫 번째 방식에서는 가장 긴 증가수열의 최댓값을 [0, i-1] 에서 찾았다면, 재귀함수를 이용할 때에는 가장 긴 증가수열의 최댓값을 [i+1, n-1] 에서 찾는 것을 볼 수 있다. 방식은 비슷하지만 반복문과 재귀함수의 차이인지, 실행시간이 꽤 차이가 났다. (첫 번째 방식은 12ms, 두 번째 방식은 884ms)