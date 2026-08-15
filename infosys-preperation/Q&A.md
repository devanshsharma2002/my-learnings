# Infosys SP/DSE Mock Exam - Coding Questions & Solutions

This document contains the problem concepts and optimal Python solutions for the Infosys mock exam. All solutions are designed to handle strict Time Limit Exceeded (TLE) constraints and dirty input data from competitive programming platforms.

---

## Question 1: Maximum Perimeter of a Valid Triangle (Fixed Gap)

**Problem Description:**
Given an array `nums` of size `N`, find the maximum perimeter of a valid triangle. A valid triangle in this specific problem is formed by choosing three elements whose indices form an arithmetic progression (a fixed gap between them, such as indices 0, 1, 2 or 0, 2, 4). Return 0 if no valid triangle can be formed.

**Concept Used:**
*   **Sliding Window with Fixed Gaps:** Iterate through all possible gap sizes `d`. The indices checked are `i`, `i+d`, and `i+2d`.
*   **Triangle Inequality Theorem:** Check if `a + b > c`, `a + c > b`, and `b + c > a`.
*   **Optimization:** Uses `zip()` and Python list slicing to push the loop execution to C-level speeds, avoiding TLE on $O(N^2)$ logic. It dynamically calculates array lengths to bypass platform input parsing bugs.

**Optimal Python Code:**
```python
def solve(N, nums):
    maxp = 0
    # Ignore N, get the absolute true length of the array to prevent hidden bugs
    n_len = len(nums)
    
    # Let d go all the way up to the length of the array
    for d in range(1, n_len):
        
        # If the gap is too large to form a triplet, break out
        if 2 * d >= n_len:
            break
            
        # zip handles the boundaries perfectly automatically at C-speed
        for a, b, c in zip(nums[:-2*d], nums[d:-d], nums[2*d:]):
            a, b, c = int(a), int(b), int(c)
            
            if (a + b > c) and (a + c > b) and (b + c > a):
                p = a + b + c
                if p > maxp:
                    maxp = p
                    
    return maxp