---
title: Leetcode 121 - Best Time to Buy and Sell Stock - Easy
author: Sanh Doan
date: 2022-04-11 10:44:00 +0700
categories: [Algorithm, Two Pointers]
tags: [Algorithm, Two Pointers, easy]
---

### Leetcode link

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

Cho 1 mảng các số nguyên `prices`, với số `prices[i]` tương ứng giá stock của ngày thứ `i`. Hãy tính ra giá lợi nhuận cao nhất bằng cách chọn 1 ngày để mua stock và chọn 1 ngày (lớn hơn ngày mua) để bán stock và trừ 2 giá trị đó với nhau

Ví dụ: prices = [6,2,4,3,1,3,2,5]

![leetcode121-diagram](/assets/img/pages/leetcode121-diagram.png)

| Step | left | right | Mua | Bán | Profit | Max profit |
| :--: | :--: | :---: | :-: | :-: | :----: | :--------: |
|  1   |  0   |   1   |  6  |  2  |   x    |     0      |
|  2   |  1   |   2   |  2  |  4  |   2    |     2      |
|  3   |  1   |   3   |  2  |  3  |   1    |     2      |
|  4   |  1   |   4   |  2  |  1  |   x    |     2      |
|  5   |  4   |   5   |  1  |  3  |   2    |     2      |
|  6   |  4   |   6   |  1  |  2  |   1    |     2      |
|  7   |  4   |   7   |  1  |  5  |   4    |     4      |

Time complexity: O(n)
Space complexity: O(1)

# Code Golang

```go
func maxProfit(prices []int) int {
  l := 0
  r := 1

  maxProfit := 0
  maxIndex := len(prices) - 1

  for {
    if r > maxIndex {
      break
    }

    profit := prices[r] - prices[l]
    if profit < 0 {
      l = r
    } else {
      maxProfit = max(maxProfit, profit)
    }
    r += 1
  }
  return maxProfit
}

func max(a, b int) int {
  if a > b {
      return a
  }
  return b
}
```

# Code Python

```python
def maxProfit(self, prices: List[int]) -> int:
  l = 0
  r = 1
  maxProfit = 0

  while r < len(prices):
    profit = prices[r] - prices[l]
    if profit >= 0:
      maxProfit = max(maxProfit, profit)
    else:
      l = r
    r +=
  return maxProfit
```
