---
title: '[LeetCode 26 & 80] Remove Duplicates from Sorted Array'
date: 2018-09-28 12:58:30
categories: 
  - leetcode
  - 数组
tags:
  - leetcode
  - 算法
  - C++
---

LeetCode 26题与80题，两者很相似，都是在有序数组中去除重复项。题目如下：
<!-- more --> 
## 26. Remove Duplicates from Sorted Array（删除排序数组中的重复项） ##

> 
English：  
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.  
中文：  
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

本题考察数组的基本操作。做法是维护两个指针，一个保留当前有效元素的长度，一个从前往后扫，然后跳过那些重复的元素。因为数组是有序的，所以重复元素一定相邻，不需要额外记录。时间复杂度是O(n)，空间复杂度O(1)。代码如下：

    class Solution {
    public:
      int removeDuplicates(vector<int>& nums) {
          if (nums.size() <= 1) return nums.size();
          
          int index = 1;
          for (int i = 1; i < nums.size(); i++){
              if (nums[i] != nums[index - 1])
                  nums[index++] = nums[i];
                  }
          return index;
      }
     };
     
## 80. Remove Duplicates from Sorted Array II（删除排序数组中的重复项 II） ##

> English：  
Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.  
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.  
中文：  
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。  
不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

和26题很相似，唯一的区别是允许每个元素最多出现两次，思路和26题是相同的，只需要将其中的1改为2即可。类似的，如果有其他的题目要求“允许每个元素最多出现n次”，将1改为n即可。代码如下：  

    class Solution {
    public:
      int removeDuplicates(vector<int>& nums) {
          if (nums.size() <= 2) return nums.size();
          int index = 2;
          for (int i = 2; i < nums.size(); i++){
              if (nums[i] != nums[index - 2])
                  nums[index++] = nums[i];
                  }
          return index;
        }
      };






















