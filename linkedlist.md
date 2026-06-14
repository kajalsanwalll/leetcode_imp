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


Reorder List
---


class Solution {
public:
    void reorderList(ListNode* head) {
        
        if(!head || !(head->next)) return;

        ListNode* slow = head;
        ListNode* fast = head;

        //finding mid element - when fast stops, slow is on mid ele
        while(fast->next && fast->next->next){
            slow = slow->next;
            fast = fast->next->next;
        }

        //reverse second part
        ListNode* second = slow->next;
        slow->next =NULL;
        ListNode* prev = NULL;

        while(second){
            ListNode* nextNode = second->next;
            second->next = prev;
            prev = second;
            second = nextNode;
        }

        //merge
        second = prev;
        ListNode* first = head;

        while(second){
            ListNode* temp1 = first->next;
            ListNode* temp2 = second->next;

            first->next = second;
            second->next = temp1;

            first = temp1;
            second = temp2;
        }
    }
};


Time O(n);
Space O(1);


Remove Nth node from the end of list
---


class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {

        ListNode* dummy = new ListNode(0);
        dummy->next = head;

        ListNode* fast = dummy;
        ListNode* slow = dummy;

        for(int i = 0; i <= n; i++) {
            fast = fast->next;
        }
        while(fast != NULL) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;

        return dummy->next;
    }
};


O(n); time 


LRU Cache
---

class LRUCache {
public:
    class Node{
        public:
            int key,value;
            Node* prev;
            Node* next;

            Node(int k,int v){
                key = k;
                value = v;
     
            }
    };

    int cap;
    unordered_map<int, Node*> mp;

    Node* head;
    Node* tail;

    LRUCache(int capacity) {
        cap = capacity;

        head = new Node(0,0);
        tail = new Node(0,0);

        head->next = tail;
        tail->prev = head;
    }

    void remove(Node* node){
        Node* prevNode = node->prev;
        Node* nextNode = node->next;

        prevNode->next = nextNode;
        nextNode->prev = prevNode;
    }

    void insert(Node* node){
        Node* nextNode = head->next;
        head->next = node;
        node->prev = head;

        node->next = nextNode;
        nextNode->prev = node;
    }
    
    int get(int key) {
        if(mp.find(key) == mp.end()){
            return -1;
        }
        Node* node = mp[key];
        remove(node);
        insert(node);
        return node->value;
    }
    
    void put(int key, int value) {
        if(mp.find(key) != mp.end()){
            remove(mp[key]);
        }

        Node* node = new Node(key,value);

        mp[key] = node;
        insert(node);

        if(mp.size() > cap){
            Node* lru = tail->prev;
            remove(lru);
            mp.erase(lru->key);
        }
    }
};

O(1) get
O(1) put


Maximum twin sum of a linked list
---


class Solution {
public:
    int pairSum(ListNode* head) {

        if(!head || !head->next) return 0;

        ListNode* slow=head;
        ListNode* fast = head;

        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        } 
        ListNode* second = slow;
        ListNode* prev = NULL;
        while(second){
            ListNode* nextNode = second->next;
            second->next = prev;
            prev = second;
            second = nextNode;
        }
        int ans = 0;
        while(prev){
            ans = max(ans,head->val + prev->val);
            head = head->next;
            prev = prev->next;
        }
        return ans;
    }
};