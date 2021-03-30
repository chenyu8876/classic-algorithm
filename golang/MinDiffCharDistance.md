### 题目：将字符串A变成字符串B的最少操作次数，操作有插入、删除、替换，如"chen"和"chenyu"的最小距离为2

#### 这题最重要思想是画矩阵和利用公式求出矩阵右下角的值，算法啊到最后都是数学，本学渣哭了，有兴趣的可以去看这篇文章挺不错的
#### https://www.jianshu.com/p/a617d20162cf

#### 动态规划问题统统死记硬背方程式

```go
package main
import (
	"fmt"
)
func main() {
	num := minDistance("chenyu","chen")
    fmt.Print(num)
	
}

func minDistance(char1, char2 string) int {
	l1, l2 := len(char1), len(char2)
	dp := make([][]int, l1+1)
	dp[0] = make([]int, l2+1)
	for j := 0; j <= l2; j++ {
		dp[0][j] = j
	}

	for i := 1; i <= l1; i++ {
		dp[i] = make([]int, l2+1)
		dp[i][0] = i
		for j := 1; j <= l2; j++ {
			if char1[i-1] == char2[j-1] {
				dp[i][j] = dp[i-1][j-1]
			} else {
				dp[i][j] = MinThree(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
			}
		}
	}
	return dp[l1][l2]
}

func MinThree(a, b, c int) (min int) {
	if a >= b {
		min = b
	} else {
		min = a
	}
	if min >= c {
		min = c
	}
    return
}
```
