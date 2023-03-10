
## `SerialDate` : 날짜를 표현하는 자바 클래스

# 💡 첫째, 돌려보자

클래스를 철저히 이해하고 리팩터링하려면 훨씬 높은 테스트 커버리지가 필요하다.

---

# 💡 둘째, 고쳐보자

### ✨ 주석

법적인 정보는 필요하므로 라이선스 정보와 저작권은 보존한다.

소스 코드 제어 도구를 사용하므로 변경 이력은 없애도 괜찮다.

### ✨ import 문

java.text.* 와 java.util.*로 줄여도 된다.

### ✨ Javadoc 주석

여러 언어를 사용하면 제대로 모양새를 맞추기 어렵다.

주석 전부를 `<pre>` 로 감싸면 형식이 그대로 유지된다.

### ✨ 서술적인 용어

일련번호라는 용어는 날짜보다 제품 식별 번호로 더 적합하다.

### ✨ enum으로 변경

### ✨ 특정 버전에서 직렬화한 클래스를 다른 버전에서 복원하지 않는 편이 안전하다.

### ✨ 클래스

추상 클래스는 구체적인 구현 정보를 포함할 필요가 없다.

기반 클래스는 파생 클래스를 몰라야 바람직하다.

ABSTRACT FACTORY 패턴을 적용해 생성한다.

### ✨ 메서드

추상 메서드로 위임하는 정적 메서드는 SINGLETON, DECORATOR, ABSTRACT FACTORY 패턴 조합을 사용한다.

메서드 인수로 플래그는 바람직하지 못하다.

메서드는 단순화하고 서술적인 표현으로 가독성을 높인다.

중복이 있으면 새 메서드를 생성해 중복을 없앤다.

### ✨ 인수와 변수 선언에서 final 키워드 제거

실질적인 가치는 없으면서 코드만 복잡하게 만든다고 판단했기 때문이다.

### ✨ 숫자 1을 없앤다

## → 코드 커버리지는 84.9% 감소!

코드가 줄어서가 아니라 클래스 크기가 작아지는 바람에 테스트하지 않는 코드의 비중이 커졌기 때문이다.

---

# 💡 결론

보이스카우트 규칙

체크아웃한 코드보다 좀 더 깨끗한 코드를 체크인하게 되었다.

다음 사람은 우리보다 코드를 좀 더 쉽게 이해하리라. 그래서 우리보다 코드를 좀 더 쉽게 개선하리라.
