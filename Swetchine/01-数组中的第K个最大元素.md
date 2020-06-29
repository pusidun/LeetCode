# 方法1

```C++
bool cmp(int a,int b){
        return a > b;
    }
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end(),cmp);
        return nums[k - 1];
    }
};
```

分析：简单粗暴，从大到小排序后直接选择第k大的数就可以，空间复杂度O(n),时间复杂度O(nlgn)，基本上时间花在排序上。

# 方法2

```C++
class Solution {
public:
  int findKthLargest(vector<int>& nums, int k) {
    return topK(nums, 0, nums.size() - 1, nums.size() - k);
  }
private:
  inline int randomPartition(vector<int>& a, int l, int r) {
        int i = rand() % (r - l + 1) + l;
        swap(a[i], a[r]);
        return partition(a, l, r);
    }
  int topK(vector<int>& nums, int left, int right, int k) {
    int pos = randomPartition(nums, left, right);
    if (pos == k) {
      return nums[k];
    }
    else if (pos > k) {
      return topK(nums, left, pos - 1, k);
    }
    else {
      return topK(nums, pos + 1, right, k);
    }
  }
  int partition(vector<int>& nums, int left, int right) {
    int tail = left - 1;
    for (int i = left; i < right; ++i) {
      if (nums[i] <= nums[right]) {
        swap(nums[i], nums[++tail]);
      }
    }
    swap(nums[right], nums[++tail]);
    return tail;
  }
};
```
分析：快排的分区操作，如果每次规模为 n 的问题我们都划分成 1 和 n - 1，每次递归的时候又向 n - 1的集合中递归，这种情况是最坏的，时间代价是 O(n<sup>2</sup>)。所以引入随机化来加速这个过程，它的时间代价的期望在概率上看来是 O(n)。
