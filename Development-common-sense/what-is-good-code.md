## 좋은 코드란 무엇인가 

#### 작성자 : [박지원](@pjw5521)

</br>

### 면접 질문 예시 
- 좋은 코드란 무엇인가? 그 이유는 ? 

</br>

## **1. 좋은 코드란 ?**
### **읽기 쉬운 코드?**

읽기 쉬운 코드를 작성하려면 각자에게 익숙한 언어를 사용하면 된다. 따라서 한국인이라면 한국어로 된 주석을 상세히 작성한다면 코드가 무엇을 하는지 빠르고 쉽게 파악할 수 있다. 

</br>

하지만, 주석은 관리하기 어렵다.
- 주석은 메타데이터이기 때문에 주석의 내용과 코드가 일치한다고 보장할 수 없으며, 수시로 변하는 요구사항으로 코드가 수정될 때 주석이 수정되지 않을 수도 있다. 오히려 혼란을 야기할 수도 있다. 
    
</br>

'읽기 쉽다'는 것은 개인마다 다르다.
- 사람마다 다른 배경지식을 가지고 있고, 기준이 다르다. 코드를 작성하는 시점에서 작성한 코드에 대한 이해가 100%이기 때문에 아무리 노력해도 한계가 존재할 수 밖에 없다. 

</br>

읽는다는 것은 코드를 이해하는 것까지 포함한다.
- 따라서, 읽기만 쉬우면 안되고 이해하기 쉬워야 한다. 

</br>

### **테스트가 용이한 코드?**

테스트 코드를 작성해두면 결함을 사전에 발견할 수 있기 때문에 좀 더 신뢰성있는 코드가 될 수 있다.

</br>
테스트가 용이한 코드 

- 테스트 가능한 코드는 쉽게 관찰할 수 있다.
- 테스트 가능한 코드는 쉽게 격리할 수 있다.  

</br>

### **중복이 없는 코드?**

동일한 로직을 수행하는 코드가 여기저기 존재한다면 불편하다. 왜냐하면, 동일한 코드 조각이 어디에 퍼져있는지 기억하기 쉽지 않기 때문에 한 곳만 수정한다면 다른 곳에서는 버그가 발생한다. 따라서 동일한 로직을 수행하는 코드는 별도의 함수로 빼두고 재사용하려고 한다. 

</br>
그 당시에는 동일한 로직을 수행하여 추출했지만, 지금은 다른 역할을 수행하게 될 수도 있다. 
- 목적이 다른 코드를 추출했을 때 다시 합치거나 수정하는 것은 비용이 들어가게 한다. 

</br>

## **2. 왜 좋지 않는 코드가 생산되는가?**
코드를 작성할 시점에 좋은 코드를 작성하기 위해 노력하는데, 이를 놓치는 시점이 존재하여 코드가 상하게 되는 것이다. 

마주할 수 있는 코드 생산, 수정 상황들 
- 이미 운영 중인 서비스의 cs 대응하며 수정하기
- 변경된 요구사항, 인터페이스 반영하기
- 어제 또는 방금 작성한 코드 수정하기
 
### **쓰이지 않는 코드(Dead code)**

코드 수정 과정에서 쓰이지 않게 된 코드가 있는데, 어디에서 쓰일지도 모른다는 불안감이 있다면 감히 삭제하지 못할 것이다. 
- 불안감 제거 ? 
    + 보고 있는 코드가 일정 범위에서만 사용된다는 확신이 있다면, 범위만 확인 후 사용하지 않는 코드라고 확신할 수 있다.
    + 함수 외부의 어떤 값을 기반으로 동작하는 함수는 수정하기 까다롭다.
    
</br>

### **응급처치를 한 코드**

중복된 로직으로 추출했지만 사용하는 곳에서 다른 로직을 추가해줘야 할 때 종종 발생한다. 이러한 응급처치가 몇 번 이루어지면 누구도 알아보기 어려운 코드가 발생한다. 
+ 응급처치가 무조건 나쁘진 않다. 당장 문제 해결을 하는데에 빠른 대응을 해야하기 때문이다. 하지만, 반드시 이러한 코드들은 해결 의무를 져야 한다. 

</br>

## **3. 좋지 않은 코드 줄이기**

좋은 코드란 **좋지 않은 코드가 없는 코드**를 말한다. 따라서 완벽한 코드를 작성하려고 노력하기 보다는 좋지 않은 코드를 줄이려고 노력해야 한다. 궁극적으로 점진적인 개선이 가능해야 한다. 

</br>

### **추출이 아닌, 추상화**
추출(extraction)
- 특별한 기준없이 단순히 밖으로 끌어내는 것 
추상화(abstraction)
- 어떤 대상의 중요한 요점들을 재해석하여 정리한 것 

의존성을 드러내기 위한 추상화
- 단순히 중복된 코드 덩어리에 대해 추출하면 재사용하기 어렵다. 
- 함수를 분리할 때 그 함수의 역할을 인지하고 하나의 역할만 하도록 정의해야 한다. 코드 조각 중 서로 의존 관계에 있는 것들을 추출(추상화)해야 한다. 
- 의존을 기반으로 분리된 여러 함수들을 각자의 역할을 수행하고 있기 때문에 새로운 요구 사항이 들어왔을 때 각자의 영역을 침범할 필요가 없어진다. 

</br>

### **삭제하기 쉬운 코드와 삭제하기 어려운 코드의 분리**
- 요구사항에 맞추다 보면 어쩔 수 없이 복잡한 코드가 작성된다. 
- 복잡한 요구 사항을 담고 있는 코드는 변경에 유연하지 못하기 때문에 별도로 분리해둬야 한다. 주석들과 함께 격리시켜 제대로 관리해야 한다.

</br>

### **일관성 있는 코드**

일관성은 합의된 규칙을 기반으로 만들어지며, 합의된 규칙은 개개인에게 모두 동일하다. 코드에 일관성이 지켜진다면 어느 곳에 어떤 코드가 위치하는지 예상할 수 있다. 
1) Naming 
- 예를 들어 함수의 네이밍에서 prefix + target + action 규칙을 지켜서 정의한다면 어떤 함수인지 예상이 가능하다. 

2) Directory 
- **어디에 분리할지**
- 일관된 디렉터리 구조는 전체적인 구조를 파악하는데 큰 도움이 되고 컴포넌트 간의 관계를 파악하는데 도움을 준다. 

</br>

### **확장성 있는 코드**
- 확장이 어려운 코드는 내부에서 많은 변경이 발생하여 코드를 읽기 어렵게 만든다. 
- 확장에 너무 많이 열려있으면 내부를 수정하기 어려워지는 문제도 발생할 수 있기 때문에, 적정선을 찾아가는 것이 중요하다. 

</br>

## 4. 결론
**what?**
- 좋은 코드란 좋지 않은 코드가 없는 코드를 말한다. 

**How?**
- 코드 간의 의존성을 고민하자.
- 합의된 규칙으로 일관성있게 작성하자.
- 적절하게 확장 가능하도록 설계하자.
- 어쩔 수 없는 코드는 주석과 함께 격리하자.

**Why?**
- 투입되는 비용 대비 결과물이 있어야 하는 영역이기 때문에 상황에 따라 코드를 관리해나가는 것이 중요하다. 
