---
title: AOJ-BOARDCOVER
author: qweasfjbv
date: 2020-12-22 19:32:00 +0900
categories: [Algorithm, Problem Solving]
tags: [BruteForce]
toc: false
---

## AOJ BOARDCOVER

<https://www.algospot.com/judge/problem/read/BOARDCOVER>

### Answer

```cpp
#include <iostream>
using namespace std;

char Board[20][20];
int C, H, W;

// BOARD를 왼쪽 위에서부터 덮으면서 내려오기 때문에
// (0, 0) 기준 (0, n) 과 (m, n) (m, n < 0) 은 다 덮여있다고 생각
int type[4][3][2] = { 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 0, 0, 1, 0, 1, -1 };

/*	가독성을 위한 배열 선언
int type[4][3][2] = {
	{{0, 0}, {0, 1}, {1, 0}},
	{{0, 0}, {0, 1}, {1, 1}},
	{{0, 0}, {1, 0}, {1, 1}},
	{{0, 0}, {1, 0}, {1, -1}}
};
*/

// (a, b) 기준으로 t번째 type 블럭이 들어갈 수 있는지 확인
bool CanPut(int a, int b, int t) {

	int a1 = a + type[t][1][0], b1 = b + type[t][1][1];
	int a2 = a + type[t][2][0], b2 = b + type[t][2][1];

	// OutOfRangeError가 나지 않게 범위 먼저 확인 (a, b)는 항상 [0, H(W)-1] 이므로 생략
	if (b2 < 0 || a1 >= H || a2 >= H || b1 >= W || b2 >= W) {
		return false;
	}

	// 각 칸에 #이 하나라도 있으면 들어갈 수 없는 모양이므로 return false, 다 뛰어넘으면 걸리는게 없으므로 return true
	// 이 경우에도 (a, b)는 '.'이어야 함수가 호출되므로 생략

	if (Board[a1][b1] == '#' || Board[a2][b2] == '#') {
		return false;
	}


	return true;

}

// 재귀함수 구현
int Count() {
	int a, b;
	bool once = false;

	for (int i = 0; i < H; i++) {
		for (int j = 0; j < W; j++) {
			if (Board[i][j] == '.') {
				a = i; b = j;	// 타일 기준 (0, 0) 설정
				once = true;
				break;
			}
		}
		if (once) break;
	}

	if (!once) {
		return 1;	// board에 . 이 없어서 꽉 찬 경우 1회 return
	}

	int ret = 0;
	
	for (int i = 0; i < 4; i++) {
		// 4개 차례로 CanPut 으로 확인.
		// true면 #넣고 재귀호출후 .으로 바꿔주기, false면 그냥 continue
		if (CanPut(a, b, i)) {
			Board[a][b] = '#';
			Board[a + type[i][1][0]][b + type[i][1][1]] = '#';
			Board[a + type[i][2][0]][b + type[i][2][1]] = '#';
			ret += Count();
			Board[a][b] = '.';
			Board[a + type[i][1][0]][b + type[i][1][1]] = '.';
			Board[a + type[i][2][0]][b + type[i][2][1]] = '.';
		}
		
	}


	return ret;
}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	cin >> C;
	for (int t = 0; t < C; t++) {
		cin >> H >> W;
		int cnt = 0;

		// Board 입력받기
		for (int i = 0; i < H; i++) {
			for (int j = 0; j < W; j++) {
				cin >> Board[i][j];
				if (Board[i][j] == '.') {
					cnt++;
				}
			}
		}

		if (cnt % 3 == 0) {
			cout << Count() << endl;
		}
		else {
			cout << 0 << endl;
		}

	}



	return 0;
}
```

아무래도 재귀함수를 써야하다보니 함수에서 쓸 변수들은 웬만하면 전역변수를 쓰는게 훨씬 편하다.
어제 실수했던 전역변수 초기화는 입력이 .이든 #이든 들어와서 덮어씌워지기 때문에 할 필요가 없어보여서 하지않았다. 모양을 나타내는데 3차원 배열이 필요할 줄은 상상도 못했다.