> 🔥 오류 처리는 중요하다. 하지만 오류 처리 코드로 인해 프로그램 논리를 이해하기 어려워진다면 클린코드라 부르기 어렵다.


# 💡 오류 코드보다 예외를 사용하라

오류가 발생하면 예외를 던지는 편이 낫다. 
그러면 **호출자 코드가 더 깔끔해진다.** 
논리가 오류 처리 코드와 뒤섞이지 않기 때문이다.

---

# 💡 Try-Catch-Finally 문부터 작성하라

**`try` 블록**은 **transaction**과 비슷하다. `**try**` 블록에서 무슨 일이 생기든지 `**catch**` 블록은 프로그램 상태를 일관성 있게 유지해야 한다.
→ 그러므로 예외가 발생할 코드를 짤 때는 `**try-catch-finally**` 문으로 시작하는 편이 낫다.

**`try`** 블록에서 무슨 일이 생기든지 호출자가 기대하는 상태를 정의하기 쉬워진다.

---

# 💡 미확인 예외를 사용하라

- 확인된 예외 : 컴파일 단계에서 확인되며 반드시 처리해야 하는 예외
    - IOException
    - SQLException
- 미확인 예외 : 실행 단계에서 확인되며 명시적인 처리를 강제하지 않는 예외
    - NullPointerException
    - IllegalArgumentException
    - IndexOutOfBoundException
    - SystemException

현재는 안정적인 소프트웨어를 제작하는 요소로 확인된 예외가 반드시 필요하지는 않다는 사실이 분명해졌다. 그러므로 우리는 확인된 오류가 치르는 비용에 상응하는 이익을 제공하는지 따져봐야 한다.

비용? 확인된 예외는 OCP . Open Closed Principle 를 위반한다.
(하위 단계에서 코드를 변경하면 상위 단계 메서드 선언부를 전부 고쳐야 한다는 말)

때로는 확인된 예외도 유용하다. 아주 중요한 라이브러리를 작성한다면 모든 예외를 잡아야 한다. 하지만 일반적인 애플리케이션은 의존성이라는 비용이 이익보다 크다.

---

# 💡 예외에 의미를 제공하라

예외가 발생한다면 구체적인 정보를 제공하면 오류의 발생 원인과 위치를 찾기 쉬워진다.

- 오류 메시지에 정보를 담는다.
- 실패한 연산 이름, 실패 유형 언급한다.


---

# 💡 호출자를 고려해 예외 클래스를 정의하라

오류를 정의할 때 프로그래머에게 가장 중요한 관심사는 오류를 잡아내는 방법이 되어야 한다.

흔히 예외 클래스 하나만 있어도 충분한 코드가 많다. 예외 클래스에 포함된 정보로 오류를 구분해도 괜찮은 경우가 그렇다. 

한 예외는 잡아내고 다른 예외는 무시해도 괜찮은 경우라면 여러 예외 클래스를 사용하라.

### ✨ 감싸기 Wrapper

실제로 외부 API를 사용할 때는 감싸기 기법이 최선이다. 외부 API를 감싸면 외부 라이브러리와 프로그램 사이에서 의존성이 크게 줄어든다. 

다른 라이브러리로 갈아타도 비용이 적다. 

외부 API를 호출하는 대신 테스트 코드를 넣어주는 방법으로 프로그램을 테스트하기도 쉬워진다.

특정 업체가 API를 설계한 방식에서 발목 잡히지 않는다. 프로그램이 사용하기 편리한 API를 정의하면 그만이다.

---

# 💡 정상 흐름을 정의하라

### ✨ 특수 사례 패턴 Special Case Pattern

: 클래스를 만들거나 객체를 조작해 특수 사례를 처리하는 방식이다.
  클라이언트 코드가 예외적인 상황을 처리할 필요가 없어진다.
  클래스나 객체가 예외적인 상황을 캡슐화해서 처리한다.

---

# 💡 `null`을 반환하지 마라

오류를 유발하는 흔한 행위 → null을 반환하는 습관

null을 반환하는 코드는 일거리를 늘릴 뿐만 아니라 호출자에게 문제를 떠넘긴다. → null 확인을 빼먹는다면 통제 불능이 될지도..

null을 반환하고 싶다면 → **예외를 던지거나 특수 사례 객체를 반환한다.**

---

# 💡 `null`을 전달하지 마라

메서드에서 null 반환보다 메서드로 null을 전달하는 방식이 더 나쁘다.

정상적인 인수로 null을 기대하는 API가 아니라면 메서드로 null을 전달하는 코드는 최대한 피한다.

호출자가 실수로 넘기는 null을 적절히 처리하는 방법이 없다.

인수로 null이 넘어오면 코드에 문제가 있다. 애초에 null을 넘기지 못하도록 금지하는 정책이 합리적이다. 이런 정책을 따르면 실수할 확률도 줄어든다.

---

# 결론

깨끗한 코드는 읽기도 좋아야 하지만 안정성도 높아야 한다.

오류 처리를 프로그램 논리와 분리해 독자적인 사안으로 고려하면 튼튼하고 깨끗한 코드를 작성할 수 있다.

오류 처리를 프로그램 논리와 분리하면 독립적인 추론이 가능해지며 코드 유지보수성도 높아진다.
