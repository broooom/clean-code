# 10μ₯ ν΄λμ€π

## ν΄λμ€ μ²΄κ³ ( μλ° conventionμ λ°λ₯Έ μ μ μμ) π
 1. static public
 2. static private
 3. private μΈμ€ν°μ€
μμ κ°μ λ³μ λͺ©λ‘μ μμλλ‘ λμ¨ ν `κ³΅κ° ν¨μ`κ° λμ¨λ€. 
`λΉκ³΅κ° ν¨μ`λ μμ μ νΈμΆνλ `κ³΅κ° ν¨μ` μ§νμ λ£λλ€.

> μ λ¬Έ κΈ°μ¬μ²λΌ μμ±νλ€.

### μΊ‘μν
- λ³μμ μ νΈλ¦¬ν° ν¨μλ κ°λ₯ν κ³΅κ°νμ§ μλ νΈμ΄ μ’λ€. (λ°λμ μ¨κ²¨μΌ νλκ²μ μλλ€!)
- λλ‘λ `protected`λ‘ μ μΈν΄ `νμ€νΈ μ½λ`μ μ κ·Όμ νμ©νκΈ°λ νλ€.

## ν΄λμ€λ μμμΌ νλ€.

### λ¨μΌ μ±μ ν΄λμ€
```java
public class SuperDashboard extends JFrame implements MetaDataUser {
	public Component getLastFocusedComponent()
	public void setLastFocused(Component lastFocused)
	public int getMajorVersionNumber()
	public int getMinorVersionNumber()
	public int getBuildNumber() 
}
```
κ°κ²°ν μ΄λ¦μ΄ λ μ€λ₯΄μ§ μλλ€λ©΄ ν΄λμ€ μ±μμ΄ λλ¬΄ λ§μμμ΄λ€.
 - Manager, Processor, Superμ κ°μ μ΄λ¦μ λ€μ΄κ°μ§ μλκ² μ’λ€
 - λν ν΄λμ€ μ€λͺμ "if", "and", "or", "but"μ μ¬μ©νμ§ μκ³  25 λ¨μ΄ λ΄μΈλ‘ κ°λ₯ν΄μΌλλ€. 
 - νκΈμ κ²½μ° λ§μ½, κ·Έλ¦¬κ³ , ~νλ©°, νμ§λ§ μ΄ λ€μ΄κ°λ©΄ μλλ€.
 - μμ κ°μ λ΄μ©μ΄ λ€μ΄κ°λ©΄ λ¨μΌ μ±μμ΄ μλλΌ μ¬λ¬κ°μ§ μ±μμ ν¬ν¨νλ μ΄λ¦μ΄κΈ° λλ¬Έμ΄λ€!

### λ¨μΌ μ±μμ μμΉ - Single Responsibility Principle (`SRP`)
 - λ¨μΌ μ±μμ μμΉμ `ν΄λμ€`λ `λͺ¨λ`μ λ³κ²½ν  μ΄μ κ° λ¨ νλλΏμ΄μ΄μΌ νλ€λ μμΉμ΄λ€.
```java
// μλ μ½λμμ Versionμ΄λΌλ ν΄λμ€λ₯Ό λ§λ€μ΄ Version μ λ³΄λ§ κ΄λ¦¬λ₯Ό ν  μ μλ€.
public class SuperDashboard extends JFrame implements MetaDataUser {
	public Component getLastFocusedComponent()
	public void setLastFocused(Component lastFocused)
	public int getMajorVersionNumber()
	public int getMinorVersionNumber()
	public int getBuildNumber() 
}
```
```java
// Versionμ κ΄λ¦¬νλ λ μμ ν΄λμ€λ‘ λΆλ¦¬νλ€.
public class Version {
	public int getMajorVersionNumber() 
	public int getMinorVersionNumber() 
	public int getBuildNumber()
}
```

> ν° ν΄λμ€ λͺκ°κ° μλλΌ μμ ν΄λμ€ μ¬λΏμΌλ‘ μ΄λ€μ§ μμ€νμ΄ λ λ°λμ§νλ€.
> μμ ν΄λμ€λ κ°μ λ§‘μ μ±μμ΄ νλλ©°, λ³κ²½ν  μ΄μ κ° νλλ©°, λ€λ₯Έ μμ ν΄λμ€μ νλ ₯ν΄
> μμ€νμ νμν λμμ μννλ€.

### μμ§λ(Cohension)
 - ν΄λμ€λ μΈμ€ν΄μ€ λ³μκ° μμμΌ νλ€.
 - κ° `ν΄λμ€μ λ©μλ`λ `ν΄λμ€ μΈμ€ν΄μ€ λ³μ`λ₯Ό νλ μ΄μ μ¬μ©ν΄μΌ νλ€.
 - μΌλ°μ μΌλ‘ λ§€μλ λ³μλ₯Ό λ λ§μ΄ μ¬μ©ν μλ‘ λ§€μλμ ν΄λμ€λ μμ§λκ° λ λλ€.
 - λͺ¨λ  `μΈμ€ν΄μ€ λ³μ`λ₯Ό `λ§€μλλ§λ€ μ¬μ©`νλ ν΄λμ€λ μμ§λκ° κ°μ₯ λλ€.
> μΈμ€ν΄μ€ λ³μλ₯Ό μ μΈνλ©΄ λ§€μλλ§λ€ μ¬μ©ν μλ‘ μ’λ€.

```java
// μμ§λκ° λμ μ½λμ΄λ€.
// μΈμ€ν΄μ€ λ³μλ‘ μ μΈλ topOfStack, elements λ€μ size()λ₯Ό μ μΈν κ° λ§€μλμμ λͺ¨λ μ¬μ©νκΈ° λλ¬Έμ΄λ€.
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
#### μμ§λλ₯Ό μ μ§νλ©΄ μμ ν΄λμ€ μ¬λΏμ΄ λμ¨λ€.
 - λ³μλ€μ λ§€μλμμ λͺ¨λ μ¬μ©νλ €κ³  νλ€λ³΄λ©΄ μμμ§λ€!

ν° ν¨μ μΌλΆλ₯Ό μμ ν¨μλ‘ λΉΌλ΄κ³  μΆλ€

-> λΉΌλ΄λ €λ μ½λκ° ν° ν¨μμ μ μ λ λ³μλ₯Ό λ§μ΄ μ¬μ©νλ€ 

-> λ³μλ€μ μ ν¨μμ μΈμλ‘ λκ²¨μΌ νλ? NO!

-> λ³μλ€μ ν΄λμ€ μΈμ€ν΄μ€ λ³μλ‘ μΉκ²© μν€λ©΄ μΈμκ° νμμλ€. But! μμ§λ ₯μ΄ λ?μμ§ 

-> λͺλͺ ν¨μκ° λͺλͺ μΈμ€ν΄μ€ λ³μλ§ μ¬μ©νλ€λ©΄ λμμ μΈ ν΄λμ€λ‘ λΆλ¦¬ν΄λ λλ€!

## λ³κ²½νκΈ° μ¬μ΄ ν΄λμ€
```java
// ν΄λΉ μ½λλ μλ‘μ΄ SQLλ¬Έμ μ§μν  λ μλμΌ νκ³ , κΈ°μ‘΄ SQLλ¬Έμ μμ ν  λλ μλμΌ νλ―λ‘ SRPλ₯Ό μλ°νλ€.
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
μμ κ°μ μ½λλ₯Ό κ²°ν©λλ₯Ό λ?μΆκΈ° μν΄ μλμ²λΌ μμ±ν΄μ€λ€.
```java
// κ³΅κ° μΈν°νμ΄μ€λ₯Ό μ λΆ SQL ν΄λμ€μμ νμνλ ν΄λμ€λ‘ λ§λ€κ³ , λΉκ³΅κ° λ©μλλ ν΄λΉ ν΄λμ€λ‘ μ?κΈ°κ³ ,
// κ³΅ν΅λ μΈν°νμ΄μ€λ λ°λ‘ ν΄λμ€λ‘ λΊλ€.
// μ΄λ κ² νλ©΄ updateλ¬Έ μΆκ° μμ κΈ°μ‘΄μ ν΄λμ€λ₯Ό κ±΄λλ¦΄ μ΄μ κ° μμ΄μ§λ€.

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
### λ³κ²½μΌλ‘λΆν° κ²©λ¦¬
μ μ§μ¬μ§ μ½λλ λ³κ²½μΌλ‘λΆν° κ²©λ¦¬λμΌ νλ€.

μμΈν κ΅¬νμ μμ‘΄νλ μ½λλ νμ€νΈκ° μ΄λ ΅λ€. νμ€νΈκ° κ°λ₯ν  μ λλ‘ μμ€νμ `κ²°ν©λλ₯Ό λ?μΆλ©΄` `μ μ°μ±`κ³Ό
`μ¬μ¬μ©μ±`λ λμ± λμμ§λ€.

κ²°ν©λκ° λ?λ€λ μλ¦¬λ κ° μμ€ν μμκ° λ€λ₯Έ μμλ‘λΆν° κ·Έλ¦¬κ³  λ³κ²½μΌλ‘λΆν° μ κ²©λ¦¬λμ΄ μλ€λ μλ―Έλ€.

μμ€ν μμκ° μλ‘ μ κ²©λ¦¬λμ΄ μμΌλ©΄ (`κ²°ν©λκ° λ?μΌλ©΄`) κ° μμλ₯Ό μ΄ν΄νκΈ°λ λ μ¬μμ§λ€.

μ΄μ²λΌ κ²°ν©λλ₯Ό μ€μ΄λ€λ³΄λ©΄ μμ°μ€λ½κ² DIP(Dependency Inversion Principle) μμΉμ λ°λ₯Όμ μκ² λλ€.

### DIP
- ν΄λμ€ μ€κ³ μμΉμΌλ‘ μμΈν κ΅¬νμ΄ μλλΌ μΆμνμ μμ‘΄ν΄μΌ νλ€λ μμΉμ΄λ€.
- `μΈν°νμ΄μ€`μ `μΆμν΄λμ€`λ₯Ό μ¬μ©νμ¬ μ΅λν κ²°ν©λλ₯Ό λ?μΆ ν΄λμ€ μ€κ³ μμΉμ΄λΌκ³  μκ°νλ€.
