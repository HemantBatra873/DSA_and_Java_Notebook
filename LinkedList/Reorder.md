# REORDER LINKED LIST (L0→Ln→L1→Ln-1…)

Basically after the first we should have last then second then second last and we hace to modify the original linkedlist
```
    public static void reorderList(ListNode head) {
        if (head == null || head.next == null) return;
        
        // Find middle
        ListNode slow = head, fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // Reverse second half
        ListNode secondHalf = reverseList(slow.next);
        slow.next = null;
        
        // Merge alternately
        ListNode first = head, second = secondHalf;
        while (second != null) {
            ListNode temp1 = first.next, temp2 = second.next;
            first.next = second;
            second.next = temp1;
            first = temp1;
            second = temp2;
        }
    }
```
