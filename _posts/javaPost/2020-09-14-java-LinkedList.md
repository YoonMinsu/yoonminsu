---
title   : "LinkedList"
excerpt : "Collection Framework-List"
categories : 
    - Java
tags : 
    - Java
    - List
---

배열은 가장 기본적인 형태의 자료구조이다.  
구조가 간단하면서 사용하기 쉽고 데이터를 읽어오는데 걸리는 시간이 가장 빠르다는 장점을 가지고 있다.  
다음과 같은 단점을 가지고 있다.  

1. 크기를 변경할 수 없다.
   - 크기를 변경할 수 없으므로 새로운 배열을 생성해서 데이터를 복사해야한다.
   - 실행속도를 향상시키기 위해서는 충분히 큰 크기의 배열을 생성해야 하므로 메모리가 낭비된다.
  
2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.
   - 차례대로 데이터를 추가하고 마지막에서부터 데이터를 삭제하는 것은 빠르지만,
   - 배열의 중간에 데이터를 추가하려면 빈자리를 만들기 위해 다른 데이터들을 복사 해서 이동해야 한다.

위와 같은 배열의 단점을 보완하기 위해서 `링크드 리스트(LinkedList)`라는 자료구조가 고안되었다.  
배열은 모든 데이터가 연속적으로 존재하지만, 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다.  

![ArrayVsLinkedList](/assets/img/java/ArrayVsLinkedList.PNG)  

<br/>  

링크드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어 있다.

```java
class Node {
    Node next;
    Object data;
}
```  

링크드 리스트에서의 삭제는 간단하다.  
삭제하고자 하는 요소의 이전요소가 삭제하고자 하는 요소의 다음 요소를 참도하도록 변경하면 된다.  
단 하나의 참조만 변경하면 삭제가 이루어진다. 배열처럼 데이터를 이동하기 위해 복사하는 과정이 없기 때문에 처리속도가 매우 빠르다.  

![nodeDelete](/assets/img/java/nodeDelete.PNG)  

새로운 노드의 추가 역시 새로운 요소를 생성한 다음 추가하고자 하는 위치의 이전요소의 참조를 새로운 요소에 대한 참조로 변경해주고, 새로운 요소가 그 다음 요소를 참조하도록 변경하기만 하면된다. 처리속도 역시 빠르다.  

![nodeAdd](/assets/img/java/nodeAdd.PNG)  

링크드 리스트는 이동방향이 단방향이기 때문에 다음 요소에 대한 접근은 쉽지만 이전요소에 대한 접근은 어렵다.  
이 점을 보완한 것이 `더블 링크드 리스트(이중 연결리스트, Doubly Linked List)` 이다.  
이중 연결 리스트는 링크드 리스트에 참조 변수를 하나 더 추가하여 다음 요소에 대한 참조뿐 아니라 이전 요소에 대한 참조가 가능하도록 했다.  
이중 연결 리스트는 링크드 리스트보다 각 요소에 대한 접근과 이동이 쉽기 때문에 많이 사용된다.  

```java
class Node {
    Node next;   // 다음 노드의 주소를 저장
    Node prev;   // 이전 노드의 주소를 저장
    Object data; // 데이터를 저장
}
```  
![doubleLinkedList](/assets/img/java/doubleLinkedList.PNG)  

실제로 LinkedList클래스는 이름과 달리 '링크드 리스트'가 아닌 '더블 링크드 리스트'로 구현되어 있다.  
이는 링크드 리스트의 단점인 낮은 접근성(accessability)을 높이기 위한 것이다.  

LinkedList 역시 List인터페이스를 구현했기 때문에 ArrayList와 내부 구현방법만 다를 뿐  
제공하는 메서드의 종류와 기능은 거의 같다.  


## ArrayList와 LinkedList의 성능 차이  
![perfor](/assets/img/java/perform.PNG)  

링크드 리스트의 추가/삭제가 O(1)인 것은 삭제와 추가할 위치를 알고 있다는 가정하에 나온 값이다.  
모른다면 검색을 통해 데이터를 얻어야하니 O(n)이 된다. __보통 알고 있다고 가정하여 O(1)로 정의한다.__  

__사용 용도__
- 데이터의 조회가 자주 이루어질 때 ArrayList를 사용하는 것이 좋다.  
- 데이터의 삽입, 삭제가 빈번히 일어날 때 LinkedList를 사용하는 것이 좋다.  


참고 : 자바의 정석 3rd Edition