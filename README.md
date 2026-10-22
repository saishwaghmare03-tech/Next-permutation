# 31. Next Permutation

![Java](https://img.shields.io/badge/Language-Java-orange.svg)
![LeetCode](https://img.shields.io/badge/LeetCode-Medium-yellow.svg)
![Time Complexity](https://img.shields.io/badge/Time_Complexity-O(N)-green.svg)
![Space Complexity](https://img.shields.io/badge/Space_Complexity-O(1)-green.svg)

An optimal, in-place Java implementation for LeetCode Problem 31: **Next Permutation**.

---

## 📌 Problem Description

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container.

If such an arrangement is not possible (i.e., the array is in descending order), the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

The replacement must be done **in place** and use only **constant extra memory**.

---

## 💡 Algorithm Explanation

To find the next lexicographically greater permutation efficiently in $O(N)$ time:

1. **Find the Pivot (`i`)**: Scan backwards from right to left to find the first element `nums[i]` that is smaller than its adjacent element `nums[i + 1]` (`nums[i] < nums[i + 1]`).
2. **Find the Successor (`j`)**: If a pivot exists (`i >= 0`), scan backwards again to find the first element `nums[j]` that is strictly greater than `nums[i]`.
3. **Swap**: Swap the elements at indices `i` and `j`.
4. **Reverse**: Reverse the suffix starting at index `i + 1` up to the end of the array to ensure the lowest possible lexicographical order for the remaining elements.

---

## 📂 Code Implementation

```java
import java.util.Arrays;

class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int i = n - 2;
        
        // Step 1: Find the first decreasing element from the right
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
        
        // Step 2: If pivot is found, find element just larger than nums[i]
        if (i >= 0) {
            int j = n - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            // Step 3: Swap nums[i] and nums[j]
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
        
        // Step 4: Reverse suffix starting at index i + 1
        reverse(nums, i + 1, n - 1);
    }
    
    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
    
    public static void main(String[] args) {
        Solution solution = new Solution();
        
        // Test Case 1
        int[] nums1 = {1, 2, 3};
        solution.nextPermutation(nums1);
        System.out.println("Test 1: " + Arrays.toString(nums1)); // Output: [1, 3, 2]
        
        // Test Case 2
        int[] nums2 = {3, 2, 1};
        solution.nextPermutation(nums2);
        System.out.println("Test 2: " + Arrays.toString(nums2)); // Output: [1, 2, 3]
        
        // Test Case 3
        int[] nums3 = {1, 1, 5};
        solution.nextPermutation(nums3);
        System.out.println("Test 3: " + Arrays.toString(nums3)); // Output: [1, 5, 1]
    }
}
