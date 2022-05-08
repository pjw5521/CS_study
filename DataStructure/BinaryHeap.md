## 힙(Heap) [= 이진 힙(Binary Heap)]

---

최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전 이진트리(complete binary tree)를 기본으로 한 자료구조

힙은 다음과 같은 속성을 가진다.

1. **완전 이진 트리(complete binary tree)**이다.
    1. 완전 이진 트리 : 모든 레벨의 노드가 채워져 있어야 하며, 마지막 레벨은 왼쪾부터 차 있어야 함
2. 부모노드의 키 값과 자식 노드의 키 값 사이에는 **대소관계가 성립**한다. (형제 사이에는 대소관계가 정해지지 않음)

### 힙의 종류

---

**1) 최대 힙 (Max Heap)**

- 부모 노드의 키 값이 자식 노드의 키 값보다 큰 힙
- 가장 큰 값이 루트 노드에 있음
- 최대값을 찾는 연산의 시간 복잡도는 O(1)

![heap1](https://user-images.githubusercontent.com/67946662/167283142-0addd3fe-8d69-4976-bde3-132dcbdaf974.png)


**2) 최소 힙 (Min Heap)**

- 부모 노드의 키 값이 자식 노드의 키 값보다 작은 힙
- 가장 작은 값이 루트 노드에 있음
- 최솟값을 찾는 연산의 시간 복잡도는 O(1)

![heap2](https://user-images.githubusercontent.com/67946662/167283149-9898089a-a54c-411a-8fee-c3955687d0a2.png)


### Heapify

---

- 이진트리에서 힙 속성을 유지하는 작업

- Max Heap에서의 heapify 작업
1. 요소 값과 자식 노드 값을 비교
2. 자식 노드 값이 크다면, 자식 중 큰 값으로 교환
3. 힙 속성이 유지될 때까지 1, 2번 과정 반복

- 구현

```python
def heapify(unsorted, index, heap_size):

    largest = index

    left_index = 2 * index
    right_index = 2 * index +1

    # 자식노드가 범위안에 드는지 확인, 자식노드가 부모노드보다 큰지 확인
    # 자식노드가 부모노드보다 크다면 인덱스 스위치

    if left_index < heap_size and unsorted[left_index] > unsorted[largest]:
        ### [loop1]. largest = 6
        largest = left_index

    if right_index < heap_size and unsorted[right_index] > unsorted[largest]:
        largest = right_index
   
    # 부모노드의 인덱스값이 바뀌었다면 자식노드의 값과 스위치

    if largest != index:
        unsorted[largest], unsorted[index] = unsorted[index], unsorted[largest]
        # 재귀 함수
        heapify(unsorted, largest, heap_size)
```
