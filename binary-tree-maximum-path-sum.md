## binary-tree-maximum-path-sum

### 题目描述
Given a binary tree, find the maximum path sum.
The path may start and end at any node in the tree.
For example:
Given the below binary tree,

   1
  / \
 2   3
 

Return6.

### 思路
1. 这道题在让求树中任意起始结束结点的最大路径，由于我们不知道起始和结束结点的位置，一个路径中必定有一个根节点，所以我们把树中每个结点对应的最大路径值记录在每个结点上。注意：这个节点值是从该节点遍历下去的一条最大路径的值，除了该节点，其子节点计算的值都只有一个子树。根据先计算子节点再计算根节点，我们选择后序遍历二叉树。比如
                5
              /  \
             3    8
            / \   / \
           2   4 6    9
          /       \     \
         1         7    10

每个节点对应的值为
               32
              /  \
             7    27
            / \   / \
           3   4 13   19
          /       \     \
         1         7    10
         
2. 这里存储的每个节点的值和最后的值不是一个值，我们定义一个sum变量来存储我们要求的值，每遍历到一个节点时，我们需要将该节点的左右子节点存储的值相加，看看该节点对应的路径是否是比sum大，大的话就替换掉sum当前值
3. 还要注意：树的节点的值可能是负数，所以要对每个节点左右子节点的返回值判断一下，若比0小，就赋值为0；初始化sum时不要赋值为0，要赋值为最小值0x80000000（int的最大值为0x7fffffff）

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
        int sum = 0x80000000; // 赋值为最小值
    	public int maxPathSum(TreeNode root) {
    		if (root == null) {
    			return 0;
    		}
    		getSum(root);
    		return sum;
        }
    	
    	public int getSum(TreeNode root) {
    		if (root == null) {
    		    // 没有节点，返回0
    			return 0;
    		}
    		// 后序遍历
    		int leftNum = getSum(root.left);
    		int rightNum = getSum(root.right);
    		// 判断子节点的值是否小于0
            if (leftNum < 0) {
    			leftNum = 0;
    		}
    		if (rightNum < 0) {
    			rightNum = 0;
    		}
    		// 计算当前路径值，和现有sum比较
    		int temp = leftNum + rightNum + root.val; 
    		if (temp > sum) {
    			sum = temp;
    		}
    		// 返回左右子节点中值比较大的一个
    		return (leftNum > rightNum ? leftNum : rightNum) + root.val;
    	}
    }
