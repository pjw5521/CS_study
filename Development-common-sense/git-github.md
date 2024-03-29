## Git과 GitHub에 대해서 

#### 작성자 : [박지원](@pjw5521)

</br>

### 면접 질문 예시 
- Git을 프로젝트에서 사용했다면 어떤 식으로 기여했는지 

</br>

### 1. **Git** 이란?
- VCS(Version Control System) 중 하나로 프로젝트 파일의 변경 사항을 추적하는 시스템이다.
- 개발자들은 Git을 통해 변경 사항을 기록하고, 특정 시점의 버전으로 언제든 돌아갈 수 있다. 
- 오픈 소스에 기여하거나 공동 작업을 하기 위해 꼭 필요하다.
- 기본적으로 파일 시스템의 스낸샵을 저장하고 이를 해시하여 빠르게 바뀐 버전인지 아닌지 체크한다. 

#### **Repository** 
- 프로젝트 저장소 
- Local Repository : 자신의 컴퓨터에 저장된 로컬 버전의 프로젝트 저장소 
- Remote Repository : 내 컴퓨터가 아닌 외부 버전의 프로젝트 저장소로서, 협업 시 많이 사용하며 프로젝트 코드를 공유할 수 있다. 로컬 버전의 프로젝트와 병합할 수 있고, 변경 사항을 적용할 수 있는 곳이다. 

#### **Commit** 
- 프로젝트의 현재 상태를 나타내는 스냅샷
- 현재 버전의 코드를 커밋에 저장한다. 따라서 커밋 앞뒤로 이동하여 프로젝트 코드의 다른 변경 사항을 확인할 수 있다. 

#### **Branch**
- 독립적으로 어떤 작업을 진행하기 위한 개념으로, 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에 여러 작업을 동시에 진행할 수 있다. 
- 팀 안에서 동시 작업할 때, 메인 브랜치에서 자신의 작업 전용 브랜치를 만들고 각자 작업이 마무리 되면 변경 사항을 메인 브랜치에 적용한다. 
- 보통 현업에서는 development 브랜치를 만들고, 여기에 병합한다. 최종적으로 배포 단계에서는 
master 브랜치에 병합한다. 

</br>

### 2. GitHub란?
- Git repository를 위한 호스팅 플랫폼 
- GitHub 없이도 Git을 사용할 수 있지만 다른 개발자와 협업하거나 내 코드를 공유하기는 어렵다. 

#### **Pull Request(PR)** 
- 자신이 작업한 브랜치 작업 내용을 master 브랜치에 반영해달라는 요청
- 병합되기에 아무런 문제가 없다면 Merge 권한이 있는 개발자가 병합을 진행 

#### **Conflicts**
- 어떤 파일의 변경 사항이 기준이 되는 master 브랜치의 파일과 겹쳐, Git에서 어떤 버전의 코드를 선택해야 할지 모를 때 발생
- 개발자가 직접 코드를 비교해 이를 해결하고, Merge 해야 한다. 

#### **Git Rebase**
- 일련의 커밋들을 새로운 베이스 커밋으로 옮기거나 합치는 과정 
- base가 옮겨지니 commmit도 변경되어 새로운 base 기준으로 정렬 
- merge & rebase : 두 명령 모두 한 브랜치에서 다른 브랜치로 변경 사항들을 통합하기 위해 디자인 되었다. 

</br>

### 3. **Git Flow**
- Vincent Drissen이 시작한 Git 사용 방법론 
- 5가지의 브랜치를 사용 
    + master: 기준이 되는 브랜치로 제품을 배포하는 브랜치
    + develop: 개발 브랜치로 개발자들이 이 브랜치를 기준으로 각자 작업한 기능들을 병합(merge)
    + feature: 단위 기능을 개발하는 브랜치로 기능 개발이 완료되면 develop 브랜치에 합친다.
    + release: 배포를 위해 master 브랜치로 보내기 전에 먼저 QA(Quality Assurance, 품질 검사)를 하기위한 브랜치
    + hotfix: master 브랜치로 배포를 했는데 버그가 생겼을 때 긴급 수정하는 브랜치