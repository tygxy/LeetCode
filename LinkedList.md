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