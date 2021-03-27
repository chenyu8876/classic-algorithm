### 题目简单：123 转成 321，1234 转成 4321

#### 思路：循环乘以️10 + 取余 	
##### 1234 -> 4321 = 432 * 10 + 1 = (43 * 10 + 2) * 10 + 1 = ((4*10+3) * 10 + 2) * 10 +1

```go
package main
import (
	"fmt"
    "math"
)
func main() {
	num := reverse(1234)
    fmt.Print(num)
	
}

func reverse(x int) (num int) {
	for x != 0 {
		num = num*10 + x%10
		x = x / 10
	}
	// 使用 math 包中定义好的最大最小值
	if num > math.MaxInt32 || num < math.MinInt32 {
		return 0
	}
	return
}
```