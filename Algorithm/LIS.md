## LIS (최장 증가 수열)

#### 작성자 : [박지원](@pjw5521)

### 대표문제 
백준 11053 [가장 긴 증가하는 부분 수열](https://www.acmicpc.net/problem/1260)
백준 12015 [가장 긴 증가하는 부분 수열2](https://www.acmicpc.net/problem/12015)

### 최장 증가 수열(LIS, Longest Increasing Subsequence)
- 원소가 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, 긱 원소가 이전 원소보다 크다는 조건을 만족하고 그 길이가 최대인 부분 수열

### 알고리즘
1. DP로 풀이
- 시간 복잡도 : O(N^2)
1. 주어진 배열에서 인덱스 i를 한 칸씩 늘려가면서 확인
2. 내부 반복문에서 i보다 작은 인덱스들을 살펴보며 data[j]< data[i]인 것이 있는지 확인 
3. 있다면 dp[i] 업데이트 
    - 기존의 dp[i] 값과 dp[j]에서 마지막에 i를 추가했을 때의 길이 중 더 큰 값
```python
for i in range(n):
# 본인의 왼쪽 숫자들 비교 
    for j in range(i):
    # 이전의 원소가 작은지 확인하여, 작다면 dp 최댓값 구해 +1 
        if data[j] < data[i]:
            dp[i] = max(dp[i],dp[j]+1)
```

2. Lower Bound
- O(N^2)로 해결할 수 없는 문제라면 Lower Bound로 풀이
- 시간 복잡도 : O(NlogN)
- 이진 탐색을 사용하여 LIS 를 구하는 알고리즘
- 원하는 값 k 이상이 처음 나오는 위치를 찾는 과정 
```python
# num과 같거나 큰 가장 작은 인덱스 구하기 
def binary_search(arr, num):
    start = 0 
    end = len(arr) -1 
    
    while start <= end :
        mid = (start+end) // 2
        
        if arr[mid] >= num :
            end = mid -1 
        else:
            start = mid + 1 
    
    return start 
```