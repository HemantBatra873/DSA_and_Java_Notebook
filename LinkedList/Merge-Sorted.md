## Merge Two Sorted Linked Lists
```
    public static Node mergeTwoLists(Node l1, Node l2) {
        Node dummy = new Node(0);
        Node current = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.data <= l2.data) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }
        
        if (l1 != null) current.next = l1;
        if (l2 != null) current.next = l2;
        
        return dummy.next;
    }
```
    
## Merge K Sorted Linked Lists (Heap-based)
```
    public static Node mergeKLists(Node[] lists) {
        PriorityQueue<Node> minHeap = new PriorityQueue<>((a, b) -> a.data - b.data);
        
        // Add first node of each list to min heap
        for (Node list : lists) {
            if (list != null) minHeap.offer(list);
        }
        
        Node dummy = new Node(0);
        Node current = dummy;
        
        while (!minHeap.isEmpty()) {
            Node node = minHeap.poll();
            current.next = node;
            current = current.next;
            
            if (node.next != null) {
                minHeap.offer(node.next);
            }
        }
        
        return dummy.next;
    }
```
