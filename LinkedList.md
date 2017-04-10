# LinkedList

## 不会做的题目: 2,445

- 237.Delete Node in a Linked List
```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public void deleteNode(ListNode node) {
	        node.val = node.next.val;
	        node.next = node.next.next;
	    }
	}
```

- 206.Reverse Linked List
```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public ListNode reverseList(ListNode head) {
	        ListNode prevNode = head;
	        if(prevNode!=null && prevNode.next!=null){
	            ListNode middleNode = prevNode.next;
	            prevNode.next = null;
	            if(middleNode.next!=null){
	                ListNode nextNode = middleNode.next;
	                while(nextNode!=null){
	                    middleNode.next = prevNode;
	                    prevNode = middleNode;
	                    middleNode = nextNode;
	                    nextNode = nextNode.next;
	                }
	                middleNode.next = prevNode;
	                return middleNode;
	            }else{
	                middleNode.next = prevNode;
	                return middleNode;
	            }
	        }else{
	            return head;
	        }
	    }
	}
```

- 203.Remove Linked List Elements
```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public ListNode removeElements(ListNode head, int val) {
	        if(head != null){
	            while(head.val==val){
	                head=head.next;
	                if(head == null){
	                    return head;
	                }
	            }
	            ListNode tmp = head.next;
	            ListNode prev = head;
	            while(tmp!=null){
	                if(tmp.val == val){
	                    prev.next = tmp.next;
	                }else{
	                    prev = tmp;
	                }
	                tmp = tmp.next;
	            }
	            return head;
	        }else{
	            return head;
	        }
	    }
	}
```

- 83.Remove Duplicates from Sorted List
```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public ListNode deleteDuplicates(ListNode head) {
	        ListNode currentNode = head;
	        ListNode predNode = head;
	        ListNode tmpNode = head;
	        if(currentNode == null){
	            return currentNode;
	        }else{
	            while(currentNode!=null){
	                tmpNode = currentNode.next;
	                predNode = currentNode;
	                while(tmpNode!=null){
	                    if(tmpNode.val == currentNode.val){
	                        predNode.next = tmpNode.next;
	                    }else{
	                        predNode = tmpNode;
	                    }
	                    tmpNode = tmpNode.next;
	                }
	                currentNode = currentNode.next;
	            }
	        }
	        return head;
	    }
	}
```

- 2. Add Two Numbers
```java
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode prev = new ListNode(0);
        ListNode head = prev;
        int carry = 0;
        while (carry !=0 || l1 != null || l2 != null) {
            ListNode cur = new ListNode(0);
            int sum = ((l1 == null) ? 0: l1.val) +  ((l2 == null) ? 0: l2.val) + carry;
            cur.val = sum % 10;
            carry = sum / 10;
            prev.next = cur;
            prev = cur;
            
            l1 = (l1 == null) ? l1 : l1.next;
            l2 = (l2 == null) ? l2 : l2.next;
        }
        return head.next;
    }
}
```
- 445.Add Two Numbers II
```
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<Integer>();
        Stack<Integer> s2 = new Stack<Integer>();
        
        while(l1 != null) {
            s1.push(l1.val);
            l1 = l1.next;
        };
        while(l2 != null) {
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        int sum = 0;
        ListNode list = new ListNode(0);
        while (!s1.empty() || !s2.empty()) {
            if (!s1.empty()) sum += s1.pop();
            if (!s2.empty()) sum += s2.pop();
            list.val = sum % 10;
            ListNode head = new ListNode(sum / 10);
            head.next = list;
            list = head;
            sum /= 10;
        }
        
        return list.val == 0 ? list.next : list;
    }
}
```
