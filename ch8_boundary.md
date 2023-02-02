
시스템에 들어가는 모든 소프트웨어를 직접 개발하는 경우는 드물다.
외부코드를 우리 코드에 깔끔하게 통합해야 한다.

> 🔥 소프트웨어 경계를 깔끔하게 처리하는 기법과 기교 살펴보기!


**경계란?**

외부 코드를 내 코드에서 호출하는 부분을 경계

---

# 💡 외부 코드 사용하기

인터페이스 제공자와 사용자 사이에는 특유의 긴장이 존재한다.

**제공자**(패키지, 프레임워크) 
→ 더 많은 환경에서 더 많은 고객이 구매 가능하게 적용성을 넓히려고 애쓴다.

**사용자**
→ 자신의 요구에 집중하는 인터페이스를 바란다.

### `Map`이 제공하는 메서드

Map은 굉장히 다양한 인터페이스로 수많은 기능을 제공한다.
    
Map이 제공하는 기능성과 유연성은 확실히 유용하지만 그만큼 위험도 크다.
    
Map이 반환하는 Object를 올바른 유형으로 변환할 책임은 Map을 사용하는 클라이언트에 있다. 

```java
clear() void – Map
containsKey(Object key) boolean – Map
containsValue(Object value) boolean – Map
clear() void – Map
containsKey(Object key) boolean – Map
containsValue(Object value) boolean – Map
entrySet() Set – Map
equals(Object o) boolean – Map
get(Object key) Object – Map
getClass() Class<? extends Object> – Object
hashCode() int – Map
isEmpty() boolean – Map
keySet() Set – Map
notify() void – Object
notifyAll() void – Object
put(Object key, Object value) Object – Map
putAll(Map t) void – Map
remove(Object key) Object – Map
size() int – Map
toString() String – Object
values() Collection – Map
wait() void – Object
wait(long timeout) void – Object
wait(long timeout, int nanos) void – Object
```   

```java
>>bad
Map sensors = new HashMap();

Sensor s = (Sensor)sensors.get(sensorId);

Map<String, Sensor> sensors = new HashMap<Sensor>();
...
Sensor s = sensors.get(sensorId);

>>good
public class Sensors {
private Map sensors = new HashMap();

public Sensor getById(String id){
    return (Sensor) sensors.get(id);
  }
  ..
}
```

- 경계 인터페이스인 `Map`을 `Sensors` 안으로 숨기므로 `Map` 인터페이스가 변하더라도 나머지 프로그램에는 영향을 미치지 않는다.
제네릭스의 사용 여부에도 문제가 되지 않는다.
→Sensors 클래스 안에서 객체 유형을 관리하고 변환하기 때문이다.
- `Sensors` 클래스는 프로그램에 필요한 인터페이스만 제공한다.
→코드는 이해하기 쉽지만 오용하기 어렵다. 설계 규칙과 비즈니스 규칙을 따르도록 강제할 수 있다.
- 매번 사용할 때마다 캡슐화하라는 소리가 아니다.
→`Map`을 여기저기 넘기지 말라는 말이다.
→이용하는 클래스나 클래스 계열 밖으로 노출되지 않도록 주의한다.
→`Map`인스턴스를 공개 API의 인수로 넘기거나 반환값으로 사용하지 않는다.

---

# 💡 경계 살피고 익히기

> 외부에서 가져온 패키지를 사용하고 싶다면 어디서 어떻게 시작해야 좋을까?

우리 자신을 위해 우리가 **사용할 코드를 테스트**하는 편이 바람직하다.

- 문서를 읽으며 사용법을 결정하자
- 코드를 작성해 라이브러리가 예상대로 동작하는지 확인하자

코드를 작성해 외부 코드를 호출하는 대신 먼저 간단한 테스트 케이스를 작성해 외부 코드를 익힌다.

- **학습 테스트** _ 짐 뉴커크
- 프로그램에서 사용하려는 방식대로 외부 API를 호출한다.
→ 통제된 환경에서 API를 제대로 이해하는지를 확인하는 것
→ API를 사용하려는 목적에 초점을 맞춤

---

# 💡 log4j 익히기

### 1️⃣ 첫 번째 테스트 케이스
: 패키지를 내려 받고 소개 페이지를 열어 화면에 hello를 출력하는 테스트 케이스
    
```java
@Test
public void testLogCreate() {
    Logger logger = Logger.getLogger("MyLogger");
    logger.info("hello");
}
```
    
Error.

→ Appender이 필요하다는 오류 발생
    `ConsoleAppender`라는 클래스가 필요
    
### 2️⃣ 두 번째 테스트 케이스
    
```java
@Test
public void testLogAddAppender() {
    Logger logger = Logger.getLogger("MyLogger");
    ConsoleAppender appender = new ConsoleAppender();
    logger.addAppender(appender);
    logger.info("hello");
}
```
    
Error.
   
→ Appender에 출력 스트림이 없다는 오류 발생
    
### 3️⃣ 세 번째 테스트 케이스
    
```java
@Test
public void testLogAddAppender() {
    Logger logger = Logger.getLogger("MyLogger");
    logger.removeAllAppenders();
    logger.addAppender(new ConsoleAppender(
        new PatternLayout("%p %t %m%n"),
        ConsoleAppender.SYSTEM_OUT));
    logger.info("hello");
}
```
    

- LogTest.java
    
    ```java
    public class LogTest {
        private Logger logger;
        
        @Before
        public void initialize() {
            logger = Logger.getLogger("logger");
            logger.removeAllAppenders();
            Logger.getRootLogger().removeAllAppenders();
        }
        
        @Test
        public void basicLogger() {
            BasicConfigurator.configure();
            logger.info("basicLogger");
        }
        
        @Test
        public void addAppenderWithStream() {
            logger.addAppender(new ConsoleAppender(
                new PatternLayout("%p %t %m%n"),
                ConsoleAppender.SYSTEM_OUT));
            logger.info("addAppenderWithStream");
        }
        
        @Test
        public void addAppenderWithoutStream() {
            logger.addAppender(new ConsoleAppender(
                new PatternLayout("%p %t %m%n")));
            logger.info("addAppenderWithoutStream");
        }
    }
    ```
    
---

# 💡 학습 테스트는 공짜 이상이다

필요한 지식만 확보하는 손쉬운 방법. 이해도를 높여주는 정확한 실험.

- 학습 테스트는 **공짜 이상**이다.
    
    투자하는 노력보다 얻는 성과가 크다.
    패키지 새 버전이 나온다면 학습 테스트를 돌려 차이가 있는지 확인한다.
    
- 학습 테스트는 **패키지가 예상대로 도는지 검증**한다.
    
    우리 코드와 패키지가 호환된다는 보장이 없다.
    코드를 변경할 필요가 생길 수 있다.
    작성자는 버그를 수정하고 기능을 추가하기에 새 버전이 나올 때마다 새로운 위험이 생긴다.
    
- **실제 코드와 동일한 방식으로 인터페이스를 사용하는 테스트 케이스**가 필요하다.
    
    경계 테스트가 있다면 패키지의 새 버전으로 이전하기 쉬워진다.
    없다면 낡은 버전을 필요 이상으로 오랫동안 사용하려는 유혹에 빠지기 쉽다.

---

# 💡 아직 존재하지 않는 코드를 사용하기

아는 코드와 모르는 코드를 분리하는 경계.

구현되지 않은 인터페이스가 필요한 경우가 있다.
→ 이런 제약 상황으로 개발이 늦어질 수 있음.

→ 이를 해결하기 위해 자체적으로 필요한 인터페이스를 정의했다.
    (코드의 가독성도 높아지고 코드의 의도도 분명해진다.)

---

# 💡 깨끗한 경계

경계에서는 흥미로운 일이 많이 벌어진다.

소프트웨어 설계가 우수하다면 변경하는데 많은 투자와 재작업이 필요하지 않다. 시간과 노력과 재작업을 요구하지 않는다.

- 경계에 위치하는 코드는 깔끔히 분리한다.
기대치를 정의하는 테스트 케이스도 작성한다.
→ 통제가 가능한 우리 코드에 의존하는 편이 훨씬 좋다.
- 외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리하자.
새로운 클래스로 경계를 감싸거나 우리가 원하는 인터페이스를 패키지가 제공하는 인터페이스로 변환하자.
→ 코드의 가독성이 높아지며, 경계 인터페이스를 사용하는 일관성도 높아지며, 외부 패키지가 변했을 때 변경할 코드도 줄어든다.
