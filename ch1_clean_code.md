# 코드가 존재하리라
앞으로 코드가 사라질 가망은 전혀 없다.
코드는 요구 사항을 상세하게 표현하는 수단이니까!
추상화 수준이 점차 높아질 거라고 예상하니까!
코드의 도움 없이 요구 사항을 상세하게 표현하는 것은 불가능.
추상화도 불가능.
기계가 실행할 정도로 상세하게 요구 사항을 명시하는 작업이 바로 ‘프로그래밍’ → 고로 코드는 항상 존재한다.

---

# ✨ 나쁜 코드
나쁜 코드 → 고행 wading
우리는 대충 짠 프로그램이 돌아간다는 사실에 안도감을 느끼며 그래도 안 돌아가는 프로그램보다 돌아가는 쓰레기가 좋다고 스스로를 위로한다.
다시 돌아와 나중에 정리하겠다고 다짐한다.
→ 르블랑의 법칙(나중은 결코 오지 않는다.)

# ✨ 나쁜 코드로 치르는 대가
나쁜 코드가 쌓일수록 시간 대 생산성 (시간이 갈수록 생산성은 떨어진다)
→ 시간이 지나면서 쓰레기 더미가 높아지고 깊어지며 이에 따라 생산성은 떨어지며 0에 근접한다.

### 1️⃣ 원대한 재설계의 꿈
시간을 들여 깨끗한 코드를 만드는 노력이 비용을 절감하는 방법일 뿐만 아니라 전문가로서 살아남는 길이다.

### 2️⃣ 태도
프로그래머는 나쁜 코드의 위험을 이해하지 못하는 관리자의 말을 그대로 따르는 행동은 전문가답지 못하다.
좋은 코드를 사수하는 일은 프로그래머들의 책임이다.

### 3️⃣ 원초적 난제
나쁜 코드를 양산하면 기한을 맞추지 못한다.
오히려 엉망진창인 상태로 인해 속도가 곧바로 늦어지고, 결국 기한을 놓친다.
기한을 맞추는 유일한 방법은, 빨리 가는 유일한 방법은, 언제나 코드를 최대한 깨끗하게 유지하는 습관이다.

---

# ✨ 깨끗한 코드란?

### 👨‍💻 그래디 부치
깨끗한 코드는 잘 쓴 문장처럼 읽혀야 한다.
코드는 추측이 아니라 사실에 기반으로 하며 반드시 필요한 내용만 담아야 한다.

### 👨‍💻 워드 커닝햄
짐작했던 기능을 그대로 수행한다면 깨끗한 코드이다.
읽으면서 짐작한 내용으로 돌아가는 코드가 깨끗한 코드이다.

# ✨ 보이스카우트 규칙
캠프장은 처음 왔을 때보다 더 깨끗하게 해 놓고 떠나라!

변수 이름 하나를 개선하고 조금 긴 함수 하나를 분할하고 약간의 중복을 제거하고 복잡한 if문 하나를 정리하면 충분하다.

# ✨ 프리퀄과 원칙

* SRP Single Responsibility Principle : 클래스에는 한 가지, 단 한 가지 변경 이유만 존재해야 한다.
* OCP Open Closed Principle : 클래스는 확장에 열려 있어야 하며 변경에 닫혀 있어야 한다.
* DIP Dependency Inversion Principle : 추상화에 의존해야 하며, 구체화에 의존하면 안 된다.
* LSP The Liskov Substitution Principle : 상속 받는 클래스는 기초 클래스를 대체할 수 있어야 한다.
* ISP The Interface Segregation Principle : 클라이언트에 밀접하게 작게 쪼개진 인터페이스를 유지한다.

---
