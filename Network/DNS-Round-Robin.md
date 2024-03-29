## DNS Round Robin 

#### 작성자 : [박지원](@pjw5521)

</br>

### 면접 질문 예시 
- 로드 밸런싱에 대한 설명 
- 로드 밸런싱 알고리즘에 대해 설명 
- DNS에 대한 설명  

</br>

### 1. 로드 밸런싱(Load Balancing) 이란 ? 
- 서버에 가해지는 부하를 분산해주는 장치 또는 기술 
- 사업의 규모가 확장되고 클라이언트의 수가 늘어나면 기존 서버만으로는 정상적인 서비스 불가능 
    + Scale up : 서버 자체의 성능을 높이는 것
    + Scale out : 여러 대의 서버를 두는 것, 여러 대의 서버로 트래픽을 균등하게 분산해주는 로드밸런싱이 반드시 필요 
    
### 2. **DNS(Domain Name System)** 란 ?
- 호스트의 도메인 이름을 호스트의 네트워크 주소로 바꾸거나 그 반대의 변환을 수행하는 시스템 
- 사이트는 IP 주소를 통해 접속해야하는데, 이 때 DNS server는 웹 서버 주소에 해당하는 IP 주소 테이블 가지고 있는 서버로서 url이 가리키는 IP 주소를 브라우저에게 반환 

</br>

### 3. DNS Round Robin 이란 ?
- DNS 서버 구성 방식 중 하나로, 도메인에 대한 IP 요청 시 round robin 방식으로 IP를 반환 
- 별도의 로드밸런싱 장비를 사용하지 않고 DNS만 이용해서 트래픽 분산 기법 
- round robin 
    + 선점형 스케줄링의 하나로서, 시간 단위로 CPU를 할당하는 스케줄링 방식  
- 예시
    + 웹 서비스를 담당할 웹 서버는 자신의 공인 IP를 각각 가지고 있는데, 웹 사이트에 접속을 원하는 유저가 도메인 주소를 브라우저에 입력하면 DNS는 도메인의 IP 정보를 조회한다. 이 때 IP 주소를 여러 대의 서버 IP 리스트 중에서 round robin 방식으로 랜덤하게 하나 또는 여러개를 선택하여 사용자에게 알려준다. 따라서 다수의 사용자는 실제로 여러 개의 웹 서버에 나뉘어 접속하게 되어 서버의 부하가 자연스럽게 분산된다. 
- 조회 결과로 1개의 IP만 조회되는 경우도 있지만 최근은 복수의 IP를 모두 제공하고 클라이언트가 선택하도록 한다. 

</br>

### 4. 문제점 
**서버의 수만큼 공인 IP 주소가 필요하다.**
- 부하 분산을 위해 여러 개의 웹 서버를 만드는데, 그 만큼의 공인 IP가 필요하다.

**균등하게 분산되지 않는다.**
- 캐싱으로 인해 균등하게 부하분산되지 않는다.
- 스마트폰으로 접속할 경우 : 캐리어 게이트웨이라고 하는 프록시 서버 경유하여 도메인 이름 변환 결과가 일정 시간동안 캐싱된다. 따라서 프록시 서버를 경유하는 접속은 항상 같은 서버로 접속된다.
- PC용 웹 브라우저로 접속할 경우 : 질의 결과 캐싱하기 때문에 균등하게 부하 분산되지 않는다.
- TTL (Time To Live) 시간을 짧게 설정함으로써 어느 정도 해소 가능하다. 

**서버가 다운되도 확인이 불가능하다.**
- DNS 서버는 웹 서버의 부하나 접속 수 등의 상황에 따라 질의결과 제어가 불가능하다.
- 어떤 원인으로 다운되더라도 이를 검출하지 못하고 유저들에게 제공된다. 따라서 간혹 다운된 서버로 연결될 수 있다. 

</br>

### 5. 해결 방법 
**가중치 편성 방식(Weighted Round Robin, WRR)**
- 각 웹 서버에 가중치를 부여해서 분산 비유을 변경하는 방식
- 가중치가 큰 서버일수록 빈번하게 선택되므로 처리 능력이 높은 서버는 가중치를 높게 설정하는 것이 좋다.

**최소 연결(Least connection)**
- 접속 클라이언트가 가장 적은 서버를 선택하는 방식 
- 로드 밸런서에서 실시간으로 접속자 수를 관리하거나 각 서버에서 주기적으로 알려주는 것이 필요하다.

</br>

### 6. L4 로드 밸런싱 
- transport 계층에서 로드를 분산 
- 데이터 안을 보지 않고, 패킷 레벨에서만 부하를 분산시키기 때문에 속도가 빠르고 효율이 높다. 
- 섬세한 라우팅이 불가능하지만 L7 로드 밸런서보다 저렴

</br>

### 7. L7 로드 밸런싱 
- application 계측에서 로드를 분산
- 사용자의 요청을 기준으로 특정 서버에 부하를 분산시키는 것이 가능하다. 즉, 패킷의 내용을 확인하고 그 내용에 따라 부하를 특정 서버에 분배하는 것이 가능
- 섬세한 라우팅이 가능하고, 비정상적인 트래픽을 필터링할 수 있다.
- 패킷의 내용을 복호화 해야하기 때문에 더 많은 비용이 든다. 

#### 프록시 서버 (Proxy Server)
- 시스템에 방화벽을 가지고 있는 경우 외부와의 통신을 위해 만들어 놓은 서버로서, 클라이언트가 프록시 서버를 통해 다른 네트워크에 간접적으로 접속할 수 있게 함 
- WHY ?
    + 보안 상의 이유로 직접 통신할 수 없을 경우 사용
    + 내부 네트워크 IP 주소에 액세스할 권한이 없는 외부 사용자 차단
    + 컴퓨터 네트워크가 외부 사용자에게 보이지 않게 함 
- **프록시 서버에 요청된 내용들을 캐시를 이용하여 저장**
    + 전송 시간 절약
    + 불필요하게 외부와의 연결을 하지 않아도 됨
    + 네트워크 병목 현상 방지 가능 
    
### 방화벽 
- 무단 액세스로부터 컴퓨터 네트워크를 보호하는데 사용되는 네트워크 보안 시스템 
- 외부에서 컴퓨터 네트워크의 악의적인 접근을 방지할 수 있다.