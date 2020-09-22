## 数据结构与算法 
### 1.数据结构
  - 一维
    - 简单
      - 数组[array] / 链表[linked list]
    - 高级
      - 栈[Stack] / 队列[queue] / 双向队列[deque] / 集合[set] / 映射[map]
  - 二维
    - 简单
      - 树[tree] / 图[graph]
    - 高级
      - 二叉树(红黑树 / AVL)
      - 并查集
      - 堆
      - 字典树
  - 特殊
    - 位运算[bitwise]
    - 布隆过滤器
    - LRU Cache
### 2.算法
 - 分支
 - 循环
 - 迭代
## 各种算法模板汇总
[经典二分算法](https://www.lintcode.com/problem/classical-binary-search)

```text
描述
在一个排序数组中找一个数，返回该数出现的任意位置，如果不存在，返回 -1。
```
```Java
public int binarySearch(int[] nums, int target) {
    // write your code here
    if(nums == null
       || nums.length == 0 
       || target < nums[0] 
       || target > nums[nums.length - 1]) 
    return -1;

    int left = 0, right = nums.length - 1;
    while(left + 1 < right){
        int mid = left + (right - left) / 2;
        if(target > nums[mid]){
            left = mid;
        }else if(target < nums[mid]){
            right = mid;
        }else{
            return mid;
        }
    }

    if(nums[left] == target){
        return left;
    }else if(nums[right] == target){
        return right;
    }else{
        return -1;
    }
}
```