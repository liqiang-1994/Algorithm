# 5.最长回文子串

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

**示例 1：**

<pre><strong>输入：</strong>s = "babad"
<strong>输出：</strong>"bab"
<strong>解释：</strong>"aba" 同样是符合题意的答案。
</pre>

**示例 2：**

<pre><strong>输入：</strong>s = "cbbd"
<strong>输出：</strong>"bb"
</pre>

**提示：**

* `1 <= s.length <= 1000`
* `s` 仅由数字和英文字母组成

```cpp
std::string longestPalindrome(std::string s) {
    int n = s.size();
    if (n < 2) {
        return s;
    }
    int maxLen = 1;
    int begin = 0;
    // dp[i][j] 表示 s[i..j] 是否是回文串
    std::vector<std::vector<bool>> dp(n, std::vector<bool>(n));
    // 初始化：所有长度为 1 的子串都是回文串
    for (int i = 0; i < n; i++) {
        dp[i][i] = true;
    }
    // 递推开始
    // 先枚举子串长度
    for (int L = 2; L <= n; L++) {
        for (int i = 0; i < n; i++) {
            // 由 L 和 i 可以确定右边界，即 j - i + 1 = L 得
            int j = L + i - 1;
            // 如果右边界越界，就可以退出当前循环
            if (j >= n) {
                break;
            }
            if (s[i] != s[j]) {
                dp[i][j] = false;
            } else {
                if (j - i < 3) {
                    dp[i][j] = true;
                } else {
                    dp[i][j] = dp[i + 1][j - 1];
                }
            }
            if (dp[i][j] && L > maxLen) {
                maxLen = L;
                begin = i;
            }
        }
    }
    return s.substr(begin, maxLen);
}
```
