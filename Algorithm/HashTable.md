## 해시 테이블 (Hash Table)

#### 작성자 : [박지원](@pjw5521)

### 해시 테이블 
- (key, value)로 데이터를 저장하는 자료구조 
- key를 통해 데이터를 검색하므로, 완전 탐색 시 시간초과가 발생할 때 고려할 수 있음 
- 파이썬에서는 딕셔너리(Dictionary)를 사용하면 되므로 별도로 구현할 필요가 없음 
```python
dic = {}
dic['coin'] = 500
print(dic['coin']) # 500
```

### 시간복잡도
- Collision이 없는 일반적인 경우 : O(1)
- 최악의 경우 : O(n)

### reference
- 충돌과 관련된 구체적인 내용은 [HashTable](DataStructure/HashTable.md) 참고