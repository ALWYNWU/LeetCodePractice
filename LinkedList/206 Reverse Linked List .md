# 206. Reverse Linked List

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.
Link: [https://leetcode.com/problems/reverse-linked-list/](https://leetcode.com/problems/reverse-linked-list/)

**Easy**

![Untitled](206%20Reverse%20Linked%20List%20d87a211b42664982a4b77cd27b1fb9d5/Untitled.png)

### Method 1 Iteration

对于迭代法 相对于递归空间复杂度更低 时间复杂度相同 如果追求效率使用iteration

额外使用两个listnode 一个用来记录previous node一个用来记录next 最后返回的head是prev

> **Time O(n)
Space O(1)**
> 

```java
public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode prev = null;
        ListNode next;
        ListNode cur = head;
        while(cur!=null){
            next = cur.next;
            cur.next = prev;
            prev = cur;
            cur = next;
        }
        return prev;

    }
```

### Method 2 Recursion

recursion解法 不要跳进递归中 先分析base case 然后递归

reverse linkedlist 的basecase

> **Time O(n)
Space O(n)**
> 

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

![Untitled](206%20Reverse%20Linked%20List%20d87a211b42664982a4b77cd27b1fb9d5/Untitled%201.png)

**Follow up** 反转链表前N个node

![Untitled](206%20Reverse%20Linked%20List%20d87a211b42664982a4b77cd27b1fb9d5/Untitled%202.png)

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