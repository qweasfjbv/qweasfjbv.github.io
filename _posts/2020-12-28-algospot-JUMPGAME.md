---
title: AOJ-JUMPGAME
author: qweasfjbv
date: 2020-12-28 15:49:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DynamicProgramming]
toc: false
---

## AOJ JUMPGAME

<https://www.algospot.com/judge/problem/read/JUMPGAME>

### Answer

```cpp
#include <iostream>
using namespace std;

int map[100][100];
// 기본적으로 -1, false면 0, true면 1
int pos[100][100];
int N;

// 오른쪽이나 왼쪽으로만 진행
bool Jump(int a, int b) {

	// 목적지에 도착했으면 
	if (a == N - 1 && b == N - 1) return true;

	if (a >= N || b >= N) return false;

	if (pos[a][b] != -1) return pos[a][b];


	bool ret = (Jump(a + map[a][b], b) || Jump(a, b + map[a][b]));
	
	if (ret == true) pos[a][b] = 1;
	else pos[a][b] = 0;

	return ret;

}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	int C;
	cin >> C;
	for (int t = 0; t < C; t++) {
		cin >> N;
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < N; j++) {
				pos[i][j] = -1;
				cin >> map[i][j];
			}
		}

		if (Jump(0, 0)) {
			cout << "YES" << endl;
		}
		else {
			cout << "NO" << endl;
		}

	}


	return 0;
}
```

항상 점프를 오른쪽이나 아래로만 할 수 있었기 때문에 간단하게 구할 수 있었다. 또한, 메모이제이션을 통해 시간을 단축시켰다.