# 3.无重复字符的最长子串


给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串 **的长度。

**示例 1:**

<pre><strong>输入: </strong>s = "abcabcbb"
<strong>输出: </strong>3 
<strong>解释:</strong> 因为无重复字符的最长子串是 <code>"abc"，所以其</code>长度为 3。
</pre>

**示例 2:**

<pre><strong>输入: </strong>s = "bbbbb"
<strong>输出: </strong>1
<strong>解释: </strong>因为无重复字符的最长子串是 <code>"b"</code>，所以其长度为 1。
</pre>

**示例 3:**

<pre><strong>输入: </strong>s = "pwwkew"
<strong>输出: </strong>3
<strong>解释: </strong>因为无重复字符的最长子串是 <code>"wke"</code>，所以其长度为 3。
     请注意，你的答案必须是 <strong>子串 </strong>的长度，<code>"pwke"</code> 是一个<em>子序列，</em>不是子串。</pre>


```cpp
int lengthOfLongestSubstring(std::string s) {
    std::unordered_set<char> set;
    std::unordered_map<char, int> map;
    int n = s.size();
    int p = -1, temp =0;
    int start = 0, max = 0;
    for (int i = 0; i < n; i++) {
        if (map.find(s[i])!=map.end()) {
            start = std::max(start, map[s[i]] + 1);
            map[s[i]]=i;
            max = std::max(max, i - start + 1);
        } else {
            max = std::max(max, i - start + 1);
            map.insert({s[i], i});
        }

//        if (i != 0) {
//            set.erase(s[i - 1]);
//        }
//        while (p + 1 < n && !set.count(s[p + 1])) {
//            set.insert(s[p + 1]);
//            ++p;
//        }
//        temp = std::max(temp, p - i + 1);
    }
    return max;
}
```
