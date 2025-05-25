# ROTATE LINKED LIST (Right rotation by K places)
1. if head is null or there is just one node or k == 0 return head. (No change)
2. Find the length and make the linkedlist circular using a tail pointer. (set the last node's next to head)
3. Now if the length is 5 and k = 13 after 5 steps it will become same.
4. So we need to find k % length. In our example its 3.
5. We need to make 3 rotations which means new head will be length - k
6. iterate to the new head and set 


eg.  
1->2->3->4->5->(goes back to 1 coz we made it circular)    
k = 3
first   
5->1->2->3->4->(goes to 5)
second
4->5->1->2->3->(goes to 4) (we do it only till here because we return its next)
third
3->4->5->1->2->(goes to 3)
```
    public static ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) return head;
        
        // Find length and make it circular
        ListNode tail = head;
        int length = 1;
        while (tail.next != null) {
            tail = tail.next;
            length++;
        }
        tail.next = head; // Make circular
        
        // Find new tail (length - k%length - 1 steps from head)
        // If it would be left rotations stepstonewtail will be k but for right its length - k
        k = k % length;
        int stepsToNewTail = length - k;
        ListNode newTail = head;
        for (int i = 1; i < stepsToNewTail; i++) {
            newTail = newTail.next;
        }
        
        ListNode newHead = newTail.next;
        newTail.next = null; // Break the circle
        return newHead;
    }
```
