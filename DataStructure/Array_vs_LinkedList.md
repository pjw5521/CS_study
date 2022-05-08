# DataStructure

</br>

## Array이란 ?

연관된 데이터를 모아서 관리하기 위해 사용되는 데이터 타입으로 여러개의 데이터를 갖고 관리하고 저장하기 위한 자료구조이다.

![스크린샷 2022-05-08 오전 12 53 04](https://user-images.githubusercontent.com/60414900/167261972-ca9ad98d-713c-4df7-ba63-e7d778bbee4a.png)

특징
- 논리적 저장 순서와 물리적 저장순서가 일치하기 때문에 index로 원소에 접근이 가능하다. (Random Access)

- 연산 수행 시간(BigO)
  - 접근: O(1)
  - 삽입(Pop): O(N)
  - 삭제(Peek): O(N)

</br>

## LinkedList란 ?

각 노드가 데이터와 포인터를 갖고 한줄로 연결되어 잇는 방식으로 돠어있는 자료구조이다.

![스크린샷 2022-05-08 오전 12 53 20](https://user-images.githubusercontent.com/60414900/167261983-86e9b7da-8bf4-4931-a2a1-bbd358c55c8d.png)

- 연산 수행 시간(BigO)
  - 접근: O(1)
  - 삽입(Pop): O(N)
  - 삭제(Peek): O(N)

</br>

## Array vs LinkedList

- 차이점   
  Array의 경우는 요소들이 인접 메모리에 저장되며 size를 선언 시점에 지정해야 한다. 또한 메모리 할당도 선언가 동시에 Compile time에 할당되는데 이러한 것을 Static Memory Allocation 이라고 한다.
  또한 Random Access를 통해 인덱스 접근이 가능하고 삽입 삭제는 O(1) + 전체 배열 요소를 1씩 shift O(N) = O(N) 시간 걸린다.    
   
  LinkedList는 요소들이 정확히 어디에 저장되는지 알기 힘들며 size 또한 다양하다. 또한 메모리 할당은 새로운 노드가 추가될때 시행되며 Dynamic Memory Allocation 이라고 한다.
  Sequential Acess를 지원하며 순차적 접근이기 때문에 O(N) 시간이 걸린다. 그렇기 때문에 맨 앞과 뒤가 아니라면 삽입, 삭제에 O(N) 시간이 걸린다.  
  
- 결론   
  _데이터의 접근이 주 업무일 경우에는 Array를 사용하고 데이터의 수정이 주 업무라면 Linked List를 사용한다._
  

