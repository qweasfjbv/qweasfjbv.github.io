---
title: BOJ-N과 M(1-4)
author: qweasfjbv
date: 2020-12-25 23:05:00 +0900
categories: [Algorithm, Problem Solving]
tags: [BackTracking]
toc: true
---

## BOJ N과 M(1)(15649)

<https://www.acmicpc.net/problem/15649>

### Answer

```cpp
#include <iostream>
using namespace std;

int N, M;
int cnt = 0;
bool selected[8] = { false };
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] + 1 << " ";
	}

}

void Make() {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}


	for (int i = 0; i < N; i++) {
		if (!selected[i]) {
			selected[i] = true;
			arr[cnt] = i;
			cnt++;
			Make();
			cnt--;
			selected[i] = false;
		}
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	Make();

	return 0;
}
```

한 번 틀렸는데, arr를 만들 때 크기가 4인 경우를 생각하면서 만들어서 arr의 크기를 4로 만들어버렸다. 신기하게도 이 경우에는 에러가 나지 않았고, 심지어 값이 제대로 나왔다.

## BOJ N과 M(2)(15650)

<https://www.acmicpc.net/problem/15650>

### Answer

```cpp
#include <iostream>
using namespace std;

int N, M;
int cnt = 0;
bool selected[8] = { false };
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] + 1 << " ";
	}

}

void Make(int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}


	for (int i = x; i < N; i++) {
		if (!selected[i]) {
			selected[i] = true;
			arr[cnt] = i;
			cnt++;
			Make(i + 1);
			cnt--;
			selected[i] = false;
		}
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	Make(0);

	return 0;
}
```

(1)에 이어서 바로 (2)를 풀어보니 새로 만들게 거의 없어서 코드를 재사용했다. 그저 재귀함수에 시작점을 인수로 주면 쉽게 구현할 수 있었다.

## BOJ N과 M(3)(15651)

<https://www.acmicpc.net/problem/15651>

### Answer

```cpp
#include <iostream>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] + 1 << " ";
	}

}

void Make() {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}


	for (int i = 0; i < N; i++) {
		arr[cnt] = i;
		cnt++;
		Make();
		cnt--;
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	Make();

	return 0;
}
```

(1)에서 같은 수를 부르지 않게 하기 위해서 만들었던 `bool selected[8]` 과 그와 관련된 모든 것을 지웠다.

## BOJ N과 M(4)(15652)

<https://www.acmicpc.net/problem/15652>

### Answer

```cpp
#include <iostream>
using namespace std;

int N, M;
int cnt = 0;
int arr[8];

void Print() {

	for (int i = 0; i < M; i++) {
		cout << arr[i] + 1 << " ";
	}

}

void Make(int x) {

	if (cnt == M) {
		Print(); cout << "\n"; return;
	}


	for (int i = x; i < N; i++) {
		arr[cnt] = i;
		cnt++;
		Make(i);
		cnt--;
	}
}


int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> N >> M;
	Make(0);

	return 0;
}
```

(1)에서 (2)를 만드는 과정과 비슷했다. (1)에서 (2)로 바꿔줄 때에는 연산의 수를 조금이라도 줄이기 위해서 함수를 호출할 때 Make(i+1)로 호출해 주었지만, 이 경우에는 비내림차순 즉, 같은 수가 나올 수 있으므로 Make(i)로 재귀호출을 해주었다.