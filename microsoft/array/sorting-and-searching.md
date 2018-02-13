1. Remove Duplicates from Sorted Array 
2. Merge Sorted Array
3. Sort Colors
4. Find Minimum in Rotated Sorted Array
5. Find Minimum in Rotated Sorted Array II
6. Search in Rotated Sorted Array
7. Search a 2D Matrix
8. Search a 2D Matrix II
9. Median of Two Sorted Arrays



# 1. Remove Duplicates from Sorted Array

Given a sorted array, remove the duplicates[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm)such that each element appear onlyonceand return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array **[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

Idea: Two Pointers

Solution:

```cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.size() <= 1) return nums.size();
    int count = 1;
    for (int i = 1; i < nums.size(); i++){
        if (nums[i] != nums[i-1]) {
             count++;
             nums[count-1] = nums[i];
        } 
    }
    return count;
}
```



# 2. Merge Sorted Array

Given two sorted integer arrays nums1 and nums2 , merge nums2 into nums1 as one sorted array.

```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    vector<int> nums3;
    int i = 0, j = 0;
    while (i < m && j < n) {
        cout << i;
        if (nums1[i] <= nums2[j]) {nums3.push_back(nums1[i]);i++;}
                                   
        else {nums3.push_back(nums2[j]);j++;}
        
    }
    while (i < m) {
        nums3.push_back(nums1[i]);
        i++;
    }
    while (j < n) {
        nums3.push_back(nums2[j]);
        j++;
    }
    nums1 = nums3;
}
```

# 3. Sort Colors

Given an array withnobjects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

```cpp
void sortColors(vector<int>& nums) {
    int zero = 0;
    int one = 0;
    for (auto x: nums) {
        if (x == 0) zero++;
        else if (x == 1) one++;
    }
    int i = 0;
    while (i < zero) {
        nums[i] = 0;
        i++;
    }
    while (i < zero + one) {
        nums[i] = 1;
        i++;
    }
    while (i < nums.size()) {
        nums[i] = 2;
        i++;
    }
}
```

# 4. Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Find the minimum element.

You may assume no duplicate exists in the array.

**Solution:**

```cpp
int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    while (left + 1 < right) {
        int mid = left + ((right - left) >> 1);
        if (nums[mid] > nums[right]) left = mid;
        else right = mid;
    }
    if (nums[right] < nums[left]) return nums[right];
    return nums[left];
}
```

# 5. Find Minimum in Rotated Sorted Array II

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Find the minimum element.

**Solution:**

```cpp
int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    while (left + 1 < right) {
        int mid = left + ((right - left) >> 1);
        if (nums[mid] == nums[right]) right--;
        else if (nums[mid] > nums[right]) left = mid;
        else right = mid;
    }
    if (nums[right] < nums[left]) return nums[right];
    else return nums[left];
}
```

# 6. Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

**Solution:**

```cpp
int search(vector<int>& nums, int target) {
    if (nums.size() == 0) return -1;
    int left = 0, right = nums.size() - 1;
    while (left + 1 < right) {
        int mid = left + ((right - left) >> 1);
        if (nums[mid] == target) return mid;
        if (nums[mid] < nums[right]) {
            if (nums[mid] <= target && target <= nums[right]) left = mid;
            else right = mid;
        } else {
            if (nums[left] <= target && target <= nums[mid]) right = mid;
            else left = mid;
        }
    }
    if (nums[left] == target) return left;
    else if (nums[right] == target) return right;
    return -1;
}
```



# 7. Search a 2D Matrix

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

**Solution:**

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (!matrix.size() || !matrix[0].size()) return false;
    int m = matrix.size(), n = matrix[0].size();
    int left = 0, right = m * n - 1;
    while (left + 1 < right) {
        int mid = left + ((right - left) >> 1);
        int row = mid / n;
        int col = mid % n;
        if (matrix[row][col] == target) return true;
        if (matrix[row][col] < target) left = mid;
        else right = mid;
    }
    if (matrix[left/n][left%n] == target || matrix[right/n][right%n] == target) return true;
    else return false;
}
```

# 8. Search a 2D Matrix II

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Solution:**

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (matrix.size() == 0 || matrix[0].size() == 0) return false;
    int i = 0, j = matrix[0].size() - 1;
    while (i < matrix.size() && j >= 0) {
        if (matrix[i][j] == target) return true;
        else if (matrix[i][j] < target) i++;
        else j--;
    }
    return false;
}
```

# 9. Median of Two Sorted Arrays

There are two sorted arrays**nums1**and**nums2**of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

**Solution:**

```cpp
double findKthLargestElem (vector<int>::iterator a, int m, vector<int>::iterator b, int n, int k) {
    if (m > n) return findKthLargestElem(b, n, a, m, k);
    if (m == 0) return b[k-1];
    if (k == 1) return min(a[0], b[0]);
    int mid_a = min(m, k /2);
    int mid_b = k - mid_a;
    if (a[mid_a-1] <= b[mid_b-1]) return findKthLargestElem(a + mid_a, m - mid_a, b, n, k - mid_a);
    else return findKthLargestElem(a, m, b + mid_b, n - mid_b, k - mid_b);
}
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    int m = nums1.size();
    int n = nums2.size();
    auto a = nums1.begin();
    auto b = nums2.begin();
    int len = nums1.size() + nums2.size();
    if (len % 2 == 0) return (0.5 * findKthLargestElem(a, m, b, n, len / 2) + 0.5 * findKthLargestElem(a, m, b, n, (len / 2) + 1));
    else return findKthLargestElem(a, m, b, n, (len) / 2 + 1);
}
```



