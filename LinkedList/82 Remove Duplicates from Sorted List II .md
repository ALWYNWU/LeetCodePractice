# 82. Remove Duplicates from Sorted List II

Given the `head`of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list* Return *the linked list **sorted** as well*

**Ex.   1 - 2 -3 - 3 -4 - 4 -5   ⇒   1 - 2 - 3**

  **1 - 1 - 1 - 2 - 3  ⇒  2 - 3**

Link: [https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/solution/](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/solution/)

### Method 1

因为存在head可能被删除的情况 所以要使用dummyHead 同时要定义两个pointer, head指向当前的节点 prev表示在要被删除的sublist前的最后一个node

本题需要注意的是什么时候移动prev节点 当head移动到要删除的sublist的最后一位的时候 prev.next = head.next, 但是这时不移动prev，因为后面有可能还有重复的node

只要head.next不为空 且当前node的val和下一个val相同 就不移动prev 只移动head

![Untitled](82%20Remove%20Duplicates%20from%20Sorted%20List%20II%20f7e0a46ce2b7439cb83dab492f9deb1f/Untitled.png)

**Step1:  declare dummyHead, dummyHead.next = head, prev = dummyHead**

**Step2:** move head, if `head.next ≠ null && head.val == head.next.val`, continue move head untile head is the end of the duplicate sublist, then let `prev.next=head.next`, then continue move head forward

**Step3:** if head.next=null or head.val≠head.next.val, then we move prev

**Step4:** return dummyHead.next

Time complexity: O(n) pass alone the input list

Space: O(1)

```java
public ListNode deleteDuplicates(ListNode head){
		ListNode dummyHead = new ListNode(0,head);
		ListNode prev = dummyHead;
		
		while(head != null){
				if(head.next != null && head.val == head.next.val){
						while(head.next != null && head.val == head.next.val){
								head = head.next;
						}
						prev.next = head.next;
				} else {
						prev = prev.next;
				}
				head = head.next;
		}
		return dummyhead.next;
}
```

### Method 2

recursion解法 不要跳进递归中 先分析base case 然后递归

reverse linkedlist 的basecase

```java
if (head == null || head.next == null){
		return head;
}
```

```java
ListNode reverseLinkedList(ListNode head){
		if (head == null || head.next == null){
				return head;
		}

		ListNode last = reverseLinkedList(head.next);
		
		head.next.next = head;
		head.next = null;
		return last;
}
```

![Untitled](82%20Remove%20Duplicates%20from%20Sorted%20List%20II%20f7e0a46ce2b7439cb83dab492f9deb1f/Untitled%201.png)

**Follow up** 反转链表前N个node

![Untitled](82%20Remove%20Duplicates%20from%20Sorted%20List%20II%20f7e0a46ce2b7439cb83dab492f9deb1f/Untitled%202.png)

在反转结束后 head要连接的不是null 而是n后面的node 我们定义该node为successor

```java
ListNode reverseNnodes(ListNode head, int n){
		ListNode sucessor = null;
		if(n==1){
				// 记录第n+1个node 该node为successor
				successor = head.next;
				return head;
		}
		// 因为以head.next为起点 所以反转前n-1个node
		ListNode last = reverseNnodes(head.next, n-1);
		
		head.next.next = head;
		head.next = successor;
		//反转之后的head和后面的successor连起来
		return last;
}
```