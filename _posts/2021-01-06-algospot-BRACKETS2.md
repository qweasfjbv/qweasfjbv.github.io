---
title: AOJ-BRACKETS2
author: qweasfjbv
date: 2021-01-06 19:09:00 +0900
categories: [Algorithm, Problem Solving]
tags: [DataStructures]
toc: false
---

## AOJ BRACKETS2

<https://www.algospot.com/judge/problem/read/BRACKETS2>

### Answer

```cpp
#include <iostream>
#include <string>
#include <stack>
using namespace std;

int main() {

	string tmp;
	stack<char> S;

	int C;
	cin >> C;
	for (int t = 0; t < C; t++) {
		cin >> tmp;
		
		while (!S.empty()) {
			S.pop();
		}

		bool printed = false;
		for (int i = 0; i < tmp.size(); i++) {
			if (tmp[i] == '(' || tmp[i] == '[' || tmp[i] == '{') {
				S.push(tmp[i]);
			}
			else if (tmp[i] == ')') {
				if (!S.empty() && S.top() == '(') {
					S.pop();
				}
				else {
					cout << "NO\n";
					printed = true;
					break;
				}
			}
			else if (tmp[i] == '}') {
				if (!S.empty() && S.top() == '{') {
					S.pop();
				}
				else {
					cout << "NO\n";
					printed = true;
					break;
				}

			}
			else if (tmp[i] == ']') {
				if (!S.empty() && S.top() == '[') {
					S.pop();
				}
				else {
					cout << "NO\n";
					printed = true;
					break;
				}
			}



		}

		if (!printed) {
			if (S.empty()) cout << "YES\n";
			else { cout << "NO\n"; }
		}
	}



	return 0;
}
```

스택을 사용하는 괄호 관련 문제였다. (, [, { 의 경우에는 스택에 push 하면 되고, ), ], } 는 스택에서 짝을 맞춰서 pop 을 해주면 된다.

나는 한 번 틀렸다. 스택에서 짝을 맞춰서 pop을 해줄 때 S.top()으로 스택 맨 위의 걸 검사했는데, 여기서 스택이 비어있으면 -1이나 0 같은 수가 나올거라고 생각했지만 런타임오류가 발생했다. 그래서 앞에 !S.empty() 를 붙여서 만약 비어있으면 그 뒤를 검사하지 않도록 했다.