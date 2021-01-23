---
layout: post
title: 'Trapping Rain Water'
date: 2020-12-11
categories: Algorithm
permalink: '/:categories/:title'
---

## Description

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

![Image for example](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

<br>
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
<br>

## Idea

The total water is decided by left_max and right_max: these 2 arrays
But, need to minus the building in the building array

## Code

```
def trap(self, height: List[int]) -> int:
        """The total water is decided by left_max and right_max: these 2 arrays
        But, need to minus the building in the building array
        """
        if len(height) < 3: # if there are 2 or less element, there is no water collected
            return 0

        left_max = [None] * len(height) # check from leftside
        left_max[0] = height[0]
        for i in range(1, len(height)):
            left_max[i] = max(left_max[i-1], height[i])

        right_max = [None] * len(height) # check from right side
        right_max[-1] = height[-1]
        for i in range(-2, -len(height) - 1, -1):
            right_max[i] = max(right_max[i+1], height[i])

        total_water = [] # there is no 2 sides accounted in total water
        for i in range(1, len(height) - 1):
            total_water.append(min(left_max[i], right_max[i]) - height[i])
        return sum(total_water)
```
