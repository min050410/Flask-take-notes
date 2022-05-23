# heap sort 개념

자료구조 힙

c++에서 priority_queue<int> 자료형으로 구현 가능한 자료구조이다.

기본적으로 트리 자료 구조를 가지고 있으며,  
max heap과 min heap이 존재하는데 우선순위 큐를 위해 만들어진 자료구조이다. 

우선순위 큐를 이용하면 최댓값 or 최솟값을 log n 의 복잡도로 뽑아낼 수가 있다. 

대표적인 사용처는 min heap을 이용한 다익스트라 알고리즘이다. 

### 힙 정렬이란

최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법이다.

과정

i. 정렬해야 할 n개의 요소들로 최대 힙을 만든다.  
-> 오름차순 기준이라면 최소 힙을 사용한다.

ii. 그 다음으로 한번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤부터 저장한다.

iii. 삭제되는 요소들은 값이 감소되는 순서로 정렬되게 한다.

**코드**
```cpp
void heap_sort(element a[], int n){
    int i;
    HeapType h;

    init(&h);

    for (i=0; i<n; i++){
        insert_max_heap(&h, a[i]);
    }
    for (i=(n-1); i>=0; i--){
        a[i] = delete_max_heap(&h);
    }
}
```
### 시간 복잡도

거의 완전 이진트리여서 삽입 or 삭제시 `log2n`

요소의 개수가 n 개이므로 최종적으로
`O(nlog2n)`의 시간이 걸린다

![](https://gmlwjd9405.github.io/images/algorithm-heap-sort/sort-time-complexity.png)




