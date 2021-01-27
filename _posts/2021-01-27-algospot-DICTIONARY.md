---
title: AOJ-DICTIONARY
author: qweasfjbv
date: 2021-01-27 18:01:00 +0900
categories: [Algorithm, Problem Solving]
tags: [GraphTheory]
toc: false
---

## AOJ DICTIONARY

<https://www.algospot.com/judge/problem/read/DICTIONARY>

### Answer

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
#include <cstring>
using namespace std;

vector<string> dic;
vector<int> ans;
bool link[26][26] = { false };
bool checked[26] = { false };

// a->b 면 link[0][1] = true; link[1][0] = false;
void drawGraph(int a, int b) {
	int len = min(dic[a].size(), dic[b].size());
	int same = -1;

	for (int i = 0; i < len; i++) {
		if (dic[a][i] != dic[b][i]) {
			same = i;
			break;
		}
	}

	if (same == -1) return;
	else {
		link[(char)dic[a][same] - 97][(char)dic[b][same] - 97] = true;
		return;
	}
}

// 다음 테스트케이스를 위해 전역변수 초기화하기
void reset() {

	while (!dic.empty()) {
		dic.pop_back();
	}
	memset(link, 0, 26 * 26 * sizeof(bool));
	memset(checked, 0, 26 * sizeof(bool));

	return;
}

void dfs(int ind) {

	checked[ind] = true;
	for (int i = 0; i < 26; i++) {
		if (link[ind][i] && !checked[i]) {
			dfs(i);
		}
	}

	ans.push_back(ind);

}

bool Sort() {

	for (int i = 0; i < 26; i++) {
		if (!checked[i]) dfs(i);
	}

	reverse(ans.begin(), ans.end());

	bool check = true;
	
	for (int i = 0; i < 26; i++) {
		for (int j = i + 1; j < 26; j++) {
			if (link[ans[j]][ans[i]]) {
				return false;
			}
		}
	}

	return check;

}

int main() {

	cin.tie(0);
	ios::sync_with_stdio(0);

	int T, N;
	cin >> T;

	string s;
	for (int t = 0; t < T; t++) {
		cin >> N;
		for (int i = 0; i < N; i++) {
			cin >> s;
			dic.push_back(s);
		}

		for (int i = 0; i < dic.size()-1; i++) {
			drawGraph(i, i + 1);
		}

		if (Sort()) {
			for (int i = 0; i < 26; i++) {
				cout << (char)(ans[i] + 'a');
			}
			cout << '\n';
		}
		else {
			cout << "INVALID HYPOTHESIS\n";
		}

		reset();
	}


	return 0;
}
```

DFS를 이용해 ans에 고대어를 사전순으로 정렬하고 모순된 건 없는지 확인해주었다.

사전순으로 정렬하기 위해서는 bool형 2차원 배열 `bool link[26][26]` 에 관계를 정리하고, DFS를 이용해서 문자를 ans에 push_back 해준 뒤에 reverse로 뒤집어주면 되었다.

`INVALID HYPOTHESIS` 인지아닌지를 확인하기 위해서는 이렇게 사전순으로 정렬된 ans에서 뒤의 문자에서 앞의 문자로 link 되어있는지 확인했다.