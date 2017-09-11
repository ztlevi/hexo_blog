---
title: 'Game theory: Solutions for others'
categories: coding
tags: coding
date: 2017-09-09 15:31:05
---

This post contains solutions for other game theory problems.

Again, I don't have much time putting down a lot of details here...

# Flip game II

- Problem:

https://leetcode.com/problems/flip-game-ii/description/

- Solution:

```python
class Solution(object):
    def canWin(self, s):
        """
        :type s: str
        :rtype: bool
        """
        def search(s):
            if s not in mem:
                mem[s] = any(not search(s[:i] + '--' + s[i+2:]) for i in range(len(s)) if s[i:i+2] == '++')
            return mem[s]
        mem = {}
        return search(s) 
```

<!--more-->

# A Chessboard Game

- Problem:

https://www.hackerrank.com/challenges/a-chessboard-game-1/problem

- Solution (Search):

```python
n = int(input())
pos = []
for i in range(n):
    arr = input().strip().split()
    pos.append(tuple(int(i) for i in arr))


def search(x, y, dp, visited):
    state = False
    if visited[x][y] == True:
        state = dp[x][y]
    else:
        if x-2 > 0 and y+1 < 16 and not search(x - 2, y + 1, dp, visited):
            state = True
        elif x-2 > 0 and y-1 > 0 and not search(x - 2, y - 1, dp, visited):
            state = True
        elif x+1 < 16 and y-2 > 0 and not search(x + 1, y - 2, dp, visited):
            state = True
        elif x-1 > 0 and y -2 > 0 and not search(x - 1, y - 2, dp, visited):
            state = True
    dp[x][y] = state
    visited[x][y] = True
    return dp[x][y]


visited = [[False] * 16 for _ in range(16)]
dp = [[False] * 16 for _ in range(16)]

rst = []
for x, y in pos:
    rst.append(search(x, y, dp, visited))

for r in rst:
    if r:
        print("First")
    else:
        print("Second")
```
