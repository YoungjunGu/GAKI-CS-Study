# Data Structure(자료구조)

- Array vs LinkedList


</br>
<hr>

## Array vs LinkedList

#### Array

##### 장점 

- 논리적 저장 순서와 물리적 저장 순서가 일치한다.
- Index(인덱스)로 해당 Element(원소)에 접근가능하다.
- 인덱스의 값만 알고 있으면 `O(1)`에 가능하다.
- **Random Access**가 가능하다.

##### 단점

- 해당 원소의 접근은 인덱스를 알면 `O(1)에` 가능하지만 삭제의 경우 추가적인 작업이 필요하다.
	- e.g. int arr[100]의 정적 배열에서 arr[30]의 원소를 삭제 할 경우 남은 뒷부분은 앞으로 빈곳을 채우기 위헤 `shift`하는 작업이 필요하고 비용이 발생한다. 이때 시간 복잡도는 `O(n)`이 걸린다(n == 배열의 사이즈)
    - 규칙에 의해 정렬되어있는 배열에 원소를 삽입의 경우에도 마찬가지다 사이에 값을 삽입 하려고 하면 뒤로 값들을 밀어야 하기 때문에 `O(n)`이 걸린다.
- Array 삭제 기능에 대한 time complexity의 worst case O(n)이 된다.

</br>

#### LinkedList

##### 장점

- 배열의 삭제기능을 `O(1)`만에 가능하게 한다.
	- 각각의 원소들은 자기 다음에 어떤 원소인지 기억하고 따라서 이부분만 삭제와 삽입을 하게 되면 `O(1)`만에 가능하다
    
```c
int data; // 내가 찾고 싶어하는 linkedlist data 값
listPointer removeNode;
listPointer newNode;
// 이 경우는 LinkedList의 단점에 해당한다
for(temp = head; temp->link; tmpe = temp ->link) {
  if(temp->link->data == data)
    break;
}
//삭제 기능
removeNode = temp->link;
temp->link = removeNode->link; // 그 다음 linkedList를 가르키게 하고
free(removeNode);

//추가 기능(data를 갖는 linkedlist 이전에 삽입한다 가정)
newNode->link = temp->link;
temp->link = newNode;  

```

> 결론) Array의경우에는 뒤로 밀리거나 삭제되었을 시 빈공간을 재정렬(shift)하는 작업을 추가 적으로 해주어야 하는데 LinkedList의 경우에는 그런 작업이 필요없이 O(1)만에 가능한것을 위의 코드를 통해 확인 할 수 있다. 

##### 단점

- 위의 `for()` 구문에 보면 내가 삽입이나 삭제를 하고싶은 원소를 찾으려면 필연적으로 head부터 탐색을하여 원하는 원소의 값이 있는 linkedList로 탐색을 해야하는 작업을 해주어야 한다(Array의 경우 Index만 알게 되면 바로 접근이 가능한것과 상반되는 특징)
- 결국 추가 삭제시에는 탐색 작업이 `O(n)`만큼 발생하게 된다.

</br>

<hr>

## Stack and Queue

#### Stack

선형 자료구조의 일종으로 `Last In First Out(FIFO)`구조이다. 즉 나중에 들어간 원소가 먼저 나온다. 

#### Queue

선형 저료구조의 일종으로 `First In First out(FIFO)`. 즉 먼저 들어간 놈이 먼저 나온다.

</br>

<hr>

## Tree

- 트리는 스택이나 큐와 같은 선형구조가 아닌 **비선형 구조**이다.
- 츠리는 계층적 관계(Hierarchical Relationshhip)을 표현한다.

#### 트리 용어

- Node (노드) : 트리를 구성하고 있는 각각의 요소를 의미한다.
- Edge (간선) : 트리를 구성하기 위해 노드와 노드를 연결하는 선을 의미한다.
- Root Node (루트 노드) : 트리 구조에서 최상위에 있는 노드를 의미한다.
- Terminal Node ( = leaf Node, 단말 노드) : 하위에 다른 노드가 연결되어 있지 않은 노드를 의미한다.
- Internal Node (내부노드, 비단말 노드) : 단말 노드를 제외한 모든 노드로 루트 노드를 포함한다.



