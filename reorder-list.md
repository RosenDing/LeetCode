## reorder-list

### 题目描述
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…
You must do this in-place without altering the nodes' values.
For example,
Given{1,2,3,4}, reorder it to{1,4,2,3}.

### 思路
1. 根据题意，一个链表是从后往前相间的从前往后插入链表，可以将链表分为两部分：前面的从先往后，后面一部分从后往前，这样，后面一部分就符合“栈”的存储结构
2. 想用先后两个步数不同的指针将链表分为两部分，这样分出来的结果根据链表节点的奇偶不同，后面链表的个数小于等于前面的。然后用栈存储后面的链表，再遍历前面的链表将节点插入。

### 代码
    import java.util.ArrayDeque;
    /**
     * Definition for singly-linked list.
     * class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) {
     *         val = x;
     *         next = null;
     *     }
     * }
     */
    public class Solution {
        public void reorderList(ListNode head) {
            if (head == null || head.next == null) {
    			return;
    		}
    		ArrayDeque<ListNode> stack = new ArrayDeque<ListNode>();
    		ListNode pre = head;
    		ListNode follow = head.next;
    		while (follow.next != null) {
    			pre = pre.next;
    			follow = follow.next;
    			if (follow.next != null) {
    				follow = follow.next;
    			}
    		}
    		
    		follow = pre.next;
    		pre.next = null;
    		pre = head;
    		while (follow != null) {
    			stack.push(follow);
    			follow = follow.next;
    		}
    		
    		while (!stack.isEmpty()) {
    			ListNode temp = stack.pop();
    			temp.next = pre.next;
    			pre.next = temp;
    			
    			pre = temp.next;
    		}
        }
    }
