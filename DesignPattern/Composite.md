## 컴포지트 패턴 (Composite Pattern)

#### 작성자 : [박지원](@pjw5521)

### 컴포지트 패턴이란 ?
- 여러 개의 객체들로 구성된 복합 객체와 단일 객체를 클라이언트에서 구별 없이 다루게 해주는 패턴 
- 전체의 계층을 하나의 인터페이스로 통합해서 트리 구조로 구성하는 구조 패턴 중 하나 
- 개별 객체와 복합 객체 모두를 표현할 수 있는 하나의 추상화 클래스를 정의해야 함 
![composite](https://github.com/gyoogle/tech-interview-for-developer/raw/master/resources/composite_pattern_1.PNG)
- leaf 클래스와 composite 클래스를 같은 인터페이스로 제어하기 위해서 componet abstract 클래스 생성 
- 장점 : leaf 클래스와 composite 클래스를 구분할 필요 없이 component 클래스로 생각할 수 있다.
- 단점 : leaf 클래스가 chlid 관리 함수 호출 시 exception 발생  

### 예제
- https://gyoogle.dev/blog/design-pattern/Composite%20Pattern.html 