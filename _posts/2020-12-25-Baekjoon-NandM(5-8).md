---
title: BOJ-N과 M(5-8)
author: qweasfjbv
date: 2020-12-25 23:05:00 +0900
categories: [Algorithm, Problem Solving]
tags: [BackTracking]
toc: true
---

## BOJ N과 M(5)(15654)

<https://www.acmicpc.net/problem/15654>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
bool selected[8] = { false };

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(vector<int>& v) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = 0; i < N; i++) {
		if (!selected[i]) {
			selected[i] = true;
			arr[cnt] = v[i];
			cnt++;
			Make(v);
			cnt--;
			selected[i] = false;
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
	Make(v);

	return 0;
}
```

vector는 정렬하기 위해서 전역변수로 만들지 않았고, 그래서 함수에 인자로 vector를 레퍼런스로 넘겨주었다.
나머지는 전에 했던 것들과 마찬가지로, 'bool selected[8]' 을 만들어서 중복되지 않도록 만들어주고, 재귀함수 내 반복문에서 i를 필요한 부분에 한해서 v[i]로 바꾸어주면 된다.

## BOJ N과 M(6)(15655)

<https://www.acmicpc.net/problem/15655>

### Answer
```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];
bool selected[8] = { false };

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(vector<int>& v, int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = x; i < N; i++) {
		if (!selected[i]) {
			selected[i] = true;
			arr[cnt] = v[i];
			cnt++;
			Make(v, i + 1);
			cnt--;
			selected[i] = false;
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
	Make(v, 0);

	return 0;
}
```

위에서 한 내용의 반복이었다. 오름차순을 만들기 위해서 시작하는 위치를 위한 인자를 받도록 만들었다.

## BOJ N과 M(7)(15656)

<https://www.acmicpc.net/problem/15656>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(vector<int>& v) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = 0; i < N; i++) {
		arr[cnt] = v[i];
		cnt++;
		Make(v);
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
	Make(v);

	return 0;
}
```

지겹게 반복이다. 또 중복이 허용되었기에 'bool selected[8]' 에 대한 모든 실행문을 지우고 오름차순이라는 조건도 사라져서 반복문을 시작하는 부분을 지시하는 인자도 지웠다.

## BOJ N과 M(8)(15657)

<https://www.acmicpc.net/problem/15657>

### Answer

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] << " ";
	}

}

void Make(vector<int>& v, int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}



	for (int i = x; i < N; i++) {
		arr[cnt] = v[i];
		cnt++;
		Make(v, i);
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
	Make(v, 0);

	return 0;
}
```

비내림차순을 구현하기 위해서 인자를 다시 만들어주고 재귀호출을 Make(v, i)로 불러서 중복될 수 있도록 했다.
