---
title: AOJ-PICNIC
author: qweasfjbv
date: 2020-12-21 21:53:00 +0900
categories: [Algorithm, Problem Solving]
tags: [BruteForce]
toc: false
---

## AOJ PICNIC

<https://www.algospot.com/judge/problem/read/PICNIC>

처음엔 반복문으로 할려 했는데 도저히 안풀려서 재귀함수로 구현했다.

### Wrong Code

{% raw %}
```cpp
#include <iostream>
using namespace std;

bool isFriend[10][10] = { false };
bool hasPartner[10] = { false };

int Match(int n) {
	int start = -1;
	for (int i = 0; i < n; i++) {
		if (!hasPartner[i]) {
			start = i;
			break;
		}
	}

	if(start == -1) return 1;

	int ret = 0;
	// 짝꿍 찾기
	for (int i = start + 1; i < n; i++) {
		// start와 친구이고 짝이 없는 사람이어야 함.
		if (!hasPartner[i] && isFriend[i][start]) {
			hasPartner[i] = true;
			hasPartner[start] = true;
			ret += Match(n);
			hasPartner[i] = false;
			hasPartner[start] = false;
		}
	}

	return ret;

}


int main() {

	int C, n, m;

	cin >> C;

	int a, b;
	for (int t = 0; t < C; t++) {
		cin >> n >> m;
		for (int i = 0; i < 10; i++) {
			hasPartner[i] = false;
		}

		for (int i = 0; i < m; i++) {
			cin >> a >> b;
			isFriend[a][b] = true;
			isFriend[b][a] = true;
		}

		cout << Match(n) << endl;


	}



	return 0;
}
```
{% endraw %}

하지만 이 코드는 틀렸다.
왜 틀렸는지 보니 전역변수로 선언해준 isFriend를 각 TestCase마다 false로 초기화를 해주지 않아서 잘못된 값을 얻게된 듯 하다.

### Answer

{% raw %}
```cpp
#include <iostream>
using namespace std;

// 친구관계 기록하기 위한 배열과 현재 파트너가 있는지 적어두기 위한 배열
bool isFriend[10][10] = { false };
bool hasPartner[10] = { false };

int Match(int n) {
	int start = -1;
	for (int i = 0; i < n; i++) {
		if (!hasPartner[i]) {
			start = i;
			break;
		}
	}

	if(start == -1) return 1;

	int ret = 0;
	// 짝꿍 찾기
	for (int i = start + 1; i < n; i++) {
		// start와 친구이고 짝이 없는 사람이어야 함.
		if (!hasPartner[i] && isFriend[i][start]) {
			hasPartner[i] = true;
			hasPartner[start] = true;
			ret += Match(n);
			hasPartner[i] = false;
			hasPartner[start] = false;
		}
	}

	return ret;

}


int main() {

	int C, n, m;

	cin >> C;

	int a, b;
	for (int t = 0; t < C; t++) {
		cin >> n >> m;
		// 전역변수 초기화
		for (int i = 0; i < 10; i++) {
			hasPartner[i] = false;
		}
		for (int i = 0; i < 10; i++) {
			for (int j = 0; j < 10; j++) {
				isFriend[i][j] = false;
			}
		}

		for (int i = 0; i < m; i++) {
			cin >> a >> b;
			// 친구관계 기록
			isFriend[a][b] = true;
			isFriend[b][a] = true;
		}

		cout << Match(n) << endl;


	}



	return 0;
}
```
{% endraw %}

전역변수를 초기화하니 문제를 맞출 수 있었다.