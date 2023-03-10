# 💡 클래스 체계

클래스를 정의하는 표준 자바 관례에 따르면, 가장 먼저 변수 목록이 나온다.

정적 공개 상수 `static public` → 정적 비공개 변수 `static private`
→ 비공개 인스턴스 변수 `private` → 공개 변수`public` (필요한 경우가 거의 없다.

다음으로는 공개 함수가 나온다.

비공개 함수는 자신을 호출하는 공개 함수 직후에 넣는다. 즉, 추상화 단계가 순차적으로 내려간다. 그래서 프로그램은 신문 기사처럼 읽힌다.

## ✨ 캡슐화

💙 캡슐화를 풀어주는 결정은 언제나 최후의 수단이다.

변수와 유틸리티 함수는 가능한 공개하지 않는 편이 낫지만 반드시 숨겨야 한다는 법칙도 없다. 
때로는 변수나 유틸리티 함수를 protected로 선언해 테스트 코드에 접근을 허용하기도 한다.

같은 패키지 안에서 테스트 코드가 함수를 호출하거나 변수를 사용해야 한다면 그 함수나 변수를 protected로 선언하거나 패키지 전체로 공개한다.

하지만 공개 전 비공개 상태를 유지할 온갖 방법을 강구하며 캡슐화를 풀어주는 결정은 언제나 최후의 수단이다.

---

# 💡 클래스는 작아야 한다!

💙 클래스를 만드는 첫 번째 규칙은 크기이다. 클래스는 작아야 한다.
두 번째 규칙도 크기다. 더 작아야 한다.
클래스의 규모는 맡은 책임을 센다.


```java
public class SuperDashboard extends JFrame implements MetaDataUser {
	public Component getLastFocusedComponent()
	public void setLastFocused(Component lastFocused)
	public int getMajorVersionNumber()
	public int getMinorVersionNumber()
	public int getBuildNumber() 
}
```

클래스 이름은 해당 클래스 책임을 기술해야 한다.

작명은 클래스 크기를 줄이는 첫 번째 관문이다. → 간결한 이름이 떠오르지 않는다면 클래스의 크기가 너무 커서, 책임이 너무 많아서 이다.
이름에 Processor, Manager, Super 등의 모호한 단어가 있다면 책임을 떠안겼다는 증거

클래스 설명은 만일 if, 그리고 and, -하며 or, 하지만 but을 사용하지 않고서 25자 내외로 가능해야 한다.

## ✨ 단일 책임 원칙 Single Responsibility Principle

단일 책임 원칙은 클래스나 모듈을 변경할 이유가 단 하나뿐이어야 한다는 원칙이다.
SRP는 ‘책임’이라는 개념을 정의하며 적절한 클래스 크기를 제시한다.
클래스는 책임, 즉 변경할 이유가 하나여야 한다는 의미다.

책임, 즉 변경할 이유를 파악하려 애쓰다 보면 코드를 추상화하기도 쉬워진다.

```java
//독자적인 클래스
//Version 클래스는 다른 애플리케이션에서 재사용하기 아주 쉬운 구조다!
public class Version {
	public int getMajorVersionNumber() 
	public int getMinorVersionNumber() 
	public int getBuildNumber()
}
```

SRP는 객체 지향 설계에서 중요한 개념이자 이해하고 지키기 수월한 개념이지만 설계자가 가장 무시하는 규칙 중 하나이다.

대부분은 깨끗하고 체계적인 소프트웨어보다 돌아가는 소프트웨어에 초점을 맞춘다.
→ 문제는 프로그램이 돌아가면 끝났다고 여기는 데 있다. 깨끗하고 체계적인 소프트웨어라는 다음 관심사로 전환하지 않는다.

> 도구 상자를 어떻게 관리하고 싶은가?
작은 서랍을 많이 두고 기능과 이름이 명확한 컴포넌트를 나눠 넣고 싶은가?
아니면 큰 서랍 몇 개를 두고 모두를 던져 넣고 싶은가?
> 

큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다. 작은 클래스는 각자 맡은 책임이 하나며, 변경할 이유가 하나며, 다른 작은 클래스와 협력해 시스템에 필요한 동작을 수행한다.

## ✨ 응집도 Cohesion

클래스는 인스턴스 변수의 수가 작아야 한다. 
각 클래스 메서드는 클래스 인스턴스 변수를 하나 이상 사용해야 한다.
일반적으로 메서드가 변수를 더 많이 사용할수록 메서드와 클래스는 응집도가 더 높다.
모든 인스턴스 변수를 메서드마다 사용하는 클래스는 응집도가 가장 높다.

응집도가 높은 클래스는 바람직하지 않다. 하지만 우리는 선호한다.
응집도가 높다는 말은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미이기 때문이다.

```java
public class Stack {
	private int topOfStack = 0;
	List<Integer> elements = new LinkedList<Integer>();

	public int size() { 
		return topOfStack;
	}

	public void push(int element) { 
		topOfStack++; 
		elements.add(element);
	}
	
	public int pop() throws PoppedWhenEmpty { 
		if (topOfStack == 0)
			throw new PoppedWhenEmpty();
		int element = elements.get(--topOfStack); 
		elements.remove(topOfStack);
		return element;
	}
}
```

‘함수를 작게, 매개변수 목록을 짧게’ 전략을 따르다보면 몇몇 메서드만이 사용하는 인스턴스 변수가 많아진다. → 이는 새로운 클래스로 쪼개야 한다는 신호

응집도가 높아질수록 변수와 메서드를 적절히 분리해 새로운 클래스 두세 개로 쪼개준다.

## ✨ 응집도를 유지하면 작은 클래스 여럿이 나온다

클래스가 응집력을 잃는다면 쪼개라!

큰 함수를 작은 함수 여럿으로 쪼개다 보면 종종 작은 클래스 여럿으로 쪼갤 기회가 생긴다. 그러면서 프로그램에 점점 더 체계가 잡히고 구조가 투명해진다.

- 작은 함수와 클래스로 나눈 후 함수와 클래스와 변수에 좀 더 의미 있는 이름을 부여한 코드
    
    프로그램의 길이가 길어진 이유
    → 리팩터링한 프로그램은 좀 더 길고 서술적인 변수 이름을 사용한다.
    → 리팩터링한 프로그램은 코드에 주석을 추가하는 수단으로 함수 선언과 클래스 선언을 활용한다.
    → 가독성을 높이고자 공백을 추가하고 형식을 맞추었다.
    

가장 먼저, 원래 프로그램의 정확한 동작을 검증하는 테스트 슈트를 작성한다.

그런 다음, 한 번에 하나씩 수 차례에 걸쳐 조금씩 코드를 변경한다.

코드를 변경할 때마다 테스트를 수행해 원래 프로그램과 동일한지 확인한다.

---

# 💡 변경하기 쉬운 클래스

시스템은 지속적으로 변경이 가해지며 변경할 때마다 시스템이 의도대로 동작하지 않는 위험이 따른다.

깨끗한 시스템은 클래스를 체계적으로 정리해 변경에 수반하는 위험을 낮춘다.

새 기능을 수정하거나 기존 기능을 변경할 때 건드릴 코드가 최소인 시스템 구조가 바람직하다.

이상적인 시스템이라면 새 기능을 추가할 때 시스템을 확장할 뿐 기존 코드를 변경하지는 않는다.

## ✨ 변경으로부터 격리

구체적인 클래스와 추상 클래스가 있다.
구체적인 클래스는 상세한 구현을 포함하며 추상 클래스는 개념만 포함한다.
상세한 구현에 의존하는 클라이언트 클래스는 구현이 바뀌면 위험에 빠진다.
→ 따라서 우리는 인터페이스와 추상 클래스를 사용해 구현이 미치는 영향을 격리한다.

상세한 구현에 의존하는 코드는 테스트가 어렵다.
→ 테스트가 가능할 정도로 시스템의 결합도를 낮추면 유연성과 재사용성이 높아진다.

`결합도가 낮다`
: 각 시스템 요소가 다른 요소로부터 그리고 변경으로부터 잘 격리되어 있다는 의미

결합도를 최소로 줄이면 자연스럽게 또 다른 클래스 설계 원칙인 DIP를 따르는 클래스가 나온다. DIP는 클래스가 상세한 구현이 아니라 추상화에 의존해야 한다는 원칙이다.
→ 추상화를 통해 실제 출처나 방식 등의 구체적인 사실을 모두 숨긴다.
