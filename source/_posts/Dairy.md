---
title: Dairy
date: 2018-10-09 21:28:46
tags: Notes
---

### 10/8/2018 kadane's algorithm
---
kadane's algorithm (finding Maximum Subarray)
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
     	int max_so_far = INT_MIN, max_ending_here = 0; 

        for (int i = 0; i < nums.size(); i++) 
        { 
            max_ending_here = max_ending_here + nums[i]; 
            if (max_so_far < max_ending_here) 
                max_so_far = max_ending_here; 

            if (max_ending_here < 0) 
                max_ending_here = 0; 
        } 
        return max_so_far; 
    }
};
```
kadane's algorithm is also capable for finding the biggest difference of an array(leetcode 121)
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_here = 0, max = 0;
        for (int i = 1; i < prices.size(); i++)
        {
            max_here += (prices[i] - prices[i - 1]);
            if (max_here < 0)
                max_here = 0;
            if (max_here > max)
                max = max_here;
        }
        return max;
    }
};
```
---

	[7,1,5,3,6,4]
becomes	[-6,4,-2,3,-2]
Max subarray is 4,-2,3 = 5

### 10/9/2018
Moore's voting algorithm (finding the majority elements in an array)
```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int major = nums[0], count = 1;
        if (nums.size() == 1)
            return nums[0];
        for (int i = 1; i < nums.size(); i++)
        {
            if (nums[i] == major)
                count++;
            else
                count--;
            if (count == 0)
            {
                count++;
                major = nums[i];
            }
        }
        return major;
    }
};
```
## Factorial Trailing Zeroes
Given a factorial number, finds how many zeros are there at the end of that number 
This is a very good explanation from leetcode discuss channel:
>The ZERO comes from 10.
>Since 10 = 2 * 5
>How many multiples of 5 are there in the numbers from 1 to 100?
>because 100 ÷ 5 = 20, so, there are twenty multiples of 5 between 1 and 100.
>but wait, actually 25 is 5×5, so each multiple of 25 has an extra factor of 5, e.g. 25 × >4 = 100，which introduces extra of zero.
>So, we need know how many multiples of 25 are between 1 and 100? Since 100 ÷ 25 = 4, >there are four multiples of 25 between 1 and 100.
>Finally, we get 20 + 4 = 24 trailing zeroes in 100!
>The above example tell us, we need care about 5, 5×5, 5×5×5, 5×5×5×5 ....
>By given number 4617.
>5^1 : 4617 ÷ 5 = 923.4, so we get 923 factors of 5
>5^2 : 4617 ÷ 25 = 184.68, so we get 184 additional factors of 5
>5^3 : 4617 ÷ 125 = 36.936, so we get 36 additional factors of 5
>5^4 : 4617 ÷ 625 = 7.3872, so we get 7 additional factors of 5
>5^5 : 4617 ÷ 3125 = 1.47744, so we get 1 more factor of 5
>5^6 : 4617 ÷ 15625 = 0.295488, which is less than 1, so stop here.
>Then 4617! has 923 + 184 + 36 + 7 + 1 = 1151 trailing zeroes.
```c++
int trailingZeroes(int n) {
    int result = 0;
    for(long long i = 5; n / i>0; i *= 5){
        result += (n / i);
    }
    return result;
}
```

