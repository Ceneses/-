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
      - 并查集(最大的作用是检查一个图上是否存在一个环)
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
## 二分算法模板汇总
### 1.[经典二分算法](https://www.lintcode.com/problem/classical-binary-search)

`描述`

> 在一个排序数组中找一个数，返回该数出现的任意位置，如果不存在，返回 -1。

`样例`

> **样例 1：**
>
> ```
> 输入：nums = [1,2,2,4,5,5], target = 2
> 输出：1 或者 2
> ```
>
> **样例 2：**
>
> ```
> 输入：nums = [1,2,2,4,5,5], target = 6
> 输出：-1
> ```

`挑战`

>  `O(logn)` 的时间

```java
public int bianarySearch(int[] nums, int target) {
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

### 2.[查找数组中最后一个元素]( https://www.lintcode.com/problem/last-position-of-target )

`描述`

>  给一个升序数组，找到 `target` 最后一次出现的位置，如果没出现过返回 `-1` 

`样例`

> **样例 1：**
>
> ```
> 输入：nums = [1,2,2,4,5,5], target = 2
> 输出：2
> ```
>
> **样例 2：**
>
> ```
> 输入：nums = [1,2,2,4,5,5], target = 6
> 输出：-1
> ```

```java
public int lastPosition(int[] nums, int target) {
    // write your code here
    if(nums == null 
       || nums.length == 0 
       || target < nums[0] 
       || target > nums[nums.length - 1]) 
    return -1;

    int left = 0, right = nums.length - 1;
    while(left + 1 < right){
        int mid = left + (right - left) / 2;
        if(target >= nums[mid]){
            left = mid;
        }else{
            right = mid;
        }
    }

    if(nums[right] == target){
        return right;
    }else if(nums[left] == target){
        return left;
    }else{
        return -1;
    }
}
```

### 3.[搜索数组的第一个元素]( https://www.lintcode.com/problem/first-position-of-target )

`描述`

>  给定一个排序的整数数组（升序）和一个要查找的整数`target`，用`O(logn)`的时间查找到target第一次出现的下标（从0开始），如果target不存在于数组中，返回`-1`。 

`样例`

> ```
> 样例  1:
> 	输入:[1,4,4,5,7,7,8,9,9,10]，1
> 	输出: 0
> 	
> 	样例解释: 
> 	第一次出现在第0个位置。
> 
> 样例 2:
> 	输入: [1, 2, 3, 3, 4, 5, 10]，3
> 	输出: 2
> 	
> 	样例解释: 
> 	第一次出现在第2个位置
> 	
> 样例 3:
> 	输入: [1, 2, 3, 3, 4, 5, 10]，6
> 	输出: -1
> 	
> 	样例解释: 
> 	没有出现过6， 返回-1
> ```

`挑战`

> 如果数组中的整数个数超过了2^32，你的算法是否会出错？

```java
public int findFirstPosition(int[] nums, int target) {
    // write your code here
    if(nums.length == 0 
       || nums == null 
       || target < nums[0] 
       || target > nums[nums.length - 1]) 
    return -1;

    int left = 0;
    int right = nums.length - 1;

    while(left + 1 < right){
        int mid = left + (right - left) / 2;
        if(target <= nums[mid]){
            right = mid;
        }else{
            left = mid;
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

### 4.[寻找峰值]( https://www.lintcode.com/problem/find-peak-element )

`描述`

> 你给出一个整数数组(size为n)，其具有以下特点：
>
> - 相邻位置的数字是不同的
> - A[0] < A[1] 并且 A[n - 2] > A[n - 1]
>
> 假定*P*是峰值的位置则满足`A[P] > A[P-1]`且`A[P] > A[P+1]`，返回数组中任意一个峰值的位置。

`样例`

>```
>样例 1:
>	输入:  [1, 2, 1, 3, 4, 5, 7, 6]
>	输出:  1 or 6
>	
>	解释:
>	返回峰顶元素的下标
>
>
>样例 2:
>	输入: [1,2,3,4,1]
>	输出:  3
>```

`挑战`

> Time complexity O(logN)

```java
public int findPeak(int[] A) {
    // write your code here
    if(A.length < 3) return -1;

    int left = 1, right = A.length - 2;
    while(left + 1 < right){
        int mid = left + (right - left) / 2;
        if(A[mid - 1] > A[mid]){
            right = mid;
        }else{
            left = mid;
        }
    }

    if(A[left] > A[right]){
        return left;
    }else{
        return right;
    }
}
```

### 5.[搜索插入位置]( https://www.lintcode.com/problem/search-insert-position )

`描述`

>  给定一个排序数组和一个目标值，如果在数组中找到目标值则返回索引。如果没有，返回到它将会被按顺序插入的位置。 
>
> 你可以假设在数组中无重复元素。

`样例`

> **[1,3,5,6]**，5 → 2
>
> **[1,3,5,6]**，2 → 1
>
> **[1,3,5,6]**， 7 → 4
>
> **[1,3,5,6]**，0 → 0

`挑战`

> 时间复杂度为`O(log(n))`

```java
public int searchInsert(int[] A, int target) {
    // write your code here
    if(A.length == 0 || A == null || target <= A[0]){
        return 0;
    }

    if(target > A[A.length - 1]){
        return A.length;
    }

    int start = 0, end = A.length - 1;
    while(start + 1< end){
        int mid = start + (end - start) / 2;
        if(target <= A[mid]){
            end = mid;
        }else{
            start = mid;
        }
    }

    if(A[start] >= target){
        return start;
    }else{
        return end;
    }
}
```

### 6.[ 对x开根 ]( https://www.lintcode.com/problem/sqrtx )

`描述`

> 实现 `int sqrt(int x)` 函数，计算并返回 *x* 的平方根。

`样例`

> ```
> 样例 1:
> 	输入:  0
> 	输出: 0
> 
> 
> 样例 2:
> 	输入: 3
> 	输出: 1
> 	
> 	样例解释：
> 	返回对x开根号后向下取整的结果。
> 
> 样例 3:
> 	输入: 4
> 	输出: 2
> ```

`挑战`

> O(log(x))

```java
public int sqrt(int x) {
    // write your code here
    if(x == 0 || x == 1) return x;
    long start = 1, end = x;

    while(start + 1 < end){
        long mid = start + (end -start) / 2;
        if(x > (int)mid * mid){ // mid就是寻找的解的变量，这里就是填写目标的满足的条件
            start = mid;
        }else if(x < (int)mid * mid){
            end = mid;
        }else{
            return (int)mid;
        }
    }
    if(start * start < x){
        return (int)start;
    }else{
        return (int)end;
    }
}
```

## 排序算法模板总汇

### 1.[归并排序]()



### 2.[快速排序]()



### 3.冒泡排序



### 4.堆排序



### 5.[第K个最小的数]( https://leetcode-cn.com/problems/kth-largest-element-in-an-array)

`描述`

> 在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。 

`样例`

> 示例 1:
>
> 输入: [3,2,1,5,6,4] 和 k = 2
> 输出: 5
> 示例 2:
>
> 输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
> 输出: 4

`说明`

>  你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度 

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();

    for(int val : nums){
        pq.add(val);
        if(pq.size() > k){ // 维护优先队列的长度为K
            pq.poll();
        }
    }
    return pq.peek();
}
```

## 搜索算法模板总汇

### 1.DFS深搜



### 2.BFS宽搜



### 3.BackTracking回溯



## 链表问题总汇





## 排列问题总汇

### 1.[全排列]( https://www.lintcode.com/problem/permutations )

`描述`

> 给定一个数字列表，返回其所有可能的排列。

`样例`

**样例 1：**

```
输入：[1]
输出：
[
  [1]
]
```

**样例 2：**

```
输入：[1,2,3]
输出：
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

`挑战`

> 使用递归和非递归分别解决。

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> results = new ArrayList<>();

    // 如果数组为空直接返回空
    if (nums == null) {
        return results;
    }

    //dfs
    dfs(nums, new boolean[nums.length], new ArrayList<Integer>(), results);

    return results;
}

private void dfs(int[] nums, boolean[] used, List<Integer> current, List<List<Integer>> results) {

    //找到一组排列，已到达边界条件
    if (nums.length == current.size()) {
        results.add(new ArrayList<Integer>(current));
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        //i位置这个元素已经被用过
        if (used[i]) {
            continue;
        }

        //继续递归
        current.add(nums[i]);
        used[i] = true;
        dfs(nums, used, current, results);
        used[i] = false;
        current.remove(current.size() - 1);
    }
}
```

