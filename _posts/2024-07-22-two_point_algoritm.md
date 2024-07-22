---
layout: single
title:   "투포인터 알고리즘(two_pointer algoritm)"
categories: Algoritm
toc: true
author_profile : false
---

💡 **주로 사용되는 경우**

1. **배열이 정렬**되어 있을 때 특정 조건을 만족하는 요소 찾기
2. **연속된 부분 배열을 탐색**하는 문제

---

## 개요

- 두 개의 포인터를 사용하여 배열이나 리스트의 서로 다른 위치를 가리켜, 배열을 탐색
    - 대개는 시작점과 끝점 또는 왼쪽 포인터와 오른쪽 포인터 두 지점을 기준으로 하는 문제풀이 전략
    - **범위를 좁혀 나가기 위해서, 일반적으로 배열이 정렬되어 있을 때 유용.**
- 알고리즘의 기본 개념이라기 보다 실전적인 풀이 기법으로, 일반적인 알고리즘 교과서에는 등장하지 않음
- 투 포인터는 그림과 같이 주로 정렬된 배열을 대상으로, 2개의 포인터가 좌우로 자유롭게 움직이며 문제를 풀이하여, 투 포인터라는 이름이 붙었다.

<img width="393" alt="Untitled" src="https://github.com/user-attachments/assets/188d9e22-1a68-4a17-8002-577823d8a873">

## 시간복잡도

- 정렬된 배열에서 두수의 합 찾기 : O(n)
    - 배열을 한번 순회하여 문제해결
- 연속된 부분의 배열의 합 찾기 : O(n)
    - 배열을 한번 순회하여 문제해결

## 사용예

- [백준_실버4_2003_수들의 합2](https://jamm0316.github.io/coding_test/baek_joon_2003/)

---

- 참고사항
    - [Sliding Window (슬라이딩 윈도우](https://www.notion.so/Sliding-Window-7d85bf6c85ce4af683eecad93c1218d5?pvs=21))
