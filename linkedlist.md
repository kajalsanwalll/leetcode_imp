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
---

APPROACH 1

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        unordered_map<ListNode*,int> mp;
        if(head== NULL || head->next == NULL){
            return false;
        }
        ListNode* p;
        p=head;

        while(p!=NULL){
            if(mp.find(p) != mp.end()){
                return true;
            }
            
            mp[p]++;
            p = p->next;
        }
        return false;
    }
};

Order(n);


APPROACH 2 Floyd's cycle detection



LeetCode Merge Two Sorted Lists