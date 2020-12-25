---
title: BOJ-N과 M(9-12)
author: qweasfjbv
date: 2020-12-25 23:05:00 +0900
categories: [Algorithm, Problem Solving]
tags: [BackTracking]
toc: true
---

## BOJ N과 M(9)(15663)

<https://www.acmicpc.net/problem/15663>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
int Get[8];
int Cnt[8] = { 0 };

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make() {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = 0; i < N; i++) {
		if (Cnt[i] != 0) {
			arr[cnt] = Get[i];
			Cnt[i]--;
			cnt++;
			Make();
			cnt--;
			Cnt[i]++;
		}
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	vector<int> v(N);
	for (int i = 0; i < N; i++) {
		cin >> v[i];
	}
	sort(v.begin(), v.end());

	int point = 0;
	Get[0] = v[0];
	Cnt[0] = 1;

	for (int i = 1; i < N; i++) {	
		if (v[i] == v[i - 1]) { Cnt[point]++; }
		else {
			point++;
			Get[point] = v[i];
			Cnt[point] = 1;
		}
	}


	Make();

	return 0;
}
```

입력이 달라졌다. 이전까지는 중복되는 수가 들어오지 않았지만 중복되는 수가 들어오기 시작했고, 출력도 중복되지 않아야 했기 때문에 'bool selected[8]' 대신에 'int Cnt[8]'을 사용해서 다른 숫자로 받아들이지 않되, 여러 개 사용할 수 있도록 만들었다.

## BOJ N과 M(10)(15664)

<https://www.acmicpc.net/problem/15664>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
int Get[8];
int Cnt[8] = { 0 };

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = x; i < N; i++) {
		if (Cnt[i] != 0) {
			arr[cnt] = Get[i];
			Cnt[i]--;
			cnt++;
			Make(i);
			cnt--;
			Cnt[i]++;
		}
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	vector<int> v(N);
	for (int i = 0; i < N; i++) {
		cin >> v[i];
	}
	sort(v.begin(), v.end());

	int point = 0;
	Get[0] = v[0];
	Cnt[0] = 1;

	for (int i = 1; i < N; i++) {	
		if (v[i] == v[i - 1]) { Cnt[point]++; }
		else {
			point++;
			Get[point] = v[i];
			Cnt[point] = 1;
		}
	}


	Make(0);

	return 0;
}
```

까다로워진 입력과는 다르게 변형하는건 이전과 똑같았다. 비내림차순 이라는 조건이 추가되었기 때문에 시작하는 곳을 가리키는 인자를 하나 추가해 주었다.

## BOJ N과 M(11)(15665)

<https://www.acmicpc.net/problem/15665>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
int Get[8];
int Cnt[8] = { 0 };
int point = 0;

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make() {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = 0; i < point+1; i++) {
		arr[cnt] = Get[i];
		cnt++;
		Make();
		cnt--;
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	vector<int> v(N);
	for (int i = 0; i < N; i++) {
		cin >> v[i];
	}
	sort(v.begin(), v.end());

	Get[0] = v[0];
	Cnt[0] = 1;

	for (int i = 1; i < N; i++) {	
		if (v[i] == v[i - 1]) { Cnt[point]++; }
		else {
			point++;
			Get[point] = v[i];
			Cnt[point] = 1;
		}
	}


	Make();

	return 0;
}
```

개수에 대한 조건이 사라졌다. 1, 7, 9, 9 가 주어진다고 하면 9가 두 개고, 7이 한 개라는 사실이 중요한게 아니라, 1, 7, 9라는 수가 있다 라는게 중요했다. 그래서 'Cnt[8] = { 0 }' 에 대한 실행문을 지웠다. (일부는 내 생각이 틀렸을까봐 무서워서 지우지 못했다.)

## BOJ N과 M(12)(15666)

<https://www.acmicpc.net/problem/15666>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
int Get[8];
int Cnt[8] = { 0 };
int point = 0;

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = x; i < point+1; i++) {
		arr[cnt] = Get[i];
		cnt++;
		Make(i);
		cnt--;
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	vector<int> v(N);
	for (int i = 0; i < N; i++) {
		cin >> v[i];
	}
	sort(v.begin(), v.end());

	Get[0] = v[0];
	Cnt[0] = 1;

	for (int i = 1; i < N; i++) {	
		if (v[i] == v[i - 1]) { Cnt[point]++; }
		else {
			point++;
			Get[point] = v[i];
			Cnt[point] = 1;
		}
	}


	Make(0);

	return 0;
}
```

비내림차순으로 만들기 위해서 함수에 인자를 넣었다.