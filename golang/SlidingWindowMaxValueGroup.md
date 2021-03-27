### 题目：大小为K的滑动窗口，从数组nums从左往右滑动（可以默认k比nums长度小），滑动单位为1，返回每次滑动窗口中的最大值的组合。

#### 题解1 关键点：根据窗口界限，选举窗口期内最大值，淘汰过期数据（自己想的一个思路，根据别人的思路延伸的）
```go
package main
import "fmt"
func main() {
	nums := []int{1, 3, 2, -3, 5, 3, 1, 6}
	ret := slidingWindowMax(nums, 4)
	fmt.Print(ret)//3,5,5,5,6
    ret = slidingWindowMax(nums, 3)
	fmt.Print(ret)//3,3,5,5,5,6
    ret = slidingWindowMax(nums, 2)
	fmt.Print(ret)//3,3,2,5,5,3,6
}
func slidingWindowMax(nums []int, k int) []int {
	ret := make([]int, 0)
    	if len(nums) == 0 || k == 1 {
    		return ret
    	}
    	//记录每个数最后一次出现的位置
    	window := make(map[int]int)
    	max := nums[0]
    	var rightWindow int
    	var leftWindow int
    	for i := range nums {
    		if nums[i] > max {
    			max = nums[i]
    		}
    		window[nums[i]] = i
    		rightWindow = i + 1
    		leftWindow = rightWindow - k
    		if rightWindow >= k {
    			//判断是否要重新选举最大值,左窗口位置大于max位置的时候,需要重新选举max
    			if leftWindow > window[max] {
    				delete(window, max)
    				//重新选举最大值并清除掉历史窗口的记录
    				max = nums[i]
    				for v, index := range window {
    					if i-index > k {
    						delete(window, v)
    					} else if v > max {
    						max = v
    					}
    				}
    			}
    			ret = append(ret, max)
    		}
    	}
    	return ret
}
```
#### 常规做法，双重循环
```go
package main
func maxSlidingWindow(nums []int, k int) []int {
	length := len(nums)
	i := 0
	ret := make([]int, 0)
	for i < length {
		m := nums[i]
		if i > length - k {
			break
		}
		for j := i + 1; j < i + k; j++ {
			if m < nums[j] {
				m = nums[j]
			}
		}
		ret = append(ret,m)
		i++
	}
	return ret
}
```
