# Data Structure II

## Array

### 136. Single Number

Given a *non-empty* array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

Example 1:

Input: nums = [2,2,1]

Output: 1

Example 2:

Input: nums = [4,1,2,1,2]

Output: 4

Example 3:

Input: nums = [1]

Output: 1

Constraints:

* 1 <= nums.length <= 3 * 10^4
* -3 x 104 <= nums[i] <= 3 x 10^4
* Each element in the array appears twice except for one element which appears only once.

#### Answer 1

```javascript
var singleNumber = function(nums) {
    let single = 0;
    for (let num of nums) {
        single ^= num
    }
    return single
};


//Your input
[2,2,1]
//Output
1
//Expected
1
```

### 169. Majority Element

Given an array *nums* of size *n*, return the majority element.

The majority element is the element that appears more than *⌊n / 2⌋* times. You may assume that the majority element always exists in the array.

Example 1:

Input: nums = [3,2,3]

Output: 3

Example 2:

Input: nums = [2,2,1,1,1,2,2]

Output: 2

Constraints:

* n == nums.length
* 1 <= n <= 5 * 10^4
* -231 <= nums[i] <= 231 - 1

Follow-up: Could you solve the problem in linear time and in O(1) space?

#### Answer 2

```javascript
var majorityElement = function(nums) {
    const criterion = nums.length / 2 >> 0
    const countMap = new Map()
    for (const num of nums) {
        const curNum = (countMap.get(num) ?? 0) + 1
        if (curNum > criterion)
            return num
        countMap.set(num, curNum)
    }
};

//Your input
[3,2,3]
//Output
3
//Expected
3
```

### 15. 3Sum

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]

Example 2:

Input: nums = []

Output: []

Example 3:

Input: nums = [0]

Output: []

Constraints:

* 0 <= nums.length <= 3000
* -105 <= nums[i] <= 10^5

#### Answer 3

```javascript
var threeSum = function(nums) {
    var res = [];
    if(!nums || !nums.length) return res;

    nums = nums.sort((a, b) => a - b);

    for(let i=0; i<nums.length - 2; i++){
        while(nums[i-1] === nums[i]) i++;
        
        let j=i+1, k=nums.length-1;
        while(j<k){
            let sum = nums[i] + nums[j] + nums[k];
            if(sum === 0){
                res.push([nums[i],nums[j],nums[k]]);
                while (nums[j] === nums[j + 1]) j++;
                while (nums[k] === nums[k-1]) k--;
            }
            //searching for -nums[i]
            if(sum > 0){
                k--;
            }else{
                j++;
            }            
        }
    }
    return res;
};

//Your input
[-1,0,1,2,-1,-4]
//Output
[[-1,-1,2],[-1,0,1]]
//Expected
[[-1,-1,2],[-1,0,1]]
```

### 75. Sort Colors

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

Example 1:

Input: nums = [2,0,2,1,1,0]

Output: [0,0,1,1,2,2]

Example 2:

Input: nums = [2,0,1]

Output: [0,1,2]

Example 3:

Input: nums = [0]

Output: [0]

Example 4:

Input: nums = [1]

Output: [1]

Constraints:

* n == nums.length
* 1 <= n <= 300
* nums[i] is 0, 1, or 2.

Follow up: Could you come up with a one-pass algorithm using only constant extra space?

#### Answer 4

```javascript
var sortColors = function(nums) {
    let low= 0, high= nums.length- 1, mid= 0, temp= 0;
    
    while(mid <= high) {
        if(nums[mid] === 0) {
            // swap mid and low pointers values
            temp= nums[low];
            nums[low] = nums[mid];
            nums[mid]= temp;
            
            low++;
            mid++;
        } else if(nums[mid] === 2) {
            // swap mid and high pointers values
            temp= nums[high];
            nums[high]= nums[mid];
            nums[mid]= temp;
            
            high--;
        } else {
            mid++
        }
    }
    
    return nums;
};

//Your input
[2,0,2,1,1,0]
//Output
[0,0,1,1,2,2]
//Expected
[0,0,1,1,2,2]
```

### 56. Merge Intervals

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]

Output: [[1,6],[8,10],[15,18]]

Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

Example 2:

Input: intervals = [[1,4],[4,5]]

Output: [[1,5]]

Explanation: Intervals [1,4] and [4,5] are considered overlapping.

Constraints:

* 1 <= intervals.length <= 10^4
* intervals[i].length == 2
* 0 <= starti <= endi <= 10^4

#### Answer 5

```javascript
var merge = function(intervals) {
    
    if(intervals.length <2){
        return intervals;
    }
    
    // sort intervals    
    const sortedIntervals = intervals.sort((a,b) => {
        return a[0]-b[0];
    });
    
    
    let stack = [];
    stack.push(sortedIntervals[0]);
    
    for(let i=1;i<sortedIntervals.length;i++){
        let currStartTime = sortedIntervals[i][0];
        let currEndTime = sortedIntervals[i][1];
        let prevStartTime = stack[stack.length-1][0];
        let prevEndTime = stack[stack.length-1][1];
        
        if(currStartTime <= prevEndTime){
            stack[stack.length-1] = [Math.min(currStartTime,prevStartTime),Math.max(prevEndTime,currEndTime)];
        }
        else {
            stack.push(sortedIntervals[i]);
        }
    }
    return stack;
};

//Your input
[[1,3],[2,6],[8,10],[15,18]]
//Output
[[1,6],[8,10],[15,18]]
//Expected
[[1,6],[8,10],[15,18]]
```

### 706. Design HashMap

Design a HashMap without using any built-in hash table libraries.

Implement the MyHashMap class:

MyHashMap() initializes the object with an empty map.
void put(int key, int value) inserts a (key, value) pair into the HashMap. If the key already exists in the map, update the corresponding value.
int get(int key) returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
void remove(key) removes the key and its corresponding value if the map contains the mapping for the key.

Example 1:

Input

["MyHashMap", "put", "put", "get", "get", "put", "get", "remove", "get"]

[[], [1, 1], [2, 2], [1], [3], [2, 1], [2], [2], [2]]

Output

[null, null, null, 1, -1, null, 1, null, -1]

Explanation

MyHashMap myHashMap = new MyHashMap();

myHashMap.put(1, 1); // The map is now [[1,1]]

myHashMap.put(2, 2); // The map is now [[1,1], [2,2]]

myHashMap.get(1);    // return 1, The map is now [[1,1], [2,2]]

myHashMap.get(3);    // return -1 (i.e., not found), The map is now [[1,1], [2,2]]

myHashMap.put(2, 1); // The map is now [[1,1], [2,1]] (i.e., update the existing value)

myHashMap.get(2);    // return 1, The map is now [[1,1], [2,1]]

myHashMap.remove(2); // remove the mapping for 2, The map is now [[1,1]]

myHashMap.get(2);    // return -1 (i.e., not found), The map is now [[1,1]]

Constraints:

* 0 <= key, value <= 10^6
* At most 10^4 calls will be made to put, get, and remove.

#### Answer 6

```javascript
/*

var MyHashMap = function() {
    
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
MyHashMap.prototype.put = function(key, value) {
    
};

/** 
 * @param {number} key
 * @return {number}
 */
MyHashMap.prototype.get = function(key) {
    
};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashMap.prototype.remove = function(key) {
    
};

/** 
 * Your MyHashMap object will be instantiated and called as such:
 * var obj = new MyHashMap()
 * obj.put(key,value)
 * var param_2 = obj.get(key)
 * obj.remove(key)
 */*/


class ListNode {
    constructor(key, val, next) {
        this.key = key
        this.val = val
        this.next = next
    }
}
class MyHashMap {
    constructor() {
        this.size = 19997
        this.mult = 12582917
        this.data = new Array(this.size)
    }
    hash(key) {
        return key * this.mult % this.size
    }
    put(key, val) {
        this.remove(key)
        let h = this.hash(key)
        let node = new ListNode(key, val, this.data[h])
        this.data[h] = node
    }
    get(key) {
        let h = this.hash(key), node = this.data[h]
        for (; node; node = node.next)
            if (node.key === key) return node.val
        return -1
    }
    remove(key) {
        let h = this.hash(key), node = this.data[h]
        if (!node) return
        if (node.key === key) this.data[h] = node.next
        else for (; node.next; node = node.next)
            if (node.next.key === key) {
                node.next = node.next.next
                return
            }
    }
};

//Your input
["MyHashMap","put","put","get","get","put","get","remove","get"]
[[],[1,1],[2,2],[1],[3],[2,1],[2],[2],[2]]
//Output
[null,null,null,1,-1,null,1,null,-1]
//Expected
[null,null,null,1,-1,null,1,null,-1]
```

### 119. Pascal's Triangle II

#### Answer 7

Given an integer *rowIndex*, return the *rowIndex^th* (*0-indexed*) row of the *Pascal's triangle*.

In *Pascal's triangle*, each number is the sum of the two numbers directly above it as shown:

![PascalTriangleAnimated2](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

Example 1:

Input: rowIndex = 3

Output: [1,3,3,1]

Example 2:

Input: rowIndex = 0

Output: [1]

Example 3:

Input: rowIndex = 1

Output: [1,1]

Constraints:

* 0 <= rowIndex <= 33

Follow up: Could you optimize your algorithm to use only O(rowIndex) extra space?

The other top answers are all mostly of O(N^2) time complexity. So, I thought to include my solution here which is Linear in time.

As you see you can get any element of Pascal's Triangle in O(N) time and constant space complexity.
for first row first column we have 1C1
for second row first column we have 2C1
for second row second column we have 2C2
..... and so on
Therefore we can infer, for ith row and jth column we have the number iCj

And calculating this is pretty easy just in N time (factorial basically).

==> nCr = n*(n-1)*(n-2)...(r terms) / 1*2*..........*(r-2)*(r-1)*r

Now the question asks us to find the complete row.
If we calculate all the elements in this manner it would be quadratic in time. But, since its formula is pretty sleek, we proceed as follows:

suppose we have nCr and we have to find nC(r+1), like 5C3 and 5C4
==> 5C3 = 5*4*3 / 1*2*3

to get the next term we multiply numerator with its next term and denominator with its next term. As,
==> 5C4 = 5*4*3*2 / 1*2*3*4

We are following this simple maths logic to get the complete row in O(N) time.

Note:- We didnt actually need the variable temp. But the test cases are such that multiplying in one case exceeds the int range, and since we cannot change return type we have to take the long data type variable as temporary.

```javascript
// rowIndex = r

var getRow = function(r) {
    var ans = new Array(r+1)
    ans[0]=ans[r]=1
    for(i=1,up=r;i<r;i++,up--)
        ans[i] = ans[i-1]*up/i
    return ans
};
    

//Your input
3
//Output
[1,3,3,1]
//Expected
[1,3,3,1]
```

### 48. Rotate Image

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

![mat1](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]

Output: [[7,4,1],[8,5,2],[9,6,3]]

Example 2:

![mat2](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]

Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]

Example 3:

Input: matrix = [[1]]

Output: [[1]]

Example 4:

Input: matrix = [[1,2],[3,4]]

Output: [[3,1],[4,2]]

Constraints:

* matrix.length == n
* matrix[i].length == n
* 1 <= n <= 20
* -1000 <= matrix[i][j] <= 1000

#### Answer 8

The idea behind this relies on some math but I'll try my best with an ELI5 answer.

TLDR: Solve this by row reversing then transposing the matrix or transpose the matrix then reverse the columns

When you perform a 90 degree rotation the "diagonal" swaps directions.

[(X), 2, 3]          [7, 4, (X)]

[4, (X), 6]    =>    [8, (X), 2]     90 degree rotation

[7, 8, (X)]          [(X), 6, 3]

So to swap the diagonal you must either reverse by row or by column. If you imagine the matrix as a physical paper, swapping the row or column would be like flipping the paper over. So the diagonal is now swapped but the paper is now flipped on its back. So to flip the paper back to the proper face, you must perform a transpose.

To over simplify why you must transpose is because in 2D, a matrix transpose is like a form of geometric translation which is what a rotation is; however, a transpose is not enough to rotate a matrix as the values do not map to the correct positions. Reversing the row or column simply "corrects" the rotation.

[(X), 2, 3]          [7, 8, (X)]

[4, (X), 6]    =>    [4, (X), 6]     Reverse the rows to swap "diagonal" direction

[7, 8, (X)]          [(X), 2, 3]

[(X), 8, 9]          [7, 4, 1]

[4, (X), 6]    =>    [8, 5, 2]  Transposing along the diagonal will complete the rotation (assuming you row reversed first)

[1, 2, (X)]          [9, 6, 3]

Finally, you must know that: MATRIX MULTIPLICATION IS NOT COMMUTATIVE!

Order matters meaning,

(row reverse) x (transpose) =/= (transpose) x (row reverse)

But FYI, these two operations are the same

(row reverse) x (transpose) == (transpose) x (column reverse)

So you can solve this by first reversing rows then transposing or transposing then reverse columns. You can choose however you like.

```javascript
var rotate = function(matrix) {
    let length = matrix.length
    
    matrix.reverse()
    
    // transpose
    for (let i = 0; i < length; i++) {
        for (let j = 0; j < i; j++) {
            let temp = matrix[i][j]
            matrix[i][j] = matrix[j][i]
            matrix[j][i] = temp
        }
    }
    
    return matrix
};
    

//Your input
[[1,2,3],[4,5,6],[7,8,9]]
//Output
[[7,4,1],[8,5,2],[9,6,3]]
//Expected
[[7,4,1],[8,5,2],[9,6,3]]
```

### 59. Spiral Matrix II

Given a positive integer *n*, generate an *n x n matrix* filled with elements from *1* to *n^2* in spiral order.

Example 1:

![spiraln](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

Input: n = 3

Output: [[1,2,3],[8,9,4],[7,6,5]]

Example 2:

Input: n = 1

Output: [[1]]

Constraints:

* 1 <= n <= 20

#### Answer 9

```javascript
var generateMatrix = function (n) {
    let dr = [0, 1, 0, -1],
        dc = [1, 0, -1, 0],
        dir = 0,
        board = [],
        row = 0,
        col = 0;
    for (let i = 0; i < n; i++) {
        board[i] = Array(n).fill(0)
    }
    for (i = 1; i <= n * n; i++) {
        board[row][col] = i
        let nRow = row + dr[dir % 4],
            nCol = col + dc[dir % 4]
        if (nRow >= 0 && nRow < n && nCol >= 0 && nCol < n && board[nRow] && board[nRow][nCol] == 0) {
            row = nRow
            col = nCol
        } else {
            dir++
            row += dr[dir % 4]
            col += dc[dir % 4]
        }
    }
    return board
};
    

//Your input
3
//Output
[[1,2,3],[8,9,4],[7,6,5]]
//Expected
[[1,2,3],[8,9,4],[7,6,5]]
```

### 240. Search a 2D Matrix II

Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.

Example 1:

![searchgrid2](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5

Output: true

Example 2:

![searchgrid](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20

Output: false

Constraints:

* m == matrix.length
* n == matrix[i].length
* 1 <= n, m <= 300
* -10^9 <= matrix[i][j] <= 10^9
* All the integers in each row are sorted in ascending order.
* All the integers in each column are sorted in ascending order.
* -10^9 <= target <= 10^9
