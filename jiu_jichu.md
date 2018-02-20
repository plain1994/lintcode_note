Title: lintcode algorithm
Date: 2018-02-20 01:08
Category: Blogs
Tags: Java
Author: Tom Gou
Summary: lintcode algorithm ladder


* [Binary Search](#Binary Search)


### 1 warm-up

#### 1.1 strstr
For a given source string and a target string, you should output the first index(from 0) of target string in source string.

If target does not exist in source, just return -1.

Example:

If source = "source" and target = "target", return -1.

If source = "abcdabcdefg" and target = "bcd", return 1.

```java
class Solution {
    /**
     * Returns a index to the first occurrence of target in source,
     * or -1  if target is not part of source.
     * @param source string to be scanned.
     * @param target string containing the sequence of characters to match.
     */
    public int strStr(String source, String target) {
        // write your code here
        if (source == null || target == null){
            return -1;
        }
        for (int i = 0; i < source.length() - target.length() + 1; i++){
            int j = 0;
            for (j = 0; j < target.length(); j++){
                if (source.charAt(i + j) != target.charAt(j)){
                    break;
                }
            }
            if (j == target.length()){
                return i;
            }
        }
        return -1;
    }
}
```


### 2 Binary Search

enumeration => binary search O(logn)

#### 2.1 Binary Search template (for classic bs, first target bs, last target bs):

#####2.1.1 Classic Binary Search
```java
public class Solution {
    public int findPosition(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length == 0){
            return -1;
        }
        
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (nums[mid] == target){
                return mid;
            }else if (nums[mid] < target){
                start = mid;
            }else{
                end = mid;
            }
        }
        return -1;
    }
}
```

##### 2.1.2 First Position of Target
For a given sorted array (ascending order) and a target number, find the first index of this number in O(log n) time complexity.

If the target number does not exist in the array, return -1.

Example
If the array is [1, 2, 3, 3, 4, 5, 10], for given target 3, return 2.

```java
class Solution {
    public int binarySearch(int[] nums, int target) {
        if (nums.length == 0 || nums == null){
            return -1;
        }
        
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (nums[mid] == target){
                end = mid;
            }else if (nums[mid] < target){
                start = mid;
            }else if (nums[mid] > target){
                end = mid;
            }
        }
        
        if (nums[start] == target){
            return start;
        }
        if (nums[end] == target){
            return end;
        }
        return -1;
    }
}
```

##### 2.1.3 Last Position of Target
Find the last position of a target number in a sorted array. Return -1 if target does not exist.

```java
class Solution {
    public int lastPosition(int[] nums, int target) {
        // Write your code here
        if (nums == null || nums.length == 0){
            return -1;
        }
        
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (nums[mid] == target){
                start = mid;
            }else if (nums[mid] < target){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if (nums[end] == target){
            return end;
        }
        if (nums[start] == target){
            return start;
        }
        return -1;
    }
}
```