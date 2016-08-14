## linked-list-cycle-ii

### 题目描述
Given a linked list, return the node where the cycle begins. If there is no cycle, returnnull.
Follow up:
Can you solve it without using extra space?

### 思路
1. 设置两个指针nodeFast和nodeSlow，nodeSlow每次走一步，nodeFast每次走两步，如果存在环，则没有空指针，而且两个节点相遇的时候nodeFast比nodeSlow多走的节点数正好是环里包括的节点数
2. 然后将nodeFast置为head从头走，nodeSlow不变，这次两个节点每次都走一步，也就是说nodeSlow比nodeFast一直多走一个环，当他们相遇时，刚好是在环的起点处，然后就再也不分开了

### 代码
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
        public ListNode detectCycle(ListNode head) {
            if (head == null) {
    			return null;
    		}
    		
    		ListNode nodeFast = head;
    		ListNode nodeSlow = head;
    		do {
    			if (nodeFast.next == null) {
    				return null;
    			}
    			nodeFast = nodeFast.next;
    			nodeSlow = nodeSlow.next;
    			if (nodeFast.next == null) {
    				return null;
    			}
    			nodeFast = nodeFast.next;
    		} while (nodeFast != nodeSlow);
    		
    		nodeFast = head;
    		while (nodeFast != nodeSlow) {
    			nodeFast = nodeFast.next;
    			nodeSlow = nodeSlow.next;
    		}
    		return nodeSlow;
        }
    }
