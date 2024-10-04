# Linked List Cheat Sheet in C++

## 1. Basic Structure of a Node
```cpp
class ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
```
## 2. Inserting a Node
### Insert at Beginning
```cpp
void insertAtBeginning(ListNode*& head, int data) {
    ListNode* newNode = new ListNode(data);
    newNode->next = head;
    head = newNode;
}

```
### Insert at End
```cpp
void insertAtEnd(ListNode*& head, int data) {
    ListNode* newNode = new ListNode(data);
    if (!head) {
        head = newNode;
        return;
    }
    ListNode* temp = head;
    while (temp->next)
        temp = temp->next;
    temp->next = newNode;
}

```
### Insert After a Given Node
```cpp
void insertAfter(ListNode* prevNode, int data) {
    if (!prevNode) return;
    ListNode* newNode = new ListNode(data);
    newNode->next = prevNode->next;
    prevNode->next = newNode;
}

```
## 3. Deleting a Node
### Delete Node by Value
```cpp
void deleteNode(ListNode*& head, int key) {
    if (!head) return;
    if (head->val == key) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
        return;
    }
    ListNode* temp = head;
    while (temp->next && temp->next->val != key)
        temp = temp->next;
    if (!temp->next) return;
    ListNode* nodeToDelete = temp->next;
    temp->next = nodeToDelete->next;
    delete nodeToDelete;
}

```
### Delete Node at a Given Position
```cpp
void deleteAtPosition(ListNode*& head, int position) {
    if (!head) return;
    ListNode* temp = head;
    if (position == 0) {
        head = head->next;
        delete temp;
        return;
    }
    for (int i = 0; temp != NULL && i < position - 1; i++)
        temp = temp->next;
    if (!temp || !temp->next) return;
    ListNode* nodeToDelete = temp->next;
    temp->next = nodeToDelete->next;
    delete nodeToDelete;
}

```
## 4. Searching for a Node

```cpp
bool search(ListNode* head, int key) {
    ListNode* temp = head;
    while (temp) {
        if (temp->val == key) return true;
        temp = temp->next;
    }
    return false;
}

```
## 5. Reverse a Linked List
### Iterative Approach
```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = NULL;
    ListNode* curr = head;
    while (curr) {
        ListNode* nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}

```
### Recursive Approach
```cpp
ListNode* reverseListRecursive(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode* rest = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = NULL;
    return rest;
}

```
## 6. Detecting a Cycle (Floyd’s Cycle Detection)
### 
```cpp
bool hasCycle(ListNode* head) {
    if (!head || !head->next) return false;
    ListNode* slow = head;
    ListNode* fast = head->next;
    while (fast && fast->next) {
        if (slow == fast) return true;
        slow = slow->next;
        fast = fast->next->next;
    }
    return false;
}

```
## 7. Find the Middle of a Linked List
```cpp
ListNode* findMiddle(ListNode* head) {
    if (!head) return NULL;
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

```
## 8. Merge Two Sorted Linked Lists
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;
    if (l1->val < l2->val) {
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    } else {
        l2->next = mergeTwoLists(l1, l2->next);
        return l2;
    }
}

```
## 9. Remove N-th Node from End
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* fast = dummy;
    ListNode* slow = dummy;
    for (int i = 0; i <= n; i++)
        fast = fast->next;
    while (fast) {
        fast = fast->next;
        slow = slow->next;
    }
    ListNode* nodeToDelete = slow->next;
    slow->next = slow->next->next;
    delete nodeToDelete;
    return dummy->next;
}

```
## 10. Detect and Remove Loop
### Detect Loop
```cpp
bool detectLoop(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (slow && fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}

```
### Remove Loop
```cpp
void removeLoop(ListNode* loopNode, ListNode* head) {
    ListNode* ptr1 = head;
    ListNode* ptr2;
    while (true) {
        ptr2 = loopNode;
        while (ptr2->next != loopNode && ptr2->next != ptr1)
            ptr2 = ptr2->next;
        if (ptr2->next == ptr1)
            break;
        ptr1 = ptr1->next;
    }
    ptr2->next = NULL;
}
```

## 11. Flatten a Multilevel Doubly Linked List
```cpp
ListNode* flatten(ListNode* head) {
    if (!head) return head;
    ListNode* curr = head;
    while (curr) {
        if (curr->child) {
            ListNode* next = curr->next;
            curr->next = flatten(curr->child);
            curr->next->prev = curr;
            curr->child = NULL;
            while (curr->next) curr = curr->next;
            curr->next = next;
            if (next) next->prev = curr;
        }
        curr = curr->next;
    }
    return head;
}

```
