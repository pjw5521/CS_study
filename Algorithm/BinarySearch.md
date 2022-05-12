## 이분 탐색 (Binary Search)

#### 작성자 : [박지원](@pjw5521)

</br>

## **이분 탐색**
- 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교하는 알고리즘
- 배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있음 

### 순차 탐색
- 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인하는 알고리즘

### 사용하는 이유 
- 순차 탐색보다 훨씬 빠르기 때문에 탐색 범위가 큰 상황에서 사용할 수 있음
- 순차 탐색 : O(N)
- 이분 탐색 : O(logN)

</br>

## 알고리즘
1. **정렬**
2. left와 right의 중간값인 mid 설정
3. mid 값과 내가 구하고자 하는 값 비교
4. 구할 값이 mid 보다 높으면 left = mid + 1 로 설정, mid 보다 낮으면 right = mid -1 로 설정 

위 과정을 left <= right 인 동안 반복

</br>

## 소스 코드
- 재귀 함수로 구현한 이진 탐색 소스코드 
    ```python
    def binary_search(array, target, start ,end):
        if start > end:
            return None
        mid = ( start + end ) // 2 
        if array[mid] == target:
            return mid 
        elif array[mid] < target:
            return binary_search(array, target, mid+1, end)
        else:
            return binary_search(array, target, start, mid-1)
    ```
- 반복문으로 구현한 이진 탐색 소스코드 
    ```python
    def binary_search(array, target, start ,end):
        while start <= end:
            mid = (start + end) // 2
            if array[mid] == target:
                return mid 
            elif array[mid] < target:
                start = mid + 1 
            else: 
                end = mid - 1 
        return None
    ```