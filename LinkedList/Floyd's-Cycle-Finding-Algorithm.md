## Finding cycles
1. If head is null or head.next == null return false. (No cycle)
2. Node slow and Node fast at the head.
3. while fast or fast.next != null
4. slow = slow.next and fast = fast.next.next.
5. If slow == fast return true else return false
```
public static boolean hasCycle(Node head) {
        if (head == null || head.next == null) return false;
        
        Node slow = head;
        Node fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
```

## Find the Start Node of the Cycle
1. First find the cycle.
2. When you found the cycle put the slow node at the start.
3. Until slow != fast slow = slow.next and fast = fast.next.
4. Where they meet is the starting return it.

```
    public static Node findCycleStart(Node head) {
        if (head == null || head.next == null) return null;
        
        Node slow = head;
        Node fast = head;
        boolean hasCycle = false;
        
        // Find meeting point
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                hasCycle = true;
                break;
            }
        }
        
        if (!hasCycle) return null;
        
        // Find start of cycle
        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
```
