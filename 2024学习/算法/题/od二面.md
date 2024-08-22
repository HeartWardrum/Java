给你一个按照非递减顺序排列的整数数组 nums，和一个目标值 target。请你找出给定目标值在数组中的开始位置和结束位置。
* 如果数组中不存在目标值 target，返回 [-1, -1]。你必须设计并实现时间复杂度为 O(log n) 的算法解决此问题。
*
* 示例 1：
* 输入：nums = [5,7,7,8,8,10], target = 8
* 输出：[3,4]
*
* 示例 2：
* 输入：nums = [5,7,7,8,8,10], target = 6
* 输出：[-1,-1]
*
* 示例 3：
* 输入：nums = [], target = 0
* 输出：[-1,-1]

~~~java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = new int[2];
        result[0] = findFirstPosition(nums, target);
        result[1] = findLastPosition(nums, target);
        return result;
    }
    
    private int findFirstPosition(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int firstPos = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                firstPos = mid;
                right = mid - 1; // 继续向左寻找
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return firstPos;
    }
    
    private int findLastPosition(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int lastPos = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                lastPos = mid;
                left = mid + 1; // 继续向右寻找
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return lastPos;
    }
}


~~~