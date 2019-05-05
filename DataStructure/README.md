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

## Red Black Tree

- RBT(Red-Black Tree)는 BST를 기반으로 하는 트리형식의 자료구조이다.
- SEarch, Insert, Delete에 `O(log n)`의 시간 복잡도가 소요된다.
- 동일한 노드의 개수일 때, hight를 최소화 하여 시간 복잡도를 줄이는 것이 핵심 아이디어이다.
- 동일한 노드의 개수일때 hight 가 최소가 되는 경우는 tree 가 complete binary tree인 경우이다.


 이진 트리에서 Inorder Traversal(중위순회)시에 오름차순으로 순회가 되는 구간이 존재 할경우 또는 그 구간이 상당이 길어지게 되면 BST의 경우 일렬로 길게 오른쪽으로 한 없이 길어지게 되는 트리의 모양을 하게 된다 그렇게 되면 최악의 경우는 O(hight) 높이 만큼의 시간복잡도를 가진다. 하지만 RBT의 경우는 **Balanced BST**이므로 균형을 이루면서 BST의 성질을 가진다.  
이때 삽입 시에 삭제 시의 조건이 RBT를 Balanced 하게 유지하는 규칙이 몇가지 존재한다.

#### 기존의 RBT 조건  

1. Root Property: Black
2. External Property: Black
3. Internal Property: Red 노드의 자식은 Black(== **No Double Red** 빨간색 노드 연속으로 나올 수 없다.)
4. Depth Property: 모든 leafNode에서 Black Depth는 같다(== 리프노드에서 로트노드까지 가는 경로에서 만나는 블랙노드의 개수는 같다)

### RBT 삽입 

- 새로 삽입 되는 노드는 반드시 Red색 이어야 한다.  

하지만 위의 경우 3번 조건을 위배하게 되고 우리는 Double Red 문제를 해결하기 위해 두가지 전략을 세워 RBT를 Balance하게 유지해야한다.  

#### Restructuring

![image](https://user-images.githubusercontent.com/33486820/57152326-245a3580-6e0e-11e9-947a-b4548208b745.png)

#### ReColoring

![image](https://user-images.githubusercontent.com/33486820/57152820-849da700-6e0f-11e9-9492-3e586c9a4976.png)


> 결론) 두 작업 모두 **O(log n)** 이 걸리게 된다.


### RBT 삭제

삭제의 경우도 마찬가지로 BST의 특성을 유지하면서 해당 노드를 삭제한다. 삭제될 노드의 child의 개수에 따라 rotation 방법이 달리게된다.  

- 삭제될 노드 Black: Black-Height가 1감소한 경로에 Black Node가 1개 추가되도록 rotation 하고 노드의 색깔을 조정한다.
- 삭제될 노드 Red: Violation이 발생하지 않으므로 RBT가 그대로 유지된다.

> 참고) Java Collection 에서 ArrayList도 내부적으로 RBT로 이루어져 있고, HashMap 에서의 Separate Chaining에서도 사용된다.

</br>
<hr>

## Graph

### 용어 정리

#### Graph

- Vertex와 Edge의 집합으로 이루어진 그래프
- **유한**하고 **Nonempty**한 vertices 집합
- `G = (V, E)`

#### Undirected Graph

- 방향성이 없는 그래프
- (u, v), (v, u) 같다.

#### Directed Graph

- 방향성이 있는 그래프

#### Restrictions on Graph

- 자기 자신으로 가는 edge 없다.
- 같은 edge가 여러개 나타날수 없다.

#### Complete Graph

- 최대한의 edge개수를 갖는 그래프
- 모든 vertex끼리 edge로 연결되어있어 edge의 개수는 `n*(n-1)/2` (n: Vertex개수)

#### SubGraph

- vertex한개도 subgraph가능하다
- 기존의 vertex로만 subgraph 생성 가능하다.(추가적인 vertex로는 불가능)

#### 그 밖의 그래프 용어

- Path: vertex 에서 vertex로 이동할때 지나치는 모든 vertex 들의 경로
- Length: 그런 path의 길이 즉 edge의 개수
- Simple Path: path상 vertex가 중복되지 않는 path (시작과 도착은 같아도 된다)
- Cycle: Simple path에서 자기자신 즉 시작과 도착이 같은 path를 Simple Cycle이라고 한다.
- Connected Graph: 모든 vertex사이에 연결이 있는 graph
	- e.g. Tree 의 경우 Cycle을 가지지 않는 Connected Graph
- Connected Component: Graph 의 SubGraph 중 모든 vertex 상에 대한 Maximal(최대로) Path가 존재하는 Subgraph
- Strongly Connected: u->v , v->u 로 서로 가는길이 존재하면 두 vertex는 "강하게 연결"되어있다고 한다.
- Degree: 자기에게 붙어 있는(인접한) 모든 edge의 개수
	- Directed Graph에서는 Degree가 두개로 나뉜다. 
    - in-degree: head의 개수 즉 들어오는 edge의 개수
    - out-degree: tail의 개수 즉 나가는 edge의 개수
    
> 참고) 기존의 graph 라는 용어는 방향성이 없는 undirected 한 그래프를 말하고 방향성이 있는 그래프는 Digraph라고 지칭한다.

</br>

### 그래프를 구현하는 두 방법

#### 인접 행렬(Adjacency Matrix): 정방 행렬을 사용하는 방법

- 해당 하는 위치의 value 값을 통해서 vertex 간의 연결 관계를 O(1)으로 파악할 수 있다.
- Edge의 개수와는 무관하게 S(v^2)의 space Complexity를 갖는다.
- Dense graph를 표현할 때 적절한 방법이다.

#### 인접 리스트(Adjacency List): 연결리스트를 사용하는 방법

- vertex의 인접 리스트를 확인해봐야 하므로 vertex간 연결되어있는지 확인하는데 오래걸린다.
- space complexity 는 O(E+V)이다.
- Sparse graph를 표현하는데 적당한 방법이다.

</br>

### 그래프 탐색

#### 깊이 우선 탐색(Depth First Search: DFS)

일단 연결되어있는 정점으로 탐색을 하는 것이다. 연결 할 수 있는 정점이 있을 떄까지 계속 연결하다가 더이상 연결되지 않은 정점이 없으면 바로 전단계로 BackTracking하여 연결할수 있는 정점이 있는지 살펴야 한다. 갔던 길을 다시 되돌아 와야 하기 때문에 순차적으로 방문한 노드를 **Stack**에 삽입하고 더이상 갈곳이 없는 상황에 봉착했을 시 pop을 해가면서 이전의 노드에서 새로 갈곳을 찾아 가면된다.  

- **Time Complexity: O(V+E)**  
- Stack을 이용한 dfs 구현

```c
void dfs(int start, vector<int> graph[], bool check[]){

	stack<int> stack;
	stack.push(start);
	check[start] = true;
	printf("%d ",start);

	while(!s.empty()){
		//맨 위의 node 를 가져온다
		int current_node = stack.top();
		stack.pop();
      	
		for(int i=0; i<graph[current_node].size(); i++){

			int next_node = graph[current_node][i];
			// 인접 행렬로 주어진 그래프에서 갈곳이 있으면 stack에 넣어준다.
			if(check[next_node]==false){
				printf("%d ", next_node);
				check[next_node] = true;
				// pop()을 했었기 때문에 현재 current_node도 넣어줘야한다.
				stack.push(current_node);
				stack.push(next_node);
				break;
			}
		}
	}

}
```


#### 너비 우선 탐색(Breadth First Search: BFS)

임의의 한 정점으로 부터 연결되어있는 모든 정점으로 나아간다. Tree의 Level Order Traversal(레벨순회) 형식으로 진행 되는 것이다. **Queue**를 사용하여 해당 정점에서 갈수 있는 모든 정점을 Queue에 삽입하고 하나씩 Queue에서 deleq를 하면서 다시 그 정점에서 갈 곳을 Queue에 addq 하면된다.  

- **Time Complexity: O(V+E)**  
- Queue를 이용한 bfs 구현

```c
void bfs(int start, vector<int> graph[], bool check[]){
	queue<int> q;

	q.push(start);
	check[start] = true;

	while(!q.empty()){
		int tmp = q.front();
		q.pop();
		printf("%d ",tmp);
		for(int i=0; i<graph[tmp].size(); i++){

			// 방문하지 않았다면
			if(check[graph[tmp][i]] == false){
				// 큐에 넣어주고 방문했음을 표시한다.
				q.push(graph[tmp][i]);
				check[graph[tmp][i]] = true;
			}
		}
	}
}
```

</br>

### Spanning Tree

- 그래프의 모든 vertex를 최소한의 edge로 방문한 tree 이다.
- DFS나 BFS를 통한 탐색으로 MST를 만들어 낼 수 있다.
- edge를 하나만 추가하여도 Cycled이 생기고 tree에서 graph로 된다.
	- 단 기존의 그래프에 존재하던 edge를 추가해야한다.
- n 개의 vertex 경우 n-1개의 edge가 생성된다.  


### Minimun Spanning Tree(MST)

그래프 G의 Spanning tree 중 edge weight의 합이 최소인 Spanning Tree를 말한다.  

#### Greedy Method(그리디)

- 매 단계에서 최적의 값(Optimal Solution)을 선택
- 각 단계에서 매순간 최상의 선택을 보장받는다.
- "cannot change this decision later", 한번 선택한 결정은 번복이 불가능하다.  
- Kruskal's, Prim's, Sollin's 등

> 참고) 그리디는 매순간 최고의 값을 선택하기 때문에 음수가 있는 그래프에는 적용할 수가 없다 왜냐하면 Cycle이 발생하기 때문이다. 그렇기 때문에 음수를 제어하거나 다른 방법의 알고리즘 전략을 사용해야한다.  

(자세한건 알고리즘에서 확인 가능합니다.)

### Kruskal's Alogorithm

- edge weight 가 작은 vertex 끼리 우선 연결한다.
- 매순간 **Cycle Check** 가 필수 적이다.
	- Weighting Union을 사용하여 부모의 node가 같으면 Cycle 발생  
    
> Q) Weighting Union을 어떻게 적용시키지?

Graph의 각 vertex에 `vertexWeight`라는 변수 선언 후 초기에는 -1을 부여하고 연결이 발생할때 이 변수의 값이 큰(절대값을 취했을때) 값을 연결 된 대상과 통일 시키면서 연결을 계속한다.이 때 변수의 값이 -1인 곳은 아직 아무런 연결이 되지 않았다는 의미로 생각하면된다. 


![image](https://user-images.githubusercontent.com/33486820/57173517-0b806d00-6e6c-11e9-8026-9a2da908014d.png)


- Time Complexity
	- Edge 의 weight 를 기준으로 sorting - O(E log E)
	- cycle 생성 여부를 검사하고 `vertexWeight` 를 통일 - O(E + V log V) => 전체 시간 복잡도 : O(E log E)

</br>

### Prims's Algorithm

- 시작 vertex부터 시작해서 인접한 vertex와의 가장 작은 weight를 이어나가면서 MST생성
- Cycle check가 필요가 없다.
- 방문한곳은 재방문을 하지 않기 위해 `visited[]` 배열을 선언하여 매순간 check해야한다.

![image](https://user-images.githubusercontent.com/33486820/57173546-7a5dc600-6e6c-11e9-9bd3-78bc2132896e.png)

- Time Complexity
	- 전체 시간 복잡도 : O(E log V)

</br>

### Biconnected Components(이중연결성분)

단절점(Articulation Point)를 갖지 않는 Connected graph를 말한다.  


#### Articulation Point(단절 점)

그래프 G의 정점들 중에서 그 정점을 그 정점에 부속한 보든 간선들과 같이 삭제하면 최소한 2개의 연결 요소를 갖는 그래프 G를 생성하는 정점 V를 말한다.

##### 단절 점 되는 조건

- 자식이 두개 이상일때
- 자식의 low가 자신의 dfn값보다 크거나 같을때 (dfn: dfs시 부여되는 순서번호)  

![image](https://user-images.githubusercontent.com/33486820/57173303-90698780-6e68-11e9-8933-a4c7c34f4327.png)

> 참고) 이런 단절점은 통신국을 세울때 단절점 정점에 해당하는 곳에 통신국을 세울 경우 여러 통신국간의 단절을 초례할 수 있는 문제가 있다.

![image](https://user-images.githubusercontent.com/33486820/57173418-a5dfb100-6e6a-11e9-8f73-faddc5696ff1.png)


</br>
<hr>

## Sorting

### 각 Sorting 알고리즘 비교

|Strategy|in-place|stable|Time-Complexity|
|:---|:---|:---|:---|
|Bubble|  o  |  o  |O(n^2)|
|Selection|  o  |  o  |O(n^2)|
|Insertion|  o  |  o  |O(n^2)|
|Merge|  x  |  o  |O(n log n)|
|Heap|  o  |  x  |O(n log n)|
|Quick|  o  |  x  |O(n log n)|
|Radix|  x  |  o  |d x O(n)|
|Counting|  x  |  o  |O(n + k)|


#### In-Place

입력리스트 내부에서 정렬이 이뤄 지는 경우를 가리킨다. 반대는 정렬 도중에 별도 저장공간을 필요로 하는 경우이다. Merge Sort의 경우 입력 리스트를 분할해 이를 정렬하고 다시 합치는 과정에서 분할된 리스트를 별도로 저장해 두어야한다. Counting Sort과 Radix Srot는 입력값의 빈도를 세어서 저장 해두는 변수. 결과리스트를 저장해 둘 변수가 필요하다.  

</br>

### Bubble Sort(버블 정렬)

![image](https://user-images.githubusercontent.com/33486820/57178065-3be4fd00-6ea6-11e9-97c1-4c7df8313887.png)

```c
void bubbleSort(int list[], int size) 
{
  //배열에서 두개의 인자를 비교 하므로 size - 1회 반복한다.
  for(int i = size - 1; i > 0; i--) {
    for(int j = 0; j < i; j++){
      if(list[j] < list[j+1])
      	SWAP(list[j],list[j+1];
    }
  }
}
```

- 장점
	- 구현이 매우 간단하다.(직관적이다)
- 단점
	- 순서에 맞지 않는 요소를 인접한 요소와 무조건 교환한다.
    - 최악의 경우 맨 왼쪽에 가장 큰값이 있는 경우 또는 내림차순인 경우 오른쪽으로 이동 할때 모든 배열의 요소들과 교환되어야 한다( O(n^2)인 이유)
    - 자기자리를 찾았음에도 불구하고 이동 될 수 있다. 즉 불필요한 이동이 발생한다.
- 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동작업 보다 더 복잡하기 때문에 버블정렬은 거의 쓰이지 않는다.  

</br>

### Selection Sort(선택 정렬)

![image](https://user-images.githubusercontent.com/33486820/57178356-aa778a00-6ea9-11e9-93bf-0db11a12413d.png)

```c
void selectionSort(int list[], int size) 
{
  for(int i = 0; i < n - 1; i++) {
    int minPosition = i;
    
    for(int j = i + 1; j < size; j++) {
      if(list[j] < list[minPosition])
        minPosition = j;
    }
    
    if(i != minPosition)
      SWAP(list[i], list[minPosition]);
  }
}
```  

- 장점
	- 자료 이동 횟수가 미리 결정된다.
- 단점 
	- n^2 의 고정적인 정렬 속도가 한계다.
    
</br>    

### Insertion Sort(삽입 정렬)

```c
void insertionSort(int list[], int size) 
{
 	for(int i = 2; i <= size; i++) {
      int key = list[i];
      insert(key, list, i - 1);
    }
}

void insert(int key, int list[], int i) 
{
  while(key < list[i]) {
    list[i+1] = list[i];
    i--;
  }
  list[i+1] = key;
}

```

- key 기준 배열 좌측으로 비교를 한다
	- `key < list[i]` 이면 오른 쪽으로 이동
   	- 작으면 종료하고 그 자리에 key값 삽입 하고 종료한다.
- `insert()`함수에서 while문에 `<=`를 붙이면 stable에서 unstable이 된다.

### Quick Sort(퀵 정렬)

![image](https://user-images.githubusercontent.com/33486820/57179070-9be2a000-6eb4-11e9-9144-db03ecccf96d.png)

```c
vod quickSort(int list[], int left, int right)
{
  int pivot,i,j;
  
  if( left < right) {
    // 초기의 left = 0 ,rifht = list의 size - 1 이다.
  	i = left;
  	j = right;
      // pivot은 우선 처음 값으로 잡겠다 하지만 문제가 발생하니 밑에서 설명하겠다.
      pivot = list[left];
      do {
        // i : pivot 보다 큰 값 찾기 
        do i++ while (list[i] < pivot);
        // j : pivot 보드 작은 값 찾기
        do j-- while (list[j] > pivot);
        // i , j 값이서로 역전이 되지 않을때 두 자리의 값을 SWAP한다
        // pivot을 기준으로 작은 값 왼쪽 큰 값은 오른쪽으로 배치하게 된다.
        if(i < j)
          SWAP(list[i], list[j]);
      } while (i < j);
      // 실제 분할 정복을 수행할 부분, pivot을 중앙에 배치하고 pivot 기분 반으로
      // 나누어 다시 quickSort를 수행한다.
      SWAP(list[left], list[j]);
      quickSort(list, left, j - 1);
      quickSort(list, j + 1, right);
  }
}
```
- 장점
	- Quick Sort는 우선 O(nlogn)의 복잡도를 가지는 정렬 방법 중에 가장 빠르다
	- 추가 메모리 공간을 필요하지 않는다(in-place)
    
#### QuickSort의 Worst Case( 최악의 경우 )

퀵정렬의 유일한 문제점은 바로 **이미정렬이 되어있는 구간에서** 발생한다.  
이 경우 불균형 분할이 발행하고 오히려 수행시간이 더 많이 걸리게 된다(O(n^2) 이 걸린다)  
이 경우 해결 책은 **Pivot 의 설정** 이 중요하다.  
위의 코드에서는 Pivot을 단순하게 맨 왼쪽 처음 인자로 정했는데 그렇게 하게되면 불필요한 분할이 많이 일어난다 그렇기 때문에 Pivot을 중간값으로 설정하거나 random하게 설정을 하게 되면 이러한 불균형 분할을 조금이나마 완화 할 수 있거나 피하게 된다.  

</br>

### Sorting에 관하여

Sorting 작업은 **O(n log n) 이하로 작아 질수 없다**

</br>

### Merge Sort

- 하나의 list를 두개의 균등한 크기로 분할하고 분할된 부분 리스트를 정렬한다음 , 두개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다. 
- merge sort의 단계
	- 분할(Divide): 입력 배열을 같은 크기의 2개의 subList로 분할 한다.
    - 정복(Conquer): subList를 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.
    - 결합(Combine): 정렬된 subList를 하나의 list에 merge 한다.

<img width="704" alt="image" src="https://user-images.githubusercontent.com/33486820/57180714-5dee7780-6ec6-11e9-9d23-a996c2bcff41.png">

출처: https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html

```c
void merge(int list[],int mergedList[], int left, int mid, int right) 
{
  int i, j ,k;
  i = left;
  j = mid + 1;
  k = i;
  
  // 분할된 list를 순서대로 접근하면서 merge한다
  // i , j 각각 분할된 두 list에 접근 할 인덱스 번호이다.
  // 접근할 때 sparse matrix 다항식 덧셈 하듯이 인자를 비교하면서 mergedList에 넣는다.
  while(i <= mid && j <= right) {
    if(list[i] <= list[j])
      mergedList[k++] = list[i++];
    else
      mergedList[k++] = list[j++];
  }
  
  // 서로 남아있는 분할 리스트의 인자를 일괄로 mergedList 복사한다.
  if(i > mid) {
    // 오른쪽의 분할 List가 남아있을 경우
    for(int s = j; s <= right; s++)
      mergedList[k++] = list[s];
  } else {
    // 왼쪽의 분할 List가 남아있을 경우
    for(int s = j; s <= mid; s++)
      mergedList[k++] = list[s];
  }
  // 배열 mergedList[]의 리스트를 배열 list로 재복사한다.
  
  for(int s = left; s<= right; s++)
    list[s] = mergedList[s];
}

void mergeSort(int list[], int mergedList[], int left, int right)
{
  int mid;
  // merge Sort 재귀 종료 조건
  if(left < right ) {
    // 분할(Divide)
    mid = (left + right) / 2;
    // 앞쪽 부분 정복(Conquer)
    mergeSort(list, mergedList, left, mid);
    // 뒤쪽 부분 정복(Conquer)
    mergedList(list, mergedList, mid + 1, right);
    // 정렬된 2개의 subList를 결합(Combine)
    merge(list, mergedList, left, mid, right);
  }
}
```

- 단점
	- 레코드를 배열로 구성하면, 임시 배열이 필요하다(not In-place)
    - 레코드들의 크기가 큰 경우에는 이동 횟수가 많아지므로 상당히 큰 시간적 낭비를 초래한다.
- 장점
	- 레코드를 연결리스트로 구성하면 , 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아진다 즉 in-place한 성질로 구성할려면 **연결리스트**로 구현하면 된다.  
    

</br>

### Heap Sort

#### Heap

- FBT(완전 이진 트리)의 일종으로 **Priority Queue**를 위하여 만들어진 자료구조이다.
- 목적: 최대값, 최솟값을 O(1)에 추출 할 수 있게 하는 자료구조

#### Max Heap or Min Heap

1. 힙에 새로운 요소가 들어오면, 새로운 노드를 힙의 마지막 노드에 이어서 삽입하고
2. 이어서 힙의 성질을 만족 시키면서 위치를 찾아 가면 된다.

#### Max Heap 삽입 연산

```c
vod insertMaxHeap(int heap[], int item) 
{
  int i;
  // 현재 힙사이즈 
  // FBT 에서 배열로 접근했을때 부모 자식 관계를 Index로 찾을 수 있다.
  i = ++heapSize;
  // Bottom up으로 Heap Tree의 바닥에서 부터 위로 올라가면서 들어갈 위치를 찾는 작업
  // i = 1 이면 heap Tree의 root Node, 부모 노드의 값이 자식 보다 작을때 부모를 밑으로 보내고 다시 상위의 부모를 판단 하기 위해 index i 값을 반으로 줄인다.
  while((i != 1) && ( item > heap[i/2])) {
    heap[i] = heap[i/2];
    i /= 2;
  }
  // 들어갈 위치를 찾았으면 새로운 노드 정보 삽입
  heap[i] = item;
}
```

heap Sort는 전체 자료를 정렬하기 위함이 아니라 **가장 크거나 작은 값** 에 초점을 두어 빠르게 가져오고 싶을때 사용한다.  
우선 그렇게 하기 위해 O(n log n) 이 소요되고 , 정렬 해놓은 상태에서 O(1) 만에 최댓갓, 최솟값을 추출 할 수 있다.  

</br>

<hr>

## Hashing

### Hash Table

hash는 내부적으로 배열을 사용하여 데이터를 저장하기 떄문에 빠른 검색 속도를 갖는다.  특정한 값을 Search 하는데 데이터 고유의 `index`로 접근하게 되므로 Time Complexity O(1)이 된다. 하지만 문제는 이 인덱스로 저장되는 key 값이 불규칙하다는 것이다.  


> 참고) Hash Search는 O(1)이 항상 되는 것이 아니다. Average Case에 대해서 O(1)이다. 그 이유는 **Collision** 떄문이다. 밑에서 다루겠다.  

그래서 저장할 데이터와 연관된 **고유한 숫자**를 만들어 낸 뒤 이것을 인덱스로 사용한다. 고유의 숫자이기 때문에 데이터 마다 고유한 위치를 가진다. 삽입 연산 시 다른 데이터의 사이에 끼어들거나, 삭제 시 다른 데이터로 채울 필요가 없으므로 연산에서 추가적인 비용이 없도록 만들어진 구조이다.  

</br>

### Hash Function  

**알고리즘을 통해 데이터 마다의 고유의 숫자를 설정**하는 것이 Hash에서 중요하다.  
이 알고리즘을 `해시함수(Hash function)`이라고 하고 이 메소드에 의해 데이터의 값은 고유의 숫자 즉 `hashcode`라고 한다. 저장 되는 데이터의 key 값들을 해시 함수를 통해 데이터의 수보다 작은 범위의 값들로 바꿔준다.  
  
하지만 어설픈 hash function을 통해서 key 값들을 결정한다면 **동일한 값이 도출 될 수 있다.** 데이터를 Key로 간소화하여 저장한다는 아이디어는 좋지만 이처럼 잘못된 Hash function을 설정하여 Key를 만들어 낼 경우 **같은 데이터에 대해 동일 한 key가 생성** 될수 있다. 이러한 문제는 Hash Table에서 특정한 bucket에 데이터들이 집중된다는 뜻이고 이것을 **Collision(충돌)** 이라고 한다.  

> 참고) Hash Table은 한정적 이고 반대로 입력값은 무한대로 들어올 수 있기때문에 Collision은 반드시 일어난다. 이러한 충돌을 완화 하기위해 단일 Table이 아닌 각 Table의 고유 key 값에 **Slot**의 개념을 더해 여러개의 같은 key값을 가지는 데이터에 대해 중복 저장을 가능하게 할 수 있다. 하지만 slot이 많아지게 되면 Hash의 성질을 잃어 버리게 되고 또 적게 되면 Slot이 꽉 차있는 상태에서 데이터가 계속 들어오는 **Overflow**가 발생한다.(비둘기집 원리)  


그러므로 Hash function을 잘 정의하여 hash collision을 최소화 하는 것이 성능개선에도움이 된다.  


#### 좋은 hash function의 조건은?

일반적으로 좋은 hash function은 일부분을 참조하여 해쉬 값을 만들지 않고 키 전체를 참조하여 충돌없이 각각의 데이터 마다 고유의 key값을 만드는 것이 좋다. 하지만 무조건 1:1로 만들다 보면 그것은 hash를 사용하는 의미가 없고 단순 배열의 형태를 하고 메모리를 많이 차지하는 문제 때문에 Hash의 성질을 잃어 버리게 된다.  
  
가장 중요한 것은 Collision을 최소화하는 방향으로 설계하고 Collision에 대비해 어떻게 대응할 것인가가 더 중요하다.  

Collision이 많이 발생 할 경우 Search에 장점이 있던 hash의 O(1)은 점점 O(n)에 가까워 지게 된다. 이것은 배열의 Search와 같게 된다는 말이다.  

> 참고) 한국의 국가보안기술연구소(NSR)에서 발표한 해시함수 LSH(Lightweight Secure Hasg고속 경량 해시)알고리즘은 w비트 워드 단위로 동작하여 n비트 출력값을 가지는 고속 경량 해시 암호화 알고리즘이다. 기존의 국제 표준인 SHA-2/3 대비 2배 이상의 성능을 가진다.



### Collision Conflict 해결

#### 1. Open Address 방식(개방주소법)

해시 충돌이 발생하면,(즉 삽입하려는 해시버킷이 이미 사용 중인 경우) **다른 해시 버킷에 해당 자료를 삽입하는 방식**이다.
데이터의 key값에 이미 다른 데이터가 들어와있으면 Hash Table 내에서 빈공간을 찾아 내가 들어갈 곳을 해메게 되고 최악의 경우 찾다가 다시 시작 위치로 돌아올 수 도있다.

</br>

1. Linear Probing(선형 탐사)
	- 순차적으로 탐색하며 비어있는 버킷을 찾을 때까지 계속 진행된다.
    - `% TableSize`만큼 Mod연산을 통해 원형으로 탐색을 할수있게 알고리즘을 짜야한다.
    - 적재 밀도(load-factor)가 0.75이상이 되면 Hash Table을 늘려야한다.
    - 계속되서 Collision이 발생할 경우 Hash Table은 증가하게 되고 일반 배열과 다를 바가 없게되므로 점점 O(n)이 걸리게 되는 문제가 있다.  
    
</br>    
  
2. Quadratic Probing(제곱 탐사)    
	- 고정 폭으로 이동하는 선형탐사와 달리 그 폭이 제곱수로 늘어난다.
    - 충돌 발생시 1^2, 2^2, 3^2,,,,로 이동하면서 데이터를 저장한다.
	- Cluster의 확장을 줄이는 것이 중요하다.
    - 초기 해시값이 같으면 다음 탐사 위치 또한 고정으로 동일 하기 때문에 효율 성이 떨어진다. 

</br>

3. Double Hashing (이중해싱)
	- 탐사할 해시값의 규칙성을 없애버려 clustering을 방지하는 기법이다.
    - 2개의 해시함수를 준비하여 최초의 해시값, 해시충돌이 일어났을때 탐사 이동폭을 얻기 위해 사용 한다.
    
#### 2. Separate Channing 방식 (분리 연결법)

일반적으로 개방 주소법은 체이닝 방식 보다 느리다. 개방 주소법의 경우 해시 버킷을 채운 밀도가 높아질수록 Worst Case 발생 빈도가 더 높아 지기 때문이다. 반면 체이닝 방식의 경우 해시 충돌이 잘 발생하지 않도록 보조 해시 함수를 통해 조정할 수 있다면 Worst Case에 가까워 지는 빈도를 줄일 수 있다. 

> 참고) Java 7 에서는 Spearate Chainning 방식을 사용하여 HashMap을 구현하고있다.

- 연결리스트를 사용하는 방식(Linked List)
	각각의 버킷들은 연결리스트로 만들어 Collision 발생하면 해당 버킷의 List에 추가하는 방식이다.삭제 또는 삽입이 간단하고, Search나 데이터 저장할 때 연결리스트 자체의 오버헤드가 부담이 된다. 개방 주소법에 비해 Hash Table의 확장을 늦출 수 있다.
    
- Tree를 사용하는 방식(Red - Black Tree)
	기본적인 알고리즘은 Separate Chaining 방식과 동일하며 연결 리스트 대신 트리를 사용하는 방식이다. 이것의 차이는 하나의 해시 버킷에 할당된 Key-Value 쌍의 개수이다. 데이터가 적으면 연결리스트가 맞지만 트리는 기본적으로 메모리 사용량이 많기 때문이다. 
    
#### 데이터가 적다는 것은 얼마나 적다는 것을 의미하는가?

연결리스트와 트리의 기준은 하나의 해시 버킷에 할당된 Key-Value쌍의 개수이다. 이 키-값 쌍의 개수가 6개, 8개를 기준으로 결정한다.링크드 리스트의 기준과 트리의 기준을 6과 8로 잡은 것은 변경하는데 소요되는 시간을 줄이기 위함이다.  

#### 예제

해시 버캇에 6개의 key-value 쌍이 들어있다. 그리고 하나의 값이 추가되었다. 만약 기준이 6과 7이라면 자료구조를 연결리스트에서 트리로 변경해야한다. 그러다 바로 하나의 값이 삭제 되면 다시 트리에서 링크드 리스트로 변경해야한다. 그 사이의 tree -> linkedList의 변경 기준이 6,7 즉 1이라면 Switching 비용이 너무 많이 필요하게 된다. 그래서 2라는 여유를 남겨두고 기준을 잡아준 것이다. 따라서 데이터의 개수가 6개에서 7개로 증가했을 떄는 linedlist의 자료구조를 취하고 있을것이고 8 개에서 7개로 감소 했을 때는 트리의 자료구조를 취하고 있을 것이다.

#### Open Address vs Separate Chaining

두 방식모두  Worst Case 는 O(M)이다. 하지만 개방주소 방식은 연속된 공간에 데이터를 저장하기 떄문에 체이닝에 비해 캐시 효율이 높다. 데이터 개수가 충분히 적다면 `Open Address` 방식이 `Separate Chaining`보다 더 성능이 좋다. 한가지 차이점이 존재한다. `Separate Chaining`방식에 비해 `Open Address`방식은 버킷을 계속해서 사용한다. 따라서 `Separate Chaining`방식은 테이블의 확장을 늦출 수 있다.

### 해시 버킷 동적 확장(Resize)

해시 버킷의 개수가 적다면 메모리 사용을 아낄 수 있지만 해시 충돌로 인해 성능상의 손상이 발생한다. 그래서 HashMap은 key-value 쌍 데이터 개수가 일정 개수 이상이 되면 해시 버킷의 개수를 두배로 늘린다. 이렇게 늘리면 해시 충돌로 인한 성능 손실 문제를 어느정도 해결 가능하다. load factor 가 `0.75` 즉 75% 이상이면 해시 테이블의 사이즈를 늘린다.  


### Directory를 사용한 동적 해싱


참고 : http://d2.naver.com/helloworld/831311












                                          






