#### 	Day-1 两数之和 

```
//1 两书之和 暴力 哈希表
func twoSum(nums []int, target int) []int {
	hashMap := map[int]int{}
	for i := 0; i < len(nums); i++ {
		hashMap[nums[i]] = i
	}

	for i := 0; i < len(nums); i++ {
		if p, ok := hashMap[target-nums[i]]; ok && p != i {
			return []int{p, i}
		}
	}
	return nil
}

```



#### Day-2.1无重复最长子串

```
func lengthOfLongestSubstring(s string) int {
    // 哈希集合，记录每个字符是否出现过
    m := map[byte]int{}
    n := len(s)
    // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
    rk, ans := -1, 0
    for i := 0; i < n; i++ {
        if i != 0 {
            // 左指针向右移动一格，移除一个字符
            delete(m, s[i-1])
        }
        for rk + 1 < n && m[s[rk+1]] == 0 {
            // 不断地移动右指针
            m[s[rk+1]]++
            rk++
        }
        // 第 i 到 rk 个字符是一个极长的无重复字符子串
        ans = max(ans, rk - i + 1)
    }
    return ans
}

func max(x, y int) int {
    if x < y {
        return y
    }
    return x
}


```

#### Day2.2最长回文子串

```go
func longestPalindrome(s string) string {
    start, end := 0, -1
    t := "#"
    for i := 0; i < len(s); i++ {
        t += string(s[i]) + "#"
    }
    t += "#"
    s = t
    arm_len := []int{}
    right, j := -1, -1
    for i := 0; i < len(s); i++ {
        var cur_arm_len int
        if right >= i {
            i_sym := j * 2 - i
            min_arm_len := min(arm_len[i_sym], right-i)
            cur_arm_len = expand(s, i-min_arm_len, i+min_arm_len)
        } else {
            cur_arm_len = expand(s, i, i)
        }
        arm_len = append(arm_len, cur_arm_len)
        if i + cur_arm_len > right {
            j = i
            right = i + cur_arm_len
        }
        if cur_arm_len * 2 + 1 > end - start {
            start = i - cur_arm_len
            end = i + cur_arm_len
        }
    }
    ans := ""
    for i := start; i <= end; i++ {
        if s[i] != '#' {
            ans += string(s[i])
        }
    }
    return ans
}

func expand(s string, left, right int) int {
    for ; left >= 0 && right < len(s) && s[left] == s[right]; left, right = left-1, right+1 { }
    return (right - left - 2) / 2
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}

```



#### Day2.3 [ 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

```go
func maxArea(height []int) int {
	n := len(height)
	ans := 0
	i, j := 0, n-1
	for i < n && i < j {
		temp := min(height[i], height[j])
		ans = max(ans, temp*(j-i))
		if height[i] <= height[j] {
			i++
		} else {
			j--
		}
	}
	return ans
}
func min(x int, y int) int {
	if x < y {
		return x
	}
	return y
}

func max(x int, y int) int {
	if x > y {
		return x
	}
	return y
}

```

#### Day2.4 整数的反转

```go

func reverse(x int) (rev int) {
	for x != 0 {
		if rev < math.MinInt32/10 || rev > math.MaxInt32/10 {
			return 0
		}
		digit := x % 10
		x /= 10
		rev = rev*10 + digit
	}
	return
}

```



#### 2.5 最长公共前缀

```go

```

#### 
