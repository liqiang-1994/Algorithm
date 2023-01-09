# 4.寻找两个正序数组的中位数


给定两个大小分别为 `m` 和 `n` 的正序（从小到大）数组 `nums1` 和 `nums2`。请你找出并返回这两个正序数组的 **中位数** 。

算法的时间复杂度应该为 `O(log (m+n))` 。

**示例 1：**

<pre><strong>输入：</strong>nums1 = [1,3], nums2 = [2]
<strong>输出：</strong>2.00000
<strong>解释：</strong>合并数组 = [1,2,3] ，中位数 2
</pre>

**示例 2：**

<pre><strong>输入：</strong>nums1 = [1,2], nums2 = [3,4]
<strong>输出：</strong>2.50000
<strong>解释：</strong>合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
</pre>

**提示：**

* `nums1.length == m`
* `nums2.length == n`
* `0 <= m <= 1000`
* `0 <= n <= 1000`
* `1 <= m + n <= 2000`
* `-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup>`


```cpp
double MedianOfTwoSortedArrays::findMedianSortedArrays(std::vector<int> &nums1, std::vector<int> &nums2) {
    int l1 = 0, l2 = 0, k = 0, m1 = 0, m2 = 0;
    int mid = (nums1.size() + nums2.size()) / 2;
    while (k <= mid && (l1 < nums1.size() || l2 < nums2.size())) {
        m1 = m2;
        if (l1 == nums1.size() || (l1 != nums1.size() && l2 != nums2.size() && nums1[l1] > nums2[l2])) {
            m2 = nums2[l2++];
        } else {
            m2 = nums1[l1++];
        }
        k++;
    }
    return (nums1.size() + nums2.size()) % 2 == 0 ? (double) (m1 + m2) / 2 : (double) m2;
}

```
