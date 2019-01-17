## Add two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.


### Version1

提交了第三次才成功....第一次忘记l1=l1.next，第二次没考虑【5】【5】这种情况

想着每天都刷一题，但是懒，时间急。。。会有效果吗？...

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(-1);
        ListNode head = result;
        ListNode tempNode;
        int carry = 0, temp;
        int count = 0;
        while (l1 != null || l2 != null) {
            temp = 0;
            if (l1 != null) {
                temp += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                temp += l2.val;
                l2 = l2.next;
            }
            temp += carry;
            if (temp >= 10) {
                temp -= 10;
                carry = 1;
            } else {
                carry = 0;
            }
            tempNode = new ListNode(temp);
            result.next = tempNode;
            result = result.next;
        }
        if (carry == 1) {
            result.next = new ListNode(1);
        }
        return head.next;
    }
}
```