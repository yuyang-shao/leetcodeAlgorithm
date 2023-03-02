#剑指offer 35 复杂链表复制
**方法一 回溯+哈希表(递归方式)**
- unorederd_map : 底层由哈希表实现
- 本题的重点在于random指针的指向，在普通的链表复制中，只需在生成下一个节点的同时，将前驱的next指针指向新生成的节点即可，但是在本题中，random指向的节点可能是该节点的**next->next->...**节点，在当前尚未生成，所以可以考虑回溯的方式，即当random节点生成之后将节点地址返回。
- 具体地，我们用哈希表记录每一个节点对应新节点的创建情况。遍历该链表的过程中，我们检查「当前节点的后继节点」和「当前节点的随机指针指向的节点」的创建情况。如果这两个节点中的任何一个节点的新节点没有被创建，我们都立刻递归地进行创建。当我们拷贝完成，回溯到当前层时，我们即可完成当前节点的指针赋值。注意一个节点可能被多个其他节点指向，因此我们可能递归地多次尝试拷贝某个节点，为了防止重复拷贝，我们需要首先检查当前节点是否被拷贝过，如果已经拷贝过，我们可以直接从哈希表中取出拷贝后的节点的指针并返回即可。


```cpp
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head==NULL){
            return NULL;
        }
        if(cacheHash.count(head)==0){
            Node * newNode = new Node(head->val);
            cacheHash.emplace(head,newNode);
            newNode->next = copyRandomList(head->next);
            newNode->random = copyRandomList(head->random);
        }
        return cacheHash[head];
        
    }
    unordered_map<Node * ,Node *> cacheHash;
};
```