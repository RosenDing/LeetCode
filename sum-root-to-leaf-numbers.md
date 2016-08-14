## sum-root-to-leaf-numbers

### 题目描述
Given a binary tree containing digits from0-9only, each root-to-leaf path could represent a number.
An example is the root-to-leaf path1->2->3which represents the number123.
Find the total sum of all root-to-leaf numbers.
For example,
    1
   / \
  2   3

The root-to-leaf path1->2represents the number12.
The root-to-leaf path1->3represents the number13.
Return the sum = 12 + 13 =25.

### 思路
1. 根据题意，我们可以根据先序遍历的顺序一边遍历一边计算
2. 注意：设置两个值temp和sum，每次进入结点的时候temp加一次，每次从这个节点出来的时候temp减去这个节点的值，遍历到叶子节点的时候要对sum进行一次计算

### 代码
    /**
     * Definition for binary tree
     * public class TreeNode {
     *     int val;
     *     TreeNode left;
     *     TreeNode right;
     *     TreeNode(int x) { val = x; }
     * }
     */
    public class Solution {
        public int sumNumbers(TreeNode root) {
        	int[] data = {0, 0}; // {temp, sum}
        	if (root != null) {
        		getSum(root, data);
        	}
        	return data[1];
        	
        }
        public void getSum(TreeNode root, int[] data) {
        	data[0] *= 10;
        	data[0] += root.val;
        	if (root.left == null && root.right == null) {
        		data[1] += data[0];
        		data[0] -= root.val;
        		data[0] /= 10;
        		return;
        	}
        	if (root.left != null) {
        		getSum(root.left, data);
        	}
        	if (root.right != null) {
        		getSum(root.right, data);
        	}
        	data[0] -= root.val;
        	data[0] /= 10;
        }
    }
