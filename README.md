# trapping rain water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

## Examples

```
Example 1:


Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
Example 2:

Input: height = [4,2,0,3,2,5]
Output: 9
 

Constraints:

n == height.length
1 <= n <= 2 * 104
0 <= height[i] <= 105
```
## 解析

首先知道 要算出累積水位 就必須找出左邊的區域最大值還有右邊的區域最大值

一樣可以從左界以及右界比叫出比較小的那個 Height 

如果比較小邊的是左界 把左界向右移

如果比較小邊的是右界 把右界向左移

直到左右界交會為止

## 實作

```golang
package trapping_rain

func trap(height []int) int {

	lp := 0
	rp := len(height) - 1
	l_max := 0
	r_max := 0
	result := 0
	for lp < rp {
		if height[lp] < height[rp] {
			if height[lp] > l_max {
				l_max = height[lp]
			} else {
				result += l_max - height[lp]
			}
			lp++
		} else {
			if height[rp] > r_max {
				r_max = height[rp]
			} else {
				result += r_max - height[rp]
			}
			rp--
		}
	}
	return result
}

```