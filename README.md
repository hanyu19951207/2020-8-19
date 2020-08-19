# 2020-8-19
55. 跳跃游戏
    给定一个非负整数数组，你最初位于数组的第一个位置。
    数组中的每个元素代表你在该位置可以跳跃的最大长度。
    判断你是否能够到达最后一个位置。
    示例 1:
    输入: [2,3,1,1,4]
    输出: true
    解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
思路：
    根据题目的描述，只要存在一个位置 x，它本身可以到达，并且它跳跃的最大长度为 x+nums[x]，这个值大于等于 y，即 x+nums[x]≥y，那么位置 y 也可以到达。
    这样以来，我们依次遍历数组中的每一个位置，并实时维护 最远可以到达的位置。对于当前遍历到的位置 x，如果它在 最远可以到达的位置 的范围内，那么我们就可以从起点通过若干次跳跃到达该位置，因此我们可        以用 x+nums[x] 更新 最远可以到达的位置。
    在遍历的过程中，如果 最远可以到达的位置 大于等于数组中的最后一个位置，那就说明最后一个位置可达，我们就可以直接返回 True 作为答案。
    反之，如果在遍历结束后，最后一个位置仍然不可达，我们就返回 False 作为答案。
题解：
public class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int rightmost = 0;
        for (int i = 0; i < n; ++i) {
            if (i <= rightmost) {
                rightmost = Math.max(rightmost, i + nums[i]);
                if (rightmost >= n - 1) {
                    return true;
                }
            }
        }
        return false;
    }
}
594. 最长和谐子序列
     和谐数组是指一个数组里元素的最大值和最小值之间的差别正好是1。
      现在，给定一个整数数组，你需要在所有可能的子序列中找到最长的和谐子序列的长度。
      示例 1:
      输入: [1,3,2,2,5,2,3,7]
      输出: 5
      原因: 最长的和谐数组是：[3,2,2,2,3].
思路：
    我们可以枚举数组中的每一个元素，对于当前枚举的元素 x，它可以和 x + 1 组成和谐子序列。我们再遍历一遍整个数组，找出等于 x 或 x + 1 的元素个数，就可以得到以 x 为最小值的和谐子序列的长度。
题解：
    class Solution {
    public int findLHS(int[] nums) {
        int res = 0;
        for(int i = 0;i < nums.length;i++){
            int count = 0;
            boolean flag = false;
            for(int j = 0;j < nums.length;j++){
                if(nums[j] == nums[i])
                    count++;
                else if(nums[j] + 1 == nums[i]){
                    count++;
                    flag = true;
                }
            }
            if(flag)
                res = Math.max(count, res);
        }
        return res;
    }
}
605. 种花问题
      假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。
      给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 n 。能否在不打破种植规则的情况下种入 n 朵花？能则返回True，不能则返回False。
      示例 1:
      输入: flowerbed = [1,0,0,0,1], n = 1
      输出: True
思路：
      我们从左到右扫描数组 flowerbed，如果数组中有一个 0，并且这个 0 的左右两侧都是 0，那么我们就可以在这个位置种花，即将这个位置的 0 修改成 1，并将计数器 count 增加 1。
      对于数组的第一个和最后一个位置，我们只需要考虑一侧是否为 0。
      在扫描结束之后，我们将 count 与 n 进行比较。如果 count >= n，那么返回 True，否则返回 False。
题解：
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int i = 0, count = 0;
        while (i < flowerbed.length) {
            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) && (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
            i++;
        }
        return count >= n;
    }
}
