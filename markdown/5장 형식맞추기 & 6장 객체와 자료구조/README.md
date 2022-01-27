# 5장 형식 맞추기📌

### 형식을 맞추는 목적👀
 - 코드 형식은 `의사소통`의 일환이다.
 - `코드`는 사라질지라도 개발자의 `스타일과 규율`은 사라지지 않는다.
 
### 적절한 행 길이를 유지하라
- 일반적으로 큰 파일보다 작은 파일이 이해하기 쉽다.
- 신문 기사처럼 이름은 간단하면서도 설명이 가능하게 짓고 아래로 내려갈수록 의도를 세세하게 묘사한다.
- 개념은 빈 행으로 구분한다.
  ```java
  public class BoldWidget extends ParentWidget {
    public static final String REGEXP = "'''.+?'''";
    private static final Pattern pattern = Pattern.compile("'''(.?+)'''",
      Pattern.MULTILINE + Pattern.DOTALL
    );
  // 개념 사이 빈 행으로 구분하기
  public BoldWidget (ParentWidget parent, String text) throws Exception {
    super(parent);
    Matcher match = pattern.matcher(text);
    match.find();
    addChildWidgets(match.group(1));
  }
  ```  
- 줄바꿈이 개념을 분리한다면 세로 밀집도는 연관성을 의미한다. ( 연관성이란? 한 개념을 이해하는 데 다른 개념이 중요한 정도이다.)
  ```java
  public class ReporterConfig {
    private String m_className;
    private List<Property> m_properties = new ArrayList<>();
    public void addProperty(Property property) {
      m_properties.add(property);
    }
  }
  ```
- 서로 밀접한 개념은 세로로 가까이 두어야 한다.
- `변수선언`의 변수는 `사용하는 위치`에 최대한 가까이 선언한다.
- `인스턴스 변수`는 `클래스 맨 처음`에 선언한다.
- `종속함수`처럼 한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치하고 호출하는 함수를 호출되는 함수보다 먼저 배치한다.

# 6장 객체와 자료 구조📌
###  자료 추상화
- 구현을 감추려면 `추상화`가 필요하다.
- `추상 인터페이스`를 사용해야 진정한 의미의 클래스이다.
- `객체`는 추상화 뒤로 자료를 숨긴 채 자료를 다루는 `함수만 공개`한다.
- `자료구조`는 자료를 그대로 공개하며 별다른 `함수는 제공하지 않는다`.

### 절차지향 코드 vs 객체지향 코드
- 절차적인 코드는 기존 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다.
- 객체 지향 코드는 기존 함수를 변경하지 않으면서 새 클래스를 추가하기 쉽다.
- 즉, 새로운 함수가 아닌 새로운 자료 타입이 필요한 경우 `객체 지향 기법`이 가장 적합하고
- 새로운 자료 타입이 아닌 새로운 함수가 필요한 경우 `절차적인코드와 자료 구조`가 더 적합하다.

### 디미터 법칙
- 친구랑만 놀아라 : .get 함수를 이용해서 조회할때 최소한으로 사용하자. 
- 줄이기 위해서 객체에게 적당한 임무를 맡긴다.

### 자료 전달 객체(DTO)👀
- DTO는 `bean`구조다. bean은 private변수를 getter/setter함수로 조작한다.

### 활성 레코드
- 활성 레코드는 DTO의 특수한 형태다.
- 공개 변수가 있거나 비공개 변수에 getter/setter함수가 있는 자료 구조지만, 대개 save, find와 같은 탐색 함수도 제공한다.
- 활성 레코드는 DB 테이블이나 다른 소스에서 자료를 `직접 변환한` 결과다.
- 자료 구조로 취급해 비즈니스 규칙을 담으면서 내부 자료를 숨기는 객체는 따로 생성한다.

## 결론
 `객체`는 동작을 공개하고 자료를 숨긴다.
 `자료구조`는 별다른 동작 없이 자료를 노출한다.
 
 따라서 시스템을 구현할 때, `새로운 자료 타입을 추가`하는 유연성이 필요하면 `객체` 코드가 더 적합하고
 
 `새로운 동작(함수)을 추가`하는 유연성이 필요하면 `자료구조와 절차적인` 코드가 더 적합하다.

