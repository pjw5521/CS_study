## SOLID

#### 작성자 : [박지원](@pjw5521)

### SOLID 란 ?
- 5가지 Software design principles

1. Single Responsibility Principle(SRP)
- 클래스는 오직 하나의 이유로 수정이 되어야 한다. 

2. Open Closed Principle(OCP)
- 자신의 확장에는 열려있고 주변의 변화에는 닫혀 있어야 한다. 

3. Liskov Substitution Principle(LSP)
- 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.

4. Interface Segregation Principle(ISP)
- 사용하지 않는 메소드에 의존하면 안된다. 

5. Dependency Inversion Principle(DIP)
- 자신(high level module)보다 변하기 쉬운 모듈(low level modeul)에 의존해서는 안된다.

### Design Smells 
- 나쁜 디자인을 나타내는 증상 
- 스파게티 코드를 의미 

1. Rigidity(경직성)
- 시스템을 변경하기 어려움을 의미 
- 즉, 하나의 변경을 위해 다른 것들까지 변경해야할 때 경직성이 높다
- 관리자는 개발자에게 수정 요청을 하기 어려워짐 

2. Fragility(취약성)
- 어떤 부분을 수정하였는데 관련이 없는 다른 부분에 영향을 줌을 의미 
- 관리 비용이 커지며 시스템의 신뢰도가 떨어짐 

3. Immobility(부동성)
- 재사용하기 위해 시스템을 분리해서 컴포넌트를 만드는 것이 어려움을 의미 

4. Viscosity(점착성)
- 개발 환경에 지나친 의존성을 가짐을 의미 
- 디자인 점착성 
    - 설계를 유지한 상태에서 변경하기 쉽도록 설계할 때 
- 환경 점착성 
    - 개발 환경이 느리고 효율적이지 못할 때 
    
</br>

#### 그외 

+ Needless Complexity (불필요한 복잡성)
    - 당장 필요하지 않은 코드 구조가 존재하는 상황 
    - 언젠가는 유용할지도 모르는 코드도 포함된 상황 

+ Needless Repetition (불필요한 반복)
    - 복사 붙여넣기로 생성된 코드들이 혼재하는 상황 
    
+ Opacity (불투명성)
    - 혼란스러운 표현, 읽고 이해하기 힘든 상황 