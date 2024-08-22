����һ�����շǵݼ�˳�����е��������� nums����һ��Ŀ��ֵ target�������ҳ�����Ŀ��ֵ�������еĿ�ʼλ�úͽ���λ�á�
* ��������в�����Ŀ��ֵ target������ [-1, -1]���������Ʋ�ʵ��ʱ�临�Ӷ�Ϊ O(log n) ���㷨��������⡣
*
* ʾ�� 1��
* ���룺nums = [5,7,7,8,8,10], target = 8
* �����[3,4]
*
* ʾ�� 2��
* ���룺nums = [5,7,7,8,8,10], target = 6
* �����[-1,-1]
*
* ʾ�� 3��
* ���룺nums = [], target = 0
* �����[-1,-1]

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
                right = mid - 1; // ��������Ѱ��
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
                left = mid + 1; // ��������Ѱ��
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