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


class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;

        while(fast!= NULL && fast->next != NULL){
            slow = slow->next;
            fast = fast->next->next;

            if(fast==slow){
                return true;
            }
        }
        return false;
    }
};

LeetCode Merge Two Sorted Lists
---

class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* dummy = new ListNode(-1);
        ListNode* tail = dummy;

        while(list1 != NULL && list2 != NULL){
            if(list1->val <= list2->val){
                tail->next = list1;
                list1 = list1->next;
            }else{
                tail->next = list2;
                list2 = list2->next;
            }
            tail = tail->next;
        }

        if(list1 != NULL){
            tail->next = list1;
        }else{
            tail->next = list2;
        }
        return dummy->next;
    }
};