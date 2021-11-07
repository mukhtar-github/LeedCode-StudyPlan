# Data Structure I

In computer science, a **data structure** is a way to store and organize data.

During the computer programming process, identifying and using the appropriate data structure is an important task as it can improve the overall efficiency of the *algorithm*. In large-scale systems, choosing the most suitable data structure directly impacts the difficulty of program design and the final quality and performance.

## Array

### 217. Contains Duplicate

Given an integer array *nums*, return *true* if any value appears *at least twice* in the array, and return *false* if every element is distinct.

Example 1:

Input: nums = [1,2,3,1]

Output: true

Example 2:

Input: nums = [1,2,3,4]

Output: false

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true

Constraints:

* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

#### Answer 1

```javascript
var containsDuplicate = n => new Set(n).size !== n.length;

//Your input
[1,2,3,1]
//Output
true
//Expected
true

// Alternate early return version:
function containsDuplicate(nums, set = new Set()) {
  for (let num of nums) {
    if (set.has(num)) return true;
    set.add(num);
  }
  return false;
};
```

### 53. Maximum Subarray

Given an integer array *nums*, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: [4,-1,2,1] has the largest sum = 6.

Example 2:

Input: nums = [1]

Output: 1

Example 3:

Input: nums = [5,4,-1,7,8]

Output: 23

Constraints:

* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4

#### Answer 2

```javascript
var maxSubArray = function(nums) {
    let [max] = nums, right = 0;
  while (right < nums.length) {
      nums[right] += nums[right-1] > 0 ? nums[right-1] : 0;
    
      max = Math.max(max, nums[right++]);
  }
  return max;
};

//Your input
[-2,1,-3,4,-1,2,1,-5,4]
//Output
6
//Expected
6
```

### 1. Two Sum

Given an array of integers *nums* and an integer *target*, return indices of the two numbers such that they add up to *target*.

You may assume that each input would have *exactly one solution*, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9

Output: [0,1]

Output: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6

Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6

Output: [0,1]

Constraints:

* 2 <= nums.length <= 10^4
* -10^9 <= nums[i] <= 10^9
* -10^9 <= target <= 10^9
* Only one valid answer exists.

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

#### Answer 3

```javascript
var twoSum = function(nums, target) {
    // Define a hashmap to store values, indices
    const map = new Map();
    
    for (let i = 0; i < nums.length; i++) {
        // Define current number, current diff
        const num = nums[i];
        const diff = target - num;
                
        // If hashmap contains difference, return stored index and current index
        if (map.has(diff)) return [map.get(diff), i];
        
        // Store (key: value => number: index) in hashmap
        map.set(num, i);
    }
};

//Your input
[2,7,11,15]
9
//Output
[0,1]
//Expected
[0,1]
```

### 88. Merge Sorted Array

You are given two integer arrays *nums1* and *nums2*, sorted in *non-decreasing order*, and two integers *m* and *n*, representing the number of elements in *nums1* and *nums2* respectively.

*Merge nums1 and nums2* into a single array sorted in *non-decreasing order*.

The final sorted array should not be returned by the function, but instead be stored inside the array *nums1*. To accommodate this, *nums1* has a length of *m + n*, where the first *m* elements denote the elements that should be merged, and the last *n* elements are set to *0* and should be ignored. *nums2* has a length of *n*.

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3

Output: [1,2,2,3,5,6]

Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0

Output: [1]

Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].

Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1

Output: [1]

Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

Constraints:

* nums1.length == m + n
* nums2.length == n
* 0 <= m, n <= 200
* 1 <= m + n <= 200
* -10^9 <= nums1[i], nums2[j] <= 10^9

Follow up: Can you come up with an algorithm that runs in *O(m + n)* time?

#### Answer 4

```javascript
var merge = function (nums1, m, nums2, n) {
    nums1.splice(m); // removes all 0's
    for (var i = 0; i < n; i++) {
        nums1.unshift(nums2[i]); // inserts each number from nums2 to the beggining of nums1
    }
    nums1.sort((a, b) => a - b); // sorts the array
};

//Your input
[1,2,3,0,0,0]
3
[2,5,6]
3
//Output
[1,2,2,3,5,6]
//Expected
[1,2,2,3,5,6]
```

### 350. Intersection of Two Arrays II

Given two integer arrays *nums1* and *nums2*, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in *any order*.

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]

Output: [2,2]

Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]

Output: [4,9]

Explanation: [9,4] is also accepted.

Constraints:

* 1 <= nums1.length, nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 1000

Follow up:

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

#### Answer 5

```javascript
var intersect = function(nums1, nums2) {
  const res = [], n1 = {}, n2 = {};
  for (let i = 0; i < Math.max(nums1.length, nums2.length); i++) {
    let num1 = nums1[i], num2 = nums2[i];
    n1[num1] = n1[num1] + 1 || 1, n2[num2] = n2[num2] + 1 || 1;
    [num1, num2].forEach(num => {
      if (n1[num] && n2[num]) {
        n1[num]--, n2[num]--;
        res.push(num);
      }
    })
  }
  return res;
};

var intersect = function(nums1, nums2) {
    // sort the arrays
    nums1.sort((a,b) => a-b), nums2.sort((a,b) => a-b);

    let i = 0,
        j = 0,
        result = [];
    
    while(i<nums1.length && j<nums2.length) {
        if(nums1[i] < nums2[j]){
            i++;
        } else if(nums1[i] > nums2[j]) {
            j++;
        } else {
            result.push(nums1[i]);
            i++;
            j++;
        }
    }
    
    return result;
};

//Your input
[1,2,2,1]
[2,2]
//Output
[2,2]
//Expected
[2,2]
```

### 121. Best Time to Buy and Sell Stock

You are given an array *prices* where *prices[i]* is the price of a given stock on the *i^th* day.

You want to maximize your profit by choosing a *single day* to buy one stock and choosing a *different day in the future* to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return *0*.

Example 1:

Input: prices = [7,1,5,3,6,4]

Output: 5

Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:

Input: prices = [7,6,4,3,1]

Output: 0

Explanation: In this case, no transactions are done and the max profit = 0.

Constraints:

* 1 <= prices.length <= 10^5
* 0 <= prices[i] <= 10^4

#### Answer 6

```javascript
/*
steps:
1. Set minimum to first price
2. Keep calculating different until ith price is less than minimum
3. Maintain max diff and current diff
*/

var maxProfit = function(prices) {
    let min = prices[0];
    let diffCurrent = 0;
    let diffMax = 0;
    
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] >= min) {
            // current price is greater than or equal to minumum so far
            // calculate diffCurrent and diffMax
            
            diffCurrent = prices[i] - min;
            
            if (diffCurrent > diffMax) {
                diffMax = diffCurrent;
            }
        } else {
            // current price is less than previous minimum
            // reset diffCurrent and minimum
            
            diffCurrent = 0;
            min = prices[i];
        }
    }
    
    return diffMax;
};

//Your input
[7,1,5,3,6,4]
//Output
5
//Expected
5
```

### 566. Reshape the Matrix

In MATLAB, there is a handy function called reshape which can reshape an m x n matrix into a new one with a different size r x c keeping its original data.

You are given an m x n matrix mat and two integers r and c representing the number of rows and the number of columns of the wanted reshaped matrix.

The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the reshape operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

Example 1:

![reshape1-grid](https://assets.leetcode.com/uploads/2021/04/24/reshape1-grid.jpg)

Input: mat = [[1,2],[3,4]], r = 1, c = 4

Output: [[1,2,3,4]]

Example 2:

![reshape2-grid](https://assets.leetcode.com/uploads/2021/04/24/reshape2-grid.jpg)

Input: mat = [[1,2],[3,4]], r = 2, c = 4

Output: [[1,2],[3,4]]

Constraints:

* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 100
* -1000 <= mat[i][j] <= 1000
* 1 <= r, c <= 300

#### Answer 7

```javascript
var matrixReshape = function(mat, r, c) {
    const flat = mat.flat()
    if (flat.length !== r*c) return mat;
    return [...Array(r)].map(() => flat.splice(0,c)) 
};

var matrixReshape = function(mat, r, c) {
  if (mat.length * mat[0].length / r !== c || mat.length === r) return mat;
  const flat = mat.flat();
  while (r-- !== 0) flat.unshift(flat.splice(-c));
  return flat;
};

//Your input
[[1,2],[3,4]]
1
4
//Output
[[1,2,3,4]]
//Expected
[[1,2,3,4]]
```

### 118. Pascal's Triangle

Given an integer *numRows*, return the first *numRows* of *Pascal's triangle*.

In *Pascal's triangle*, each number is the sum of the two numbers directly above it as shown:

![PascalTriangleAnimated2](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

Example 1:

Input: numRows = 5

Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

Example 2:

Input: numRows = 1
Output: [[1]]

Constraints:

* 1 <= numRows <= 30

#### Answer 8

```javascript
var generate = function(numRows) {
    const res = [];
    let prevRow;
    
    for (let i = 1; i <= numRows; i++) {
        const row = new Array(i).fill(1);

        if (prevRow) {
            for (let j = 1; j < prevRow.length; j++) {
                const cs = prevRow[j] + prevRow[j - 1];
                row[j] = cs;
            }
        }
        
        res.push(row);
        prevRow = row;
    }
    
    return res;
};

/*
Idea:
For this problem, we can do pretty much just as the instructions tell us. We'll iterate through the building of Pascal's triangle (ans), row by row. When we create each new row, we should initially fill it with 1s so that we don't have to worry about the logic of filling the edge cells that only have one number above.

Then we can start on j = 1 for each row and repeat the process of summing up the value of the current cell until we reach the midpoint (mid). Since the triangle is symmetrical, we can actually fill both halves of the row at once, while we work inward.

Once we reach the end of the last row, we can return ans.

Time Complexity: O(N) where N is the numRowsth triangular number
Space Complexity: O(1)
*/

var generate = function(numRows) {
    let ans = new Array(numRows)
    for (let i = 0; i < numRows; i++) {
        let row = new Uint32Array(i+1).fill(1),
            mid = i >> 1
        for (let j = 1; j <= mid; j++) {
            let val = ans[i-1][j-1] + ans[i-1][j]
            row[j] = val, row[row.length-j-1] = val
        }
        ans[i] = row
    }
    return ans
};

//Your input
5
//Output
[[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
//Expected
[[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

### 36. Valid Sudoku

Determine if a *9 x 9* Sudoku board is valid. Only the filled cells need to be validated *according to the following rules*:

1. Each row must contain the digits *1-9* without repetition.
2. Each column must contain the digits *1-9* without repetition.
3. Each of the nine *3 x 3* sub-boxes of the grid must contain the digits *1-9* without repetition.

Note:

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.

Example 1:

![250px-Sudoku-by-L2G-20050714.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

Input: board =

[["5","3",".",".","7",".",".",".","."],

["6",".",".","1","9","5",".",".","."],

[".","9","8",".",".",".",".","6","."],

["8",".",".",".","6",".",".",".","3"],

["4",".",".","8",".","3",".",".","1"],

["7",".",".",".","2",".",".",".","6"],

[".","6",".",".",".",".","2","8","."],

[".",".",".","4","1","9",".",".","5"],

[".",".",".",".","8",".",".","7","9"]]

Output: true

Example 2:

Input: board =
[["8","3",".",".","7",".",".",".","."],

["6",".",".","1","9","5",".",".","."],

[".","9","8",".",".",".",".","6","."],

["8",".",".",".","6",".",".",".","3"],

["4",".",".","8",".","3",".",".","1"],

["7",".",".",".","2",".",".",".","6"],

[".","6",".",".",".",".","2","8","."],

[".",".",".","4","1","9",".",".","5"],

[".",".",".",".","8",".",".","7","9"]]

Output: false

Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

Constraints:

* board.length == 9
* board[i].length == 9
* board[i][j] is a digit 1-9 or '.'.

#### Answer 9

```javascript
var isValidSudoku = function(board) {
    const colObj = {}
    const rowObj = {}
    const areaArr = new Array(9)

    for (let row = 0; row < 9; row++) {
        for (let col = 0; col < 9; col++) {
            const num = board[row][col]
            if (num === ".") continue
            // row checking
            if (!rowObj[row]) rowObj[row] = new Set()
            if (rowObj[row].has(num)) return false
            else rowObj[row].add(num)

            // col checking
            if (!colObj[col]) colObj[col] = new Set()
            if (colObj[col].has(num)) return false
            else colObj[col].add(num)

            // area checking
            const index = Math.floor(row / 3) * 3 + Math.floor(col / 3)
            if (!areaArr[index]) areaArr[index] = new Set()
            if (areaArr[index].has(num)) return false
            else areaArr[index].add(num)
        }
    }
    return true
};

//Your input
[["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
//Output
true
//Expected
true
```

### 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an *m x n* matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

Example 1:

![mat](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

Output: true

Example 2:

![mat2](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13

Output: false

Constraints:

* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 100
* -10^4 <= matrix[i][j], target <= 10^4

#### Answer 10

```javascript
var searchMatrix = function(matrix, target) {
    // initialize a new one dimensional array
    const oneDMatrix = []
    
    // Iterate over the original two dimensional array and add each row to 
    // the new one dimensional array
    for (let i = 0; i < matrix.length; i++) {
        oneDMatrix.push(...matrix[i]);
    }

    // binary search function
    const binarySearch = (arr, target, left, right) => {
        if (left > right) return false;

        const mid = Math.ceil((left + right) / 2);
        if (arr[mid] === target) return true;

        if (target < arr[mid]) {
            return binarySearch(arr, target, left, mid - 1);
        } else if (target > arr[mid]) {
            return binarySearch(arr, target, mid + 1, right);
        }
        return false;
    }

    // return binary search function on the one dimensional array
    return binarySearch(oneDMatrix, target, 0, oneDMatrix.length - 1)
};

//Your input
[[1,3,5,7],[10,11,16,20],[23,30,34,60]]
3
//Output
true
//Expected
true
```

## String

### 387. First Unique Character in a String

Given a string *s*, find the first non-repeating character in it and return its index. If it does not exist, return *-1*.

Example 1:

Input: s = "leetcode"

Output: 0

Example 2:

Input: s = "loveleetcode"

Output: 2

Example 3:

Input: s = "aabb"

Output: -1

Constraints:

* 1 <= s.length <= 10^5
* s consists of only lowercase English letters.

#### Answer 11

```javascript
var firstUniqChar = function (s) {
  const set = new Set();
  for (let i = 0; i < s.length; ++i) {
    if (s.indexOf(s[i], i + 1) === -1 && !set.has(s[i])) return i;
    else set.add(s[i]);
  }
  return -1;
};

//Your input
"leetcode"
//Output
0
//Expected
0
```

### 383. Ransom Note

Given two stings *ransomNote* and *magazine*, return *true* if *ransomNote* can be constructed from *magazine* and *false* otherwise.

Each letter in *magazine* can only be used once in *ransomNote*.

Example 1:

Input: ransomNote = "a", magazine = "b"

Output: false

Example 2:

Input: ransomNote = "aa", magazine = "ab"

Output: false

Example 3:

Input: ransomNote = "aa", magazine = "aab"

Output: true

Constraints:

* 1 <= ransomNote.length, magazine.length <= 10^5
* ransomNote and magazine consist of lowercase English letters.

#### Answer 12

```javascript
var canConstruct = function(ransomNote, magazine) {
    const magazineMap = new Map()
    for (const ch of magazine) {
        magazineMap.set(ch, (magazineMap.get(ch) ?? 0) + 1)
    }
    for (const ch of ransomNote) {
        if (!magazineMap.get(ch))
            return false
        const left = magazineMap.get(ch) - 1
        if (left === 0) 
            magazineMap.delete(ch)
        else
            magazineMap.set(ch, left)
    }
        
    return true
};

//Your input
"a"
"b"
//Output
false
//Expected
false
```

### 242. Valid Anagram

Given two strings *s* and *t*, return *true* if *t* is an anagram of *s*, and *false* otherwise.

Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false

Constraints:

* 1 <= s.length, t.length <= 5 * 10^4
* s and t consist of lowercase English letters.

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

#### Answer 13

```javascript
var canConstruct = function(ransomNote, magazine) {
    const magazineMap = new Map()
    for (const ch of magazine) {
        magazineMap.set(ch, (magazineMap.get(ch) ?? 0) + 1)
    }
    for (const ch of ransomNote) {
        if (!magazineMap.get(ch))
            return false
        const left = magazineMap.get(ch) - 1
        if (left === 0) 
            magazineMap.delete(ch)
        else
            magazineMap.set(ch, left)
    }
        
    return true
};

//Your input
"a"
"b"
//Output
false
//Expected
false
```
