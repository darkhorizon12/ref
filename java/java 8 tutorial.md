# java 8 

아래의 모든 내용은 [여기](http://winterbe.com/posts/2014/03/16/java-8-tutorial/) 의 내용을 적은것이다. 

목표는 빠른 파악의 레벨이므로 원문에 있는 나름 심오한 내용등은 빠질 수 있다. 그건 원문을 보고 따로 학습하길 바란다. 작업은 2014년 4월 9일 12시부터 시작한다.(사실 이때부터 원문을 읽고 있다)

이 사이트를 알려준 장진우님께 감사드린다.

## 번역참고사항

- anonymous : 익명 
- lambda : 람다
- expressions : 표현식
- lambda expressions : 람다표현식 
- syntax : 문법  

## Default Method for Interface
아주 간단히 말하면 인터페이스에 구현이 가능하다.
``` java
interface Formula {
    double calculate(int a);

    default double sqrt(int a) {
        return Math.sqrt(a);
    }
}
```

위에 `default` 라는 키워드가 있는데 이 키워드를 적용하면 비추상 메소드 구현이 가능해진다. Extension method 라고도 한단다.

아래는 구현이다.
``` java
Formula formula = new Formula() {
    @Override
    public double calculate(int a) {
        return sqrt(a * 100);
    }
};

formula.calculate(100);     // 100.0
formula.sqrt(16);           // 4.0
```

실제 이 인터페이스를 이용할때는 default 를 적용한 sqrt 를 구현하지 않아도 된다. 

# Lambda expressions

아래는 이전버전에서의 자바 문장 sort 예제이다. 

``` java
List<String> names = Arrays.asList("peter", "anna", "mike", "xenia");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return b.compareTo(a);
    }
});
```
위와 같은 `Collections.sort`의 구현형태는 익명 `Compatator`를 빈번히 만들어야 한다. 

이런 익명의 오브젝트를 만드는것 대신 Java 8 은 람다표현식 같은 짧은 문법 이 제공한다. 

``` java
Collections.sort(names, (String a, String b) -> {
    return b.compareTo(a);
});
```

더 짧게도 가능하다.

``` java
Collections.sort(names, (String a, String b) -> b.compareTo(a));
```

한줄 메소드 형태는 {}, return 키워드를 뺄 수 있다. 이게 더 짧게도 가능하다.

``` java
Collections.sort(names, (a, b) -> b.compareTo(a));
```

java 컴파일러는 파라미터의 타입을 추측하기에 String 을 생략가능하다. 





