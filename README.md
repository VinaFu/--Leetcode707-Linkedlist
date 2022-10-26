# Leetcode-707-Linked-list


class Node:
    
    def __init__(self, val):
        self.val = val
        self.next = None
    
class MyLinkedList:

    def __init__(self):
        self.head=None
        self.size = 0

    def get(self, index: int) -> int:
        if index >= self.size or index<0:
            return -1
        if self.head is None:
            return -1
        
        cur = self.head
        for i in range(index):
            cur = cur.next
        return cur.val        

    def addAtHead(self, val: int) -> None:
                   //因为是在头上加，每次都是从头开始，不用loop
        prev = Node(val)
        prev.next = self.head
        self.head = prev
        
        self.size+=1   

    def addAtTail(self, val: int) -> None:
        cur = self.head
        if cur is None:
            self.head = Node(val)
        else:
            while cur.next != None:
                cur = cur.next
            cur.next = Node(val)
                   // 加尾巴就不一样了，每次要到了才知道该加，所以需要loop到那个节点。
        
        self.size +=1

    def addAtIndex(self, index: int, val: int) -> None:
        if index <0 or index> self.size:
            return
        if index == 0:
            self.addAtHead(val)
        else:
            cur = self.head
            for i in range(index-1): 
                          //写的方法还是后加，所以停在上一个的后面
                cur = cur.next
            newNode = Node(val)
            newNode.next = cur.next
                         //总是先连尾巴
            cur.next = newNode
        
        self.size +=1

    def deleteAtIndex(self, index: int) -> None:
        if index <0 or index >= self.size:
            return 
        
        cur = self.head
        if index == 0:
            self.head = cur.next
        else:
            for i in range(index-1):
                cur = cur.next
            cur.next = cur.next.next
                        //跳过了那个要删除的项，所以next.next
        self.size -=1
            


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
