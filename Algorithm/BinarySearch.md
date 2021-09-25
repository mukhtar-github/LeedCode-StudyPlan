# Algorithm

## 704. Binary Search

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

Constraints:

1 <= nums.length <= 10^4
-10^4 < nums[i], target < 10^4
All the integers in nums are unique.
nums is sorted in ascending order

### Answer

```javascript
var search = function (nums, target) {
    let start = 0;
    let end = nums.length - 1;

    while (start <= end) {
        let mid = Math.round((start + end) / 2);
        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }
    return -1;
};

Your input => [-1,0,3,5,9,12]
9
Output => 4
Expected => 4
```

### Approach 1: Binary Search

#### Intuition

Binary search is a textbook algorithm based on the idea to compare the target value to the middle element of the array. If the target value is equal to the middle element - we're done. If the target value is smaller - continue to search on the left. If the target value is larger - continue to search on the right.

#### Algorithm 1

* Initialise left and right pointers : left = 0, right = n - 1.

* While left <= right :

* Compare middle element of the array nums[pivot] to the target value target.

* If the middle element is the target target = nums[pivot] : return pivot.

* If the target is not yet found :

* If target < nums[pivot], continue the search on the left right = pivot - 1.

* Else continue the search on the right left = pivot + 1.
