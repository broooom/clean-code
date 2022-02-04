# 10장 클래스📌

## 클래스 체계 ( 자바 convention에 따른 정의 순서) 👀
 1. static public
 2. static private
 3. private 인스터스
위와 같은 변수 목록을 순서대로 나온 후 `공개 함수`가 나온다. 
`비공개 함수`는 자신을 호출하는 `공개 함수` 직후에 넣는다.

> 신문 기사처럼 작성한다.

### 캡슗화
- 변수와 유틸리티 함수는 가능한 공개하지 않는 편이 좋다. (반드시 숨겨야 하는것은 아니다!)
- 때로는 `protected`로 선언해 `테스트 코드`에 접근을 허용하기도 한다.

## 클래스는 작아야 한다.

### 단일 책임 클래스
```java
public class SuperDashboard extends JFrame implements MetaDataUser {
	public Component getLastFocusedComponent()
	public void setLastFocused(Component lastFocused)
	public int getMajorVersionNumber()
	public int getMinorVersionNumber()
	public int getBuildNumber() 
}
```
간결한 이름이 떠오르지 않는다면 클래스 책임이 너무 많아서이다.
 - Manager, Processor, Super와 같은 이름은 들어가지 않는게 좋다
 - 또한 클래스 설명은 "if", "and", "or", "but"을 사용하지 않고 25 단어 내외로 가능해야된다. 
 - 한글의 경우 만약, 그리고, ~하며, 하지만 이 들어가면 안된다.
 - 위와 같은 내용이 들어가면 단일 책임이 아니라 여러가지 책임을 포함하는 이름이기 때문이다!

### 단일 책임의 원칙 - Single Responsibility Principle (`SRP`)
 - 단일 책임의 원칙은 `클래스`나 `모듈`을 변경할 이유가 단 하나뿐이어야 한다는 원칙이다.
```java
// 아래 코드에서 Version이라는 클래스를 만들어 Version 정보만 관리를 할 수 있다.
public class SuperDashboard extends JFrame implements MetaDataUser {
	public Component getLastFocusedComponent()
	public void setLastFocused(Component lastFocused)
	public int getMajorVersionNumber()
	public int getMinorVersionNumber()
	public int getBuildNumber() 
}
```
```java
// Version을 관리하는 더 작은 클래스로 분리했다.
public class Version {
	public int getMajorVersionNumber() 
	public int getMinorVersionNumber() 
	public int getBuildNumber()
}
```

> 큰 클래스 몇개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다.
> 작은 클래스는 각자 맡은 책임이 하나며, 변경할 이유가 하나며, 다른 작은 클래스와 협력해
> 시스템에 필요한 동작을 수행한다.

### 응집도(Cohension)
 - 클래스는 인스턴스 변수가 작아야 한다.
 - 각 `클래스의 메서드`는 `클래스 인스턴스 변수`를 하나 이상 사용해야 한다.
 - 일반적으로 매서드 변수를 더 많이 사용할수록 매서드와 클래스는 응집도가 더 높다.
 - 모든 `인스턴스 변수`를 `매서드마다 사용`하는 클래스는 응집도가 가장 높다.
> 인스턴스 변수를 선언하면 매서드마다 사용할수록 좋다.

```java
// 응집도가 높은 코드이다.
// 인스턴스 변수로 선언된 topOfStack, elements 들을 size()를 제외한 각 매서드에서 모두 사용했기 때문이다.
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
#### 응집도를 유지하면 작은 클래스 여럿이 나온다.
 - 변수들을 매서드에서 모두 사용하려고 하다보면 작아진다!

큰 함수 일부를 작은 함수로 빼내고 싶다

-> 빼내려는 코드가 큰 함수에 정의 된 변수를 많이 사용한다 

-> 변수들을 새 함수에 인수로 넘겨야 하나? NO!

-> 변수들을 클래스 인스턴스 변수로 승격 시키면 인수가 필요없다. But! 응집력이 낮아짐 

-> 몇몇 함수가 몇몇 인스턴스 변수만 사용한다면 독자적인 클래스로 분리해도 된다!

## 변경하기 쉬운 클래스
```java
// 해당 코드는 새로운 SQL문을 지원할 때 손대야 하고, 기존 SQL문을 수정할 때도 손대야 하므로 SRP를 위반한다.
public class Sql {
	public Sql(String table, Column[] columns)
	public String create()
	public String insert(Object[] fields)
	public String selectAll()
	public String findByKey(String keyColumn, String keyValue)
	public String select(Column column, String pattern)
	public String select(Criteria criteria)
	public String preparedInsert()
	private String columnList(Column[] columns)
	private String valuesList(Object[] fields, final Column[] columns) private String selectWithCriteria(String criteria)
	private String placeholderList(Column[] columns)
}
```
위와 같은 코드를 결합도를 낮추기 위해 아래처럼 작성해준다.
```java
// 공개 인터페이스를 전부 SQL 클래스에서 파생하는 클래스로 만들고, 비공개 메서드는 해당 클래스로 옮기고,
// 공통된 인터페이스는 따로 클래스로 뺐다.
// 이렇게 하면 update문 추가 시에 기존의 클래스를 건드릴 이유가 없어진다.

	abstract public class Sql {
		public Sql(String table, Column[] columns) 
		abstract public String generate();
	}
	public class CreateSql extends Sql {
		public CreateSql(String table, Column[] columns) 
		@Override public String generate()
	}
	
	public class SelectSql extends Sql {
		public SelectSql(String table, Column[] columns) 
		@Override public String generate()
	}
	
	public class InsertSql extends Sql {
		public InsertSql(String table, Column[] columns, Object[] fields) 
		@Override public String generate()
		private String valuesList(Object[] fields, final Column[] columns)
	}
	
	public class SelectWithCriteriaSql extends Sql { 
		public SelectWithCriteriaSql(
		String table, Column[] columns, Criteria criteria) 
		@Override public String generate()
	}
	
	public class SelectWithMatchSql extends Sql { 
		public SelectWithMatchSql(String table, Column[] columns, Column column, String pattern) 
		@Override public String generate()
	}
	
	public class FindByKeySql extends Sql public FindByKeySql(
		String table, Column[] columns, String keyColumn, String keyValue) 
		@Override public String generate()
	}
	
	public class PreparedInsertSql extends Sql {
		public PreparedInsertSql(String table, Column[] columns) 
		@Override public String generate() {
		private String placeholderList(Column[] columns)
	}
	
	public class Where {
		public Where(String criteria) public String generate()
	}
	
	public class ColumnList {
		public ColumnList(Column[] columns) public String generate()
	}
```
### 변경으로부터 격리
잘 짜여진 코드는 변경으로부터 격리되야 한다.

상세한 구현에 의존하는 코드는 테스트가 어렵다. 테스트가 가능할 정도로 시스템의 `결합도를 낮추면` `유연성`과
`재사용성`도 더욱 높아진다.

결합도가 낮다는 소리는 각 시스템 요소가 다른 요소로부터 그리고 변경으로부터 잘 격리되어 있다는 의미다.

시스템 요소가 서로 잘 격리되어 있으면 (`결합도가 낮으면`) 각 요소를 이해하기도 더 쉬워진다.

이처럼 결합도를 줄이다보면 자연스럽게 DIP(Dependency Inversion Principle) 원칙을 따를수 있게 된다.

### DIP
- 클래스 설계 원칙으로 상세한 구현이 아니라 추상화에 의존해야 한다는 원칙이다.
- `인터페이스`와 `추상클래스`를 사용하여 최대한 결합도를 낮춘 클래스 설계 원칙이라고 생각한다.
