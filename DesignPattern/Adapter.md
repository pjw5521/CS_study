## 어댑터 패턴 정의

- 호환성이 없는 기존 클래스의 인터페이스를 변환하여 사용자가 기대하는 인터페이스 형태로 변환시키는 패턴
- 코드의 재활용성을 증가하고 기존의 코드를 수정하지 않는 장점이 있음

## 어댑터 패턴 언제 사용?

- 외부 구성 요소를 기존 시스템에 재사용하고 싶지만 호환되지 않는 경우
- 애플리케이션이 클라이언트가 기대하는 인터페이스와 호환되지 않는 경우
- 원본 코드를 수정하지 않고 애플리케이션에서 레거시 코드를 재사용하려는 경우

## 어댑터 패턴 클래스 다이어그램

<img width="500" alt="classdiagram" src="https://user-images.githubusercontent.com/67946662/171198909-ac29af33-2805-440a-bf46-eb5aa676001b.png">


## 어댑터 패턴 활용 예제

![adapterexample](https://user-images.githubusercontent.com/67946662/171199097-13651912-73c7-4260-9d1a-48caaf198ad3.png)

```python
from abc import ABC, abstractmethod

class Fighter(ABC):
    @abstractmethod
    def attack(self): pass

    @abstractmethod
    def defend(self): pass

    @abstractmethod
    def escape(self): pass

class Warrior(Fighter):
    def attack(self):
        print('칼을 휘두르다')

    def defend(self):
        print('방패를 들어올니다')

    def escape(self):
        print('뒤로 물러난다')

class WizardAdapter(Fighter):
    def __init__(self, wizard):
        self.wizard = wizard

    def attack(self):
        self.wizard.shot_fire_ball()

    def defend(self):
        self.wizard.shield()

    def escape(self):
        self.wizard.portal()

class Wizard:
    def shot_fire_ball(self):
        print('파이어볼 발사')

    def shield(self):
        print('주변에 보호막 씌우기')

    def portal(self):
        print('포탈 열고 이동')

wizard = WizardAdapter(Wizard())
wizard.attack()
wizard.defend()
wizard.escape()
```

```python
# 출력
파이어볼 발사
주변에 보호막 씌우기
포탈 열고 이동
```
