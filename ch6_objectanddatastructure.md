
# 💡 자료 추상화

    >> public , 구체적인 클래스
    public class Point {
      public double x;
      public double y;
    }

    >> abstract , 추상적인 클래스
    public interface Point {
      double getX();
      double getY();
      void setCartesian(double x, double y); 
      double getR();
      double getTheta();
      void setPolar(double r, double theta); 
    }

구현을 감추려면 추상화가 필요하다!

그저 조회 함수와 설정 함수로 변수를 다룬다고 클래스가 되지 않는다. 추상 인터페이스를 제공해 사용자가 구현을 모른 채 자료의 핵심을 조작할 수 있어야 진정한 의미의 클래스다.

자료를 세세하게 공개하기보다는 추상적인 개념으로 표현하는 편이 좋다. 인터페이스나 조회,설정 함수만으로는 추상화가 이뤄지지 않는다.

---

# 💡 자료/객체 비대칭

* 객체는 추상화 뒤로 자료를 숨긴 채 자료를 다루는 함수만 공개한다.
* 자료 구조는 자료를 그대로 공개하며 별다른 함수는 제공하지 않는다.

> 🔥 절차적인 코드는 기존 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다. 반면, 객체 지향 코드는 기존 함수를 변경하지 않으면서 새 클래스를 추가하기 쉽다.
절차적인 코드는 새로운 자료 구조를 추가하기 어렵다. 그러려면 모든 함수를 고쳐야 한다. 객체 지향 코드는 새로운 함수를 추가하기 어렵다. 그러려면 모든 클래스를 고쳐야 한다.

즉, 객체에서 어려운 건 절차에서 쉽고, 객체에서 쉬운 건 절차에서 어렵다.

---

# 💡 디미터 법칙

휴리스틱(경험을 통해서, 스스로 체험하여 발견하게 하는 방법)
자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙

디미터 법칙

다른 객체가 어떠한 자료를 가지고 있는지 속사정을 몰라야 한다.

> Don’t talk to strangers , Principle of least Knowledge

객체는 자료를 숨기고 함수를 공개한다. 객체는 조회 함수로 내부 구조를 공개하면 안 된다는 의미이다.

“클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다.”

* 클래스 C
* f가 생성한 객체
* f 인수로 넘어온 객체
* C 인스턴스 변수에 저장된 객체

하지만 위 객체에서 허용된 메서드가 반환하는 객체의 메서드는 호출하면 안 된다.

### ✨ 기차 충돌

    >>Bad

    final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

위와 같은 코드를 기차 충돌이라 부른다.
여러 객체가 한 줄로 이어진 기차처럼 보이기 때문이다. 일반적으로 조잡하다 여겨지는 방식이므로 피하는 편이 좋다.

기차 충돌이 좋지 않은 이유 : 한 메서드가 알 필요가 없는 객체의 메서드까지 접근하기 때문

    >>Good

    Options opts = ctxt.getOptions();
    File scratchDir = opts.getScratchDir();
    final String outputDir = scratchDir.getAbsolutePath();

    final String outputDir = ctxt.options.scratchDir.absolutePath;

디미터 법칙을 위반하는지 여부는 객체인지 자료구조인지에 따라 달렸다.
객체라면 내부 구조를 숨겨야 하므로 확실히 디미터 법칙을 위반한다.
반면, 자료 구조라면 당연히 내부 구조를 노출하므로 디미터 법칙이 적용되지 않는다.

### ✨ 잡종 구조

때때로 절반은 객체, 절반은 자료 구조인 잡종 구조가 나온다.

잡종 구조는 중요한 기능을 수행하는 함수도 있고, 공개 변수나 공개 조회,설정 함수도 있다. 공개 조회,설정 함수는 비공개 변수를 그대로 노출한다.

이런 잡종 구조는 새로운 함수는 물론, 새로운 자료 구조도 추가하기 어렵다.
그러므로 잡종 구조는 되도록 피하는 편이 좋다.

### ✨ 구조체 감추기

    String outFile = outputDir + "/" + className.replace('.', '/') + ".class"; 
    FileOutputStream fout = new FileOutputStream(outFile); 
    BufferedOutputStream bos = new BufferedOutputStream(fout);

추상화 수준을 뒤섞어 놓아 다소 불편하다. 점, 슬래시, 파일 확장자, File 객체를 부주의하게 마구 뒤섞으면 안 된다.
위 코드는 임시 디렉터리의 절대 경로를 얻으려는 이유가 임시 파일을 생성하기 위한 목적이라는 사실이 드러난다.

`ctxt` 객체에 임시 파일을 생성하라고 시키면 어떨까?

    BufferedOutputStream bos = ctxt.createScratchFileStrean(classFileName);

---

# 💡 자료 전달 객체 _ Data Transfer Object

자료 구조체의 전형적인 형태는 공개 변수만 있고 함수가 없는 클래스다.
이런 자료 구조체를 때로는 자료 전달 객체라 한다.

DTO는 굉장히 유용한 구조체다. 특히 데이터베이스와 통신하거나 소켓에서 받은 메시지의 구문을 분석할 때 유용하다.

빈 `bean`

자바 객체에는 데이터가 있어 그에 해당하는 getter와 setter가 있다.
이러한 변수와 그 값을 저장하고 꺼내올 수 있는 구조의 객체를 자바 빈이라고 한다.

    public class Address {
    	private String street;
    	private String streetExtra;
    	private String city;
    	private String state;
    	private String zip;
    	...
    	public String getName() {
    		return name;
    	}
    } 

### ✨ 활성 레코드

활성 레코드는 DTO의 특수한 형태다.
공개 변수가 있거나 비공개 변수에 조회, 설정 함수가 있는 자료 구조지만, 대개 save나 find와 같은 탐색 함수도 제공한다.
활성 레코드는 데이터베이스 테이블이나 다른 소스에서 자료를 직접 반환한 결과다.

활성 레코드는 자료 구조로 취급한다.
비즈니스 규칙을 담으려면 내부 자료를 숨기는 객체는 따로 생성한다.

---

# 💡 결론

객체는 동작을 공개하고 자료를 숨긴다.

그래서 기존 동작을 변경하지 않으면서 새 객체 타입을 추가하기는 쉬운 반면, 기존 객체에 새 동작을 추가하기는 어렵다.

자료 구조는 별다른 동작 없이 자료를 노출한다. 그래서 기존 자료 구조에 새 동작을 추가하기는 쉬우나, 기존 함수에 새 자료 구조를 추가하기는 어렵다.

