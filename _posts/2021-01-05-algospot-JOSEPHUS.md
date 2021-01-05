---
title: AOJ-JOSEPHUS
author: qweasfjbv
date: 2021-01-05 17:34:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DataStructures]
toc: false
---

## AOJ JOSEPHUS

<https://www.algospot.com/judge/problem/read/JOSEPHUS>

### Answer

```cpp
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;

int main() {

	int C, N, K;
	cin >> C;
	for (int t = 0; t < C; t++) {

		cin >> N >> K;
		queue<int> Q;

		for (int i = 1; i < N + 1; i++) Q.push(i);

		while (Q.size() > 2) {

			int tmp;
			// 한 명 자살
			Q.pop();
			// 순서 넘기기
			for (int i = 0; i < K-1; i++) {
				tmp = Q.front();
				Q.pop();
				Q.push(tmp);
			}


		}

		int a = Q.front(), b = Q.back();
		
		cout << min(a, b) << " " << max(a, b) << '\n';

	}

	return 0;
}
```

큐를 이용해서 답을 만들어봤다. 한 명이 자살하고, 그 다음 K번째 순서까지 다시 뒤로 보낸 후에 또 자살하도록 만들었다.

책에서는 연결리스트로 구현했는데, `iterator`가 뭔지 몰라서 따라할 수가 없었다.