---
title: '[LeetCode 136] Single Number'
date: 2018-11-05 12:30:38
categories: 
  - leetcode
  - 数组
tags:
  - leetcode
  - 算法
  - C++
---
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
<!-- more --> 

## 题目描述 ##

> 
English：  
Given an array of integers, every element appears twice except for one. Find that single one.
Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?  

>  
中文：  
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
说明：
你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？  

## 思路 ##

异或（^）的几个性质：
 - **顺序无关**：多个元素异或的结果与元素的顺序无关。
 - **同一个数异或两次等于没有异或**：如4 ^ 3 ^ 4 = 3。
 - **个数与0异或的结果为其本身**：如3 ^ 0 = 3。  
 
了解了这些性质，这道题就很简单了。result初始值设为0，将数组中每个元素都与result作异或并更新result，最终result的值就是那个唯一只出现一次的元素了。代码如下：

    class Solution {
    public:
        int singleNumber(vector<int> &nums) {
            int result = 0;
            for (auto num:nums) {
                result ^= num;
            }
        return result;
        }
    };
     



























