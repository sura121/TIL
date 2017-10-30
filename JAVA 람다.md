##JAVA 람다 

1. 람다식

- 람다식이란?

	람다식은 메서드를 하나의 식(expression)으로 표현한 것.
    
    - 객체 지향 언어보다는 함수 지향 언어에 가깝다.
    - 함수를 간략하면서도 명확한 식으로 편현할 수 있도록 해준다.
    - 메서드를 람다식으로 표현하면 메서드의 이름 및 반환 값이 업어지므로 익명 함수라고도 한다.
	- 람다식의 형태는 매개 변수를 가진 코드 블록이지만 런타임 시에는 익명 구현 객체를 생성한다.


```
(타입 매개변수) -> { 실행문; ... }

ex)
- ExFunctionInterfaceTest.java

interface ExFunctionInterface
{
    public void method();
}


public class ExFunctionInterfaceTest
{
    public static void main(String[] args)
    {
        ExFunctionInterface test = new ExFunctionInterface() {

            public void method() {
                System.out.println("test");
            }
        };

        test.method();
    }
}

public class ExFunctionInterfaceTest
{
    public static void main(String[] args)
    {
        ExFunctionInterface test = () -> System.out.println("test");

        test.method();
    }
}

```

- 반환 값이 있는 메서드의 경우 return 대신 expression 으로 대신할 수 있다.
	(expression인 경우 ; 를 붙이지 않는다.)
- 람다식에 선언된 매개변수 타입은 추론이 가능한 경우 생략 가능 (대부분 생략 가능)
- 매개 변수가 하나인 경우 ()를 생략할 수 있다.
- {} 안 문장이 하나인 경우 생략할 수 있다.

### 함수형 인터페이스(Functional Interface)

함수형 인터페이스는 람다식을 다루기 위한 인터페이스로 하나의 추상 메서드만 정의되어 있어야 한다. 단 static 메서드와 default 메서드의 개수에는 제약이 없다.
- 함수형 인터페이스 타입의 매개변수 및 반환 타입이 함수형 인터페이스 타입이라면 람다식을 참조하는 참조변수를 매개변수로 지정하고 람다식을 가리키는 참조 변수를 반환하거나 또는 람다식 자체를 반환할 수 있다.
- 람다식은 Object 타입으로 형변환 할 수 없으며, 오직 함수형 인터페이스로만 형변환이 가능하다.
- 람다식 내에서 참조하는 지역변수는 final이 붙어 있지 않아도 상수로 간주되며, 외부 지역변수와 같은 이름의 매개변수를 허용하지 않는다.
- 함수형 인터페이스는 @Funtionallinterface라는 어노테이션을 붙일 수 있다.(컴파일러에서 추상메서드를 갖춘 인터페이스인지 검사, javadoc 페이지에서 해당 인터페이스가 함수형 인터페이스임을 알 수 있도록 한다)


