8. Linked List
--

At least these.

LeetCode Reverse Linked List
---

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        
        ListNode* p = head;
        ListNode* q = NULL;
        ListNode* r = NULL;
        while(p!=NULL){
            r = q;
            q= p;
            p=p->next;
            q->next = r;
        }
        head = q;
        return head;
    }
};

Order(n);

LeetCode Linked List Cycle
LeetCode Merge Two Sorted Lists