	
---
#### 1. [Merge Sorted Arrays](https://leetcode.com/problems/merge-sorted-array/?envType=study-plan-v2&envId=top-interview-150)

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

#### Solution:

Normal merging of two sorted arrays moves from start to end. To save space and merge in the same array we move backwards. We put the larger element first while moving from the end of the array.

```cpp
class Solution {
   public void merge(int[] nums1, int m, int[] nums2, int n) {
       int ptr = n+m-1 , i = m-1 , j = n-1;
       while(i>=0 && j>=0){
           if(nums1[i]>nums2[j])nums1[ptr--]=nums1[i--];
           else nums1[ptr--]=nums2[j--];
       }
       while(i>=0)nums1[ptr--]=nums1[i--];
       while(j>=0)nums1[ptr--]=nums2[j--];
   }

}
```

#### 2. [Romove the element](https://leetcode.com/problems/remove-element/description/?envType=study-plan-v2&envId=top-interview-150)
Given an integer array nums and an integer val, remove all occurrences of val in nums [in-place](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
    
- Return k.

#### Solution:
Idea is to maintain additional pointer j which means array uptil [0,j-1] is valid(no ele with val). Now We can encounter two kinds of elements if we encounter val. Then move forward else with non val element we have to swap with jth element.

```cpp
class Solution{
public:
   int removeElement(vector<int>& nums, int val) {
       int i=0,j=0;
       int n = nums.size();
       while(i<n){
           if(nums[i]!=val){
               swap(nums[i],nums[j]);
               j++;
           }
           i++;
       }
       return j;
   }
};
```

#### 3. [Remove elemnet from sorted array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150):

Given an integer array nums sorted in non-decreasing order, remove the duplicates [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
    

Solution:

Suppose we are iterating over indexes at j and i represents the last index till which array is valid. Now for any element a[j] two cases are there if a[i]=a[j] this means this element was already used in the valid array so we don't need to add it to the valid part. If a[i]!=a[j] this means that ele was not used and must be added at i+1 th index.

```cpp
class Solution {
public:
   int removeDuplicates(vector<int>& nums) {
       int i=0;
       for(int j=1;j<nums.size();j++){
           if(nums[i]!=nums[j]){
               i++;
               nums[i]=nums[j];
           }
       }
       return i+1;
   }
};
```

#### 4. [Remove Duplicates 2](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/?envType=study-plan-v2&envId=top-interview-150):
Given an integer array nums sorted in non-decreasing order, remove some duplicates [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Solution:

Again the idea is same. Since we can keep atmost two element the condition to insert an element into valid subarray [0,i-1] is to check a[i-2]!=a[j] reason being if a[i-2]=a[j] this means for this a[j] atmost two of the entries are already inserted. So no need to insert other wise we can insert it at ith pos and increment the count.

```cpp
class Solution {
public:
   int removeDuplicates(vector<int>& nums) {
       int i=0;
       for(int j=0;j<nums.size();j++){
           if(i<=1 || nums[i-2]!=nums[j]){
               nums[i]=nums[j];
               i++;
           }
       }
       return i;
   }
};
```

#### 5. [Majority Element](https://leetcode.com/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150)

Given an array nums of size n, return the majority element.
The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Solution:

This is a famous majoirty problem. Idea is to keep a freq counter of the currently assumed majority element.

```cpp
class Solution {
public:
   int majorityElement(vector<int>& nums) {
       int ele=nums[0] , cnt = 0;
       for(auto e:nums){
           if(e==ele)cnt+=1;
           else{
               if(cnt>0)cnt--;
               else{
                   ele=e;
                   cnt=1;
               }
           }
       }
       return ele;
   }
};
```

Theorum: If the majority element is present only this element can be ele.

Proof: When we encounter an element either the freq of the element is increased or it decreases call it the balancing act. It is easy to see that if ele is majority all elements together can not balance it out. Thus in the end ele will reamin.

#### 6. [Rotate Array](https://leetcode.com/problems/rotate-array/?envType=study-plan-v2&envId=top-interview-150):

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Solution:

Right rotate:

```cpp
class Solution {
public:
   void rotate(vector<int>& nums, int k) {
       int n = nums.size();
       k %= n;
       reverse(nums.begin(), nums.end());
       reverse(nums.begin(), nums.begin()+k);
       reverse(nums.begin()+k, nums.end());
   }
};
```
  

Left Rotate: 

reverse first k element , then last n-k elements 
Finally all the elements must be reversed.

  ```python
def left_rotate(arr, d):
	n = len(arr)
	reverse(arr, 0, d - 1)
	reverse(arr, d, n - 1)
	reverse(arr, 0, n - 1)
```


Also right rotate:

```python
def right_rotate(arr, d):
	n = len(arr)
	d = d % n  # Handle if d > n
	reverse(arr, n - d, n - 1)
	reverse(arr, 0, n - d - 1)
	reverse(arr, 0, n - 1)
```

#### 7. [Best time to sell stocks](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/?envType=study-plan-v2&envId=top-interview-150):

You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Solution:

Max profit is max(a[i]-min(a[0,i-1])) - > aka we trty to sell on every day and to sell on day i we try to buy before ith day.

```cpp
class Solution {
public:
   int maxProfit(vector<int>& prices) {
       int mn = prices[0];
       int ans = 0;
       for(int i=0;i<prices.size();i++){
           ans = max(ans,prices[i]-mn);
           mn = min(mn,prices[i]);
       }
       return ans;
   }
};
```

Observing that greedy strategy like selling on the most expensive day won't work since it may happen that we may have to buy at a very high price. This strategy of trying to sell on every day while buy on cheapest day till possible is optimal.

#### 8. [Buy and sell stocks 2](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/?envType=study-plan-v2&envId=top-interview-150);

You are given an integer array of prices where prices[i] is the price of a given stock on the ith day.
On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.
Find and return the maximum profit you can achieve.

Solution:

First observe that if we plot values on a graph we should buy at minima and sell at local maxima.
This profit is the sum of deltas of maxima - minima on increasing slope. This is again equivalent to the sum of deltas when the delta is positive. 
Which gives us most simplest code.

```cpp
class Solution {
public:
   int maxProfit(vector<int>& prices) {
       int profit = 0;
       for (int i = 1; i < prices.size(); i++) {
           int del = prices[i]-prices[i-1];
           if(del>0)profit+=del;
       }
       return profit;       
   }
};
```

#### 9. [Jump Game](https://leetcode.com/problems/jump-game/description/?envType=study-plan-v2&envId=top-interview-150):

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

Solution:

Suppose it is known that we can reach upto index j. This means we can also reach upto any index k<j. Thus we can keep an index last_reach to hold this. If at any point we reach an index more than last_reach we can say this index is impossible to reach and if we can reach there may be we update last_reach to allow to reach some more indexes.

```cpp
class Solution {
public:
   bool canJump(vector<int>& nums) {
       int lst_index=0;
       for(int i=0;i<nums.size();i++){
           if(i>lst_index){
               return false;
           }else{
               lst_index = max(i+nums[i],lst_index);
           }
       }
       return true;
   }
};
```

#### 10. [Jump game 2](https://leetcode.com/problems/jump-game-ii/description/?envType=study-plan-v2&envId=top-interview-150):

You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

- 0 <= j <= nums[i] and
    
- i + j < n
    

Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

Note it is very easy to come up with O(n^2) solution:(dp based)
```cpp
class Solution {
public:
   int jump(vector<int>& nums) {
       vector<int> dp;
       dp.push_back(0);
       int n = nums.size();
       for(int i=1;i<n;i++){
           int crr_min = INT16_MAX;
           for(int j=0;j<i;j++){
               if(j+nums[j]>=i){
                   crr_min = min(crr_min,dp[j]+1);
               }
           }
           dp.push_back(crr_min);
       }
       return dp[n-1];
   }
};
```

But infact we can come up with greedy O(n) solutions: The idea is to think in terms of jumps so say we maintain a range which says in j jumps what segment we can be in. [a,b] then we can calculate in what range we can be in for the next jump. Closest we can be is b+1 for jump j+1 and farthest can be figured out by seeing all possbile jumps. 

Since each cell is processed only once we get O(n) time and O(1) space complexity.

```cpp
class Solution {
public:
   int jump(vector<int>& nums) {
       int a=0,b=0,n=nums.size(),j=0;
       while(b<n-1){
           int farthest = b+1;
           for(int i=a;i<=b;i++){
               farthest = max(farthest,nums[i]+i);
           }
           a=b+1;
           b=farthest;
           j++;
       }
       return j;
   }
};
```

couple of points:
1. Question garantees that a solution exists so we can have a = b+1 aka next near position equal to current fartest+1. If this guarantee was not there this could not have been done. And we would have to resort to a dp solution.
2. It is clear that if we can reach pos x in jumps j then pos x-1 can also be reached in the same number or smaller number of jumps. This intuition justifies the validity of continous segment [a,b].

#### 11. [H index](https://leetcode.com/problems/h-index/description/?envType=study-plan-v2&envId=top-interview-150):

Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper, return the researcher's h-index.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): The h-index is defined as the maximum value of h such that the given researcher has published at least h papers that have each been cited at least h times.

Solution:

There are two ways to do it:
a. Sorting: Reverse sort the array first. -> time complexity - O(nlogn)

```cpp
class Solution {
public:
   int hIndex(vector<int>& arr) {
       sort(arr.rbegin(),arr.rend());
       int ans=0;
       for(int i=0;i<arr.size();i++){
           if(arr[i]>=i+1)ans=i+1;
       }
       return ans;
   }
};
```

b. Counting: We can maintain the count of the number of papers having citations c. Observe that the maximum possble answer is n. Now what we can do is make an array of size n+1 and put the counts in this array. The reason for size n+1 is that all the papers with citation more than n won't increase the answer thus we can consider them having the citations n. Finally after counting we can find cumulative frequency and find the answer.

```cpp

class Solution {
public:
   int hIndex(vector<int>& arr) {
       int n = arr.size();
       vector<int> freq(n + 1, 0);
       for (int citation : arr) {
           freq[min(citation, n)]++;
       }
       int curr = 0;
       for (int i = n; i >= 0; i--) {
           curr += freq[i];
           if (curr >= i) {
               return i;
           }
       }
       return 0;       
   }
};
```

#### 12. [Insert Delete Getrandom](https://leetcode.com/problems/insert-delete-getrandom-o1/?envType=study-plan-v2&envId=top-interview-150):

Implement the RandomizedSet class:

- RandomizedSet() Initializes the RandomizedSet object.
    
- bool insert(int val) Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.
    
- bool remove(int val) Removes an item val from the set if present. Returns true if the item was present, false otherwise.
    
- int getRandom() Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.
    

You must implement the functions of the class such that each function works in average O(1) time complexity.

Solution:

The idea is to store values in array for random access and getting random element storing the actual index of elements in map.

```cpp
class RandomizedSet {
private:
   unordered_map<int, int> m;
   vector<int> l;
public:
   RandomizedSet() {
   }
   bool insert(int val) {
       if(m.count(val)!= 0) return false;
       m[val] = l.size();
       l.push_back(val);
       return true;
   }

   bool remove(int val) {
       if(m.count(val)!=0){
           int index = m[val];
           int lastvalue = l.back();
           l[index] = lastvalue;
           l.pop_back();
           m[lastvalue] = index;
           m.erase(val);
           return true;
       }
       return false;
   }

   int getRandom() {
       int randomIndex = std::rand() % l.size();
       return l[randomIndex];
   }
};
```

#### 13. [Product of array except Self](https://leetcode.com/problems/product-of-array-except-self/description/?envType=study-plan-v2&envId=top-interview-150):

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
You must write an algorithm that runs in O(n) time and without using the division operation.

Solution:

We can precal prefix sums and maintain sufffix sum while itering from back. prod[i] = pre[i-1]*curr_suff.

```cpp
class Solution {
public:
   vector<int> productExceptSelf(vector<int>& nums) {
       int n = nums.size();
       vector<int> pre(n);
       int curr=1;
       for(int i=0;i<n;i++){
           pre[i]=curr;
           curr*=nums[i];
       }
       curr=1;
       for(int i=n-1;i>=0;i--){
           pre[i]=curr*pre[i];
           curr*=nums[i];
       }
       return pre;
   }
```

In above implementation we have reused pre to strore answer.

#### 14 [Gas Station](https://leetcode.com/problems/gas-station/?envType=study-plan-v2&envId=top-interview-150):

There are n gas stations along a circular route, where the amount of gas at the ith station is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from the ith station to its next (i + 1)th station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique.

Solution:

First, what is the condition of the existence of a solution. It is sum of gas>= sum of cost if that is true there will be atleast one index which gives us the correct answer. To prove this we can consider the delta[i]=gas[i]-cost[i] now since the sum of deltas >=0 there is some index starting from it every cumm delta has to be positive.

Once we know there is a solution, the problem isn’t too difficult since the solution is guaranteed to be unique.The main logic is to move the starting point to the current index + 1 whenever the gas falls below 0.

```cpp
class Solution {
public:
   int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
       int del=0;
       for(int i=0;i<gas.size();i++){
           del+=gas[i]-cost[i];
       }
       if(del<0)return -1;
       del=0;
       int ans=0;
       for(int i=0;i<gas.size();i++){
           del+=gas[i]-cost[i];
           if(del<0){
               del=0;
               ans=i+1;
           }
       }
       return ans;
   }
};
```

