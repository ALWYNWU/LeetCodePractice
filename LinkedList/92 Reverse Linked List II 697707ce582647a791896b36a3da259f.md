# 92. Reverse Linked List II

Given the `head`of a singly linked list and two integers `left`and `right`where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return *the reversed list*.

![Untitled](92%20Reverse%20Linked%20List%20II%20697707ce582647a791896b36a3da259f/Untitled.png)

 Link: [https://leetcode.com/problems/reverse-linked-list-ii/](https://leetcode.com/problems/reverse-linked-list-ii/)

由于recursion的空间复杂度为O(n) 所以本题使用iteration 效率更高 

首先根据提供的left和right在链表中找到对应的位置（corner case: head为空或者只有一个元素返回head）然后记录起始元素的前一个node 因为该node需要在最后连接到反转之后的sublist的head 起始node为反转之后的tail 也需要记录下来 然后开始反转链表 使用常规的迭代方法 反转的次数可以通过n来控制 因为需要反转到最后一个node 反转结束后prev指向sublist的head cur指向sublist后的第一个元素 所以需要反转 m-n+1个node

```java
public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || head.next == null){
				// check corner cases
            return head;
        }
        
        ListNode prev = null;
        ListNode cur = head;
        int m = left;
        int n = right;

        while (m > 1){
            // find the m
            prev = cur;
            cur = cur.next;
            m--;
            n--;
						// n-1 是为了在反转sublist时控制反转的次数
        }
        
        ListNode con = prev;
				// con用来记录sublist前一个元素 反转结束后链接sublist的head
        ListNode tail = cur;
				// tail记录反转之后的sublist的tail 需要连接到right之后的node
        
        ListNode nextN = cur;
        // 第三个node 用来辅助reverse
        while (n > 0){
            nextN = cur.next;
            cur.next = prev;
            prev = cur;
            cur = nextN;
            n--;
						// reverse结束 此时prev指向sublist head cur指向sublist后第一个node
        }
        
        if (con == null){
				// 和原linked list连接起来 con连prev
            head = prev;
        } else {
            con.next = prev;
        }

        tail.next = cur;
        return head;
    }
```