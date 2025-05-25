## Iterative 

```
public static Node reverseLinkedList(Node head) {
        Node prev = null;
        Node curr = head;
        Node next = null;

        while (curr != null) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }

        return prev;
    }
```

## Recursive
if linkedlist is empty or 1 element return  
reverse the next node by calling recursive function  
then set the next node next to current node and current's next to null to avoid cycles  
then return rest  
rest always hold the head of the already reversed portion and the rest of the nodes gets attached later recursively  

eg.  
0->1->2->3  
we get to 3 recursively then the rest is always pointing at 3  
0->1->2<-3  
then
0->1<-2<-3  
then
0<-1<-2<-3
```
public static Node reverseRecursive(Node head) {
        if (head == null || head.next == null) return head;
        
        Node rest = reverseRecursive(head.next);
        head.next.next = head;
        head.next = null;
        return rest;
    }
```
