## hash

#### 1 两数之和
```go
func twoSum(nums []int, target int) []int {
    hash := make(map[int]int)
    for i, v := range nums {
        if p, ok := hash[target - v]; ok {
            return []int{i, p}
        }
        hash[v] = i
    }
    return nil
}
```
#### 49	字母异位词分组
```go
func groupAnagrams(strs []string) [][]string {
    var res [][]string
    hash := make(map[[26]int][]string)
    for _, s := range strs {
        var arr [26]int
        for i := 0; i < len(s); i++ {
            arr[s[i] - 'a']++
        }
        hash[arr] = append(hash[arr], s)
    }
    for _, s := range hash {
        res = append(res, s)
    }
    return res
}
```
#### 76 最小覆盖子串
```go
func minWindow(s string, t string) string {
    sArr, tArr := make([]int, 128), make([]int, 128)
    for i := range t {
        tArr[t[i] - 'A']++
    }
    left, right, length := 0, -1, len(s) + 1
    for i, j := 0, 0; j < len(s); j++ {
        sArr[s[j] - 'A']++
        for equal(sArr, tArr) {
            if length > j - i + 1 {
                length = j - i + 1
                left = i
                right = j
            }
            sArr[s[i] - 'A']--
            i++
        }
    }
    return s[left:right+1]
}

func equal(sArr, tArr []int) bool {
    for i := 0; i < 128; i++ {
        if sArr[i] < tArr[i] {
            return false
        }
    }
    return true
}
```