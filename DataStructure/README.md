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






                                          





