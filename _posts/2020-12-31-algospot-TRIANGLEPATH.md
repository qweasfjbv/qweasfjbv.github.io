---
title: AOJ-TRIANGLEPATH
author: qweasfjbv
date: 2020-12-31 18:04:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DynamicProgramming]
toc: false
---

## AOJ TRIANGLEPATH

<https://www.algospot.com/judge/problem/read/TRIANGLEPATH>

### Answer-1

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int n, tri[100][100];
int cache[100][100];

int Count(int a, int b) {

	if (a == n - 1) return tri[a][b];

	int& ret = cache[a][b];
	if (ret != -1) return ret;

	ret = max(Count(a + 1, b), Count(a + 1, b + 1)) + tri[a][b];
	return ret;

}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	int C;
	cin >> C;

	for (int t = 0; t < C; t++) {

		for (int i = 0; i < 100; i++) {
			for (int j = 0; j < 100; j++) {
				cache[i][j] = -1;
			}
		}

		cin >> n;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j <= i; j++) {
				cin >> tri[i][j];
			}
		}

		cout << Count(0, 0) << "\n";

	}


	return 0;
}
```

### Answer-2

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int n, tri[100][100];

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	int C;
	cin >> C;

	for (int t = 0; t < C; t++) {

		cin >> n;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j <= i; j++) {
				cin >> tri[i][j];
			}
		}

		for (int i = 1; i < n; i++) {
			for (int j = 0; j <= i; j++) {
				if (j == 0) {
					tri[i][j] += tri[i - 1][0];
				}
				else if (j == i) {
					tri[i][j] += tri[i - 1][i - 1];
				}
				else {
					tri[i][j] += max(tri[i - 1][j - 1], tri[i - 1][j]);
				}
			}
		}

		int m = -1;
		for (int i = 0; i < n; i++) {
			m = max(m, tri[n - 1][i]);
		}

		cout << m << "\n";

	}


	return 0;
}
```

두 가지 방법으로 구현해봤다. 첫 번째 방법은 책에서 소개한 방법으로, 재귀함수와 메모이제이션을 통해 구현한 것이다. (a, b)를 기준으로 아래에 있는 두 수중 큰 수를 맨 아래에서부터 더하면서 올라가는 방법이다.

두 번째 방법은 (a, b)를 기준으로 위에 있는 두 수 중 큰 수를 더해가며 맨 위에서부터 아래로 내려가는 방법이다. 첫 번째 방식과 다르게 반복문으로 구현했고, tri배열에 바로바로 저장하기 때문에 메모이제이션이 따로 필요하지 않았다.