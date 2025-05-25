## Check if a Linked List is a Palindrome

1. Slow and fast at the head.
2. While fast.next and fast.next.next != null slow = slow.next and fast = fast.next.next
3. Reverse the linklist starting at slow.next and set slow.next = null
4. Now you have two linkedlists. Iterate and compare.

```
public static boolean isPalindrome(Node head) {
        if (head == null || head.next == null) return true;
        
        // Find middle using slow and fast pointers
        Node slow = head;
        Node fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // Reverse second half
        Node secondHalf = reverseIterative(slow.next);
        slow.next = null;
        
        // Compare first and second half
        Node firstHalf = head;
        while (secondHalf != null) {
            if (firstHalf.data != secondHalf.data) return false;
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }
        return true;
    }
```
