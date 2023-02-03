**단위 테스트란?**

컴퓨터 프로그래밍에서 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차이다.
즉, 모든 함수와 메소드에 대한 테스트 케이스를 작성하는 절차를 말한다.

---

# 💡 TDD 법칙 세 가지

### 1️⃣첫째 법칙 
: 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.

### 2️⃣둘째 법칙
: 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.

### 3️⃣셋째 법칙
: 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

→ 실제 코드를 사실상 전부 테스트하는 테스트 케이스가 나온다.
    실제 코드와 맞먹을 정도로 방대한 테스트 코드는 심각한 관리 문제를 
    유발하기도 한다.

---

# 💡 깨끗한 테스트 코드 유지하기

> 🔥 테스트 코드는 실제 코드 못지 않게 중요하다.
테스트 코드가 지저분할수록 변경하기 어려워진다.


### 테스트는 유연성, 유지보수성, 재사용성을 제공한다.

테스트 코드를 깨끗하게 유지하지 않으면 결국은 잃어버린다. 테스트 케이스가 없으면 실제 코드를 유연하게 만드는 버팀목도 사라진다.

**코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목이 바로 단위 테스트**다.

→ 테스트 케이스가 있으면 변경이 두렵지 않으니까!

- 테스트 케이스가 없다면
    
    모든 변경이 잠정적인 버그이다.
    아키텍처가 아무리 유연하더라도, 설계를 아무리 잘 나눴더라도, 테스트 케이스가 없으면 개발자는 변경을 주저한다. → 버그가 숨어들까 두려워서
    
- 테스트 케이스가 있다면
    
    테스트 커버리지가 높을수록 공포는 줄어든다.
    아키텍처가 부실한 코드나 설계가 모호하고 엉망인 코드라도 별다른 우려 없이 변경할 수 있다.
    오히려 안심하고 아키텍처와 설계를 개선할 수 있다.
    

실제 코드를 점검하는 자동화된 단위 테스트 슈트는 설계와 아키텍처를 최대한 깨끗하게 보존하는 열쇠다.

- 테스트는 유연성, 유지보수성, 재사용성을 제공한다.
- 테스트 케이스가 있으면 변경이 쉬워지기 때문이다.

따라서 테스트 코드가 지저분하면 코드를 변경하는 능력이 떠러지며 코드 구조를 개선하는 능력도 떨어진다.
테스트 코드가 지저분할수록 실제 코드도 지저분해진다.

결국 테스트 코드를 잃어버리고 실제 코드도 망가진다.

---

# 💡 깨끗한 테스트 코드

> 🔥 깨끗한 테스트 코드를 만들려면 필요한 세 가지?<br>
가독성, 가독성, 가독성..<br>
가독성을 높이려면?<br>
명료성, 단순성, 풍부한 표현력


- 리팩터링한 코드
    
    ```java
    public void testGetPageHierarchyAsXml() throws Exception {
      makePages("PageOne", "PageOne.ChildOne", "PageTwo");
    
      submitRequest("root", "type:pages");
    
      assertResponseIsXML();
      assertResponseContains(
        "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>");
    }
    
    public void testSymbolicLinksAreNotInXmlPageHierarchy() throws Exception {
      WikiPage page = makePage("PageOne");
      makePages("PageOne.ChildOne", "PageTwo");
    
      addLinkTo(page, "PageTwo", "SymPage");
    
      submitRequest("root", "type:pages");
    
      assertResponseIsXML();
      assertResponseContains(
        "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>");
      assertResponseDoesNotContain("SymPage");
    }
    
    public void testGetDataAsXml() throws Exception {
      makePageWithContent("TestPageOne", "test page");
    
      submitRequest("TestPageOne", "type:data");
    
      assertResponseIsXML();
      assertResponseContains("test page", "<Test");
    }
    ```
    
    각 테스트는 명확히 세 부분을 나눠진다.
    
    첫 부분은 테스트 자료를 만든다.
    
    두 번째 부분은 테스트 자료를 조작한다.
    
    세 번째 부분은 조작한 결과가 올바른지 확인한다.
    
    → 잡다하고 세세한 코드를 거의 없앴다는 사실에 주목한다.
    
    → 코드를 읽는 사람은 헷갈릴 필요 없이 코드가 수행하는 기능을 재빨리 이해한다.
    

### 도메인에 특화된 테스트 언어 (DSL)

흔히 쓰는 시스템 조작 API를 사용하는 대신 API 위에다 함수와 유틸리티를 구현한 후 그 함수와 유틸리티를 사용하므로 테스트 코드를 짜기도 읽기도 쉬워진다.

이렇게 구현한 함수와 유틸리티는 테스트 코드에서 사용하는 특수 API가 된다.
즉, 테스트를 구현하는 당사자와 나중에 테스트를 읽어볼 독자를 도와주는 테스트 언어이다.

숙련된 개발자라면 자기 **코드를 좀 더 간결하고 표현력이 풍부한 코드로 리팩터링**해야 마땅하다.

### 이중 표준

테스트 API 코드에 적용하는 표준은 실제 코드에 적용하는 표준과 확실히 다르다.

단순하고, 간결하고, 표현력이 풍부해야 하지만, 실제 코드만큼 효율적일 필요는 없다. → 테스트니까!

```java
@Test
public void turnOnCoolerAndBlowerIfTooHot() throws Exception {
  tooHot();
  assertEquals("hBChl", hw.getState()); 
}
  
@Test
public void turnOnHeaterAndBlowerIfTooCold() throws Exception {
  tooCold();
  assertEquals("HBchl", hw.getState()); 
}

@Test
public void turnOnHiTempAlarmAtThreshold() throws Exception {
  wayTooHot();
  assertEquals("hBCHl", hw.getState()); 
}

@Test
public void turnOnLoTempAlarmAtThreshold() throws Exception {
  wayTooCold();
  assertEquals("HBchL", hw.getState()); 
}
//테스트 코드를 이해하기 쉽다는 사실이 분명히 드러난다.
```

```java
public String getState() {
  String state = "";
  state += heater ? "H" : "h"; 
  state += blower ? "B" : "b"; 
  state += cooler ? "C" : "c"; 
  state += hiTempAlarm ? "H" : "h"; 
  state += loTempAlarm ? "L" : "l"; 
  return state;
}
//코드가 효율적이지 못하다.
//StringBuffer가 적합하다.

//하지만 StringBuffer는 보기에 흉하다.
//StringBuffer를 안 써서 치르는 대가가 미미하다.
//실제 환경에서는 문제가 될 수 있지만 테스트 환경은 자원이 제한적일
//가능성이 낮기 때문이다.
```

이것이 이중 표준의 본질이다.

실제 환경에서는 절대로 안 되지만 테스트 환경에서는 전혀 문제없는 방식이 있다. 대개 메모리나 CPU 효율과 관련 있는 경우다. 코드의 깨끗함과는 철저히 무관하다.

---

# 💡 테스트 당 assert 하나

### 테스트 당 개념 하나

> 🔥 테스트 함수마다 한 개념만 테스트하라

한 함수로 개념들을 몰아넣으면 독자가 각 절이 거기에 존재하는 이유와 각 절이 테스트하는 개념을 모두 이해해야 한다.

assert문이 여럿이라는 사실이 문제가 아니다.

한 테스트 함수에서 여러 개념을 테스트한다는 사실이 문제다.

그러무로 가장 좋은 규칙은 “개념 당 assert 문 수를 최소로 줄여라” 와 “테스트 함수 하나는 개념 하나만 테스트하라”라 하겠다.

---

# 💡 F.I.R.S.T

### Fast - 빠르게

: 테스트는 빨리 돌아야 한다. 테스트가 느리면 자주 돌릴 엄두를 못 낸다. 
자주 돌리지 않으면 초반에 문제를 찾아내 고치지 못한다. 
코드를 마음껏 정리하지도 못한다. 
결국 코드 품질이 망가지기 시작한다.

### Independent - 독립적으로

: 각 테스트는 서로 의존하면 안 된다.
각 테스트는 독립적으로 그리고 어떤 순서도 실행해도 괜찮아야 한다.
테스트가 서로에게 의존하면 하나가 실패할 때 나머지도 잇달아 실패하므로 원인을 진단하기 어려워지며 후반 테스트가 찾아내야 할 결함이 숨겨진다.

### Repeatable - 반복가능하게

: 테스트는 어떤 환경에서도 반복 가능해야 한다.
실제 환경, QA 환경, 네트우크 연결이 되지 않은 노트북 환경에서도 실행할 수 있어야 한다.
테스트가 돌아가지 않는 환경이 하나라도 있다면 테스트가 실패한 이유를 둘러댈 변명이 생긴다.
게다가 환경이 지원되지 않기에 테스트를 수행하지 못하는 상황에 직면한다.

### Self-Validating - 자가검증하는

: 테스트는 부울 값으로 결과를 내야 한다. 성공 아니면 실패다.
통과 여부를 알려고 로그 파일을 읽게 만들어서는 안 된다.
통과 여부를 보려고 텍스트 파일 두 개를 수작업으로 비교하게 만들어서도 안 된다.
테스트가 스스로 성공과 실패를 가늠하지 않는다면 판단은 주관적이 되며 지루한 수작업 평가가 필요하게 된다.

### Timely - 적시에

: 테스트는 적시에 작성해야 한다.
단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다.
실제 코드를 구현한 다음에 테스트 코드를 만들면 실제 코드가 테스트하기 어렵다는 사실을 발견할지도 모른다.
어떤 실제 코드는 테스트하기 너무 어렵다고 판명날지 모른다.
테스트가 불가능하도록 실제 코드를 설계할지도 모른다.

---

# 결론

테스트 코드는 실제 코드만큼이나 프로젝트 건강에 중요하다.

테스트 코드는 실제 코드의 유연성, 유지보수성, 재사용성을 보존하고 강화하기 때문이다.

테스트 코드는 지속적으로 깨끗하게 관리하자.

표현력을 높이고 간결하게 정리하자.

테스트 API를 구현해 도메인 특화 언어를 만들자

→ 그러면 그만큼 테스트 코드를 짜기가 쉬워진다.

테스트 코드가 방치되어 망가지면 실제 코드도 망가진다.
