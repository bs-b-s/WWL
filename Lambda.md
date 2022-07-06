# Lambda

## 람다란 무엇인가 ?
```람다 표현식```이란 메서드로 전달할 수 있는 ```익명 함수```를 단순화 한 것

***

### 람다의 특징
* 익명 : 보통 메서드와 달리 이름이 없기에 ```익명```이라고 표현한다.
* 함수 : 메서드처럼 특정 클래스에 종속되지 않기 때문에 ```함수```라고 부른다.
* 전달 : 람다 표현식을 메서드 ```인수```로 전달하거나 ```변수```로 저장할 수 있다.
* 간결성 : 익명 클래스처럼 많은 코드를 구현할 필요가 없다.

***

## 람다 시작하기
### 람다 사용 전
```javascript
Comparator<Apple> byWeight = new Comparator<Apple>(){
    public int compare(Apple a1, Apple a2){
        return a1.getWeight.compareTo(a2.getWeight);
    }
}
```

### 람다 사용 후
```javascript
Comparator<Apple> byWeight = (Apple a1, Apple a2) 
    -> a1.getWeight().compareTo(a2.getWeight());
```

> Comparator : ```comareTo``` 메서드를 제공하는 함수형 인터페이스
>
> compareTo : 값이 같으면 ```true```, 다르면 ```false```

이렇게 람다를 사용하면 코드가 훨씬 간결해진다.

람다를 사용한 코드에서 볼 수 있듯 람다는 3부분으로 나뉘는데,
* 파라미터 리스트 : Comparator의 compare 메서드 파라미터(사과 2개) - ```(Apple a1, Apple a2)```
* 화살표 : 리스트와 바디를 구분함 - ```->```
* 람다 바디 : 람다의 반환값에 해당하는 표현식이다. - ```a1.getWeight().compareTo(a2.getWeight());```

***

## 람다 표현식

```
(String s) -> s.length();

(Apple a) -> a.getWeight() > 150 //boolean 반환
```
* 하나의 파라미터를 가지므로 return 문을 사용하지 않아도 된다.

``` 
(int x, int y) -> {
    System.out.println("Result : ");
    System.out.println(x + y);
}
```
* 반환 값이 void 이기 때문에 return 문을 사용하지 않는다. ```중괄호```를 사용해서 여러 문장을 포함할 수 있다.

```
() -> 42
```
* 파라미터가 없으며 int 42를 반환한다.
```
(Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
```

* 파라미터 2개를 가지며 두 사과의 무게 비교 결과를 반환한다.

> ## 람다 문법 문제
> 람다 규칙에 맞지 않는 람다 표현식을 고르시오.
> 1. ```() -> {}```
> 2. `````() -> "Raoul"`````
> 3. ```() -> {return "Mario";}```
> 4. ```(Integer i) -> return "Alan" + i;```
> 5. ```(String s) -> {"Iron Man"}```

***

그래서 정확히 어디에서 람다를 사용할 수 있다는 건지 궁금할 수 있다.
바로 함수형 인터페이스라는 문맥에서 람다 표현식을 사용할 수 있다.

## 함수형 인터페이스
```함수형 인터페이스```는 정확히 하나의 추상 메서드를 지정하는 인터페이스이다.

## 함수형 인터페이스 문제
> 다음 인터페이스 중 함수형 인터페이스는 어느 것인가?
```
public interface Adder {
    int add(int a, int b);
}

public interface SmartAdder extends Adder {
    int add(double a, double b);
}

public interface Nothing {
}
```

***

## 함수형 인터페이스를 기대하는 곳에서 람다 표현식 사용하기
```javascript
package anonymous;

public class UseAnonymousClass{

    public static void process(Runnable r) {
        r.run();
    }

    public static void main(String[] args) {
        Runnable r1 = () -> System.out.println("Hello Lambda!!"); // 1
        Runnable r2 = new Runnable() { // 2
            @Override
            public void run() {
                System.out.println("Hello Lambda2!!");
            }
        };

        process(r1);
        process(r2);
        process(() -> System.out.println("Hello Lambda3!!"));
    }
}
    
```

1. `람다 사용`
2. `Runnable` 이라는 `익명 함수 클래스`를 사용함

***

## 함수형 인터페이스 사용해보기
### Supplier <T> - 매개변수 X, 반환 T

```javascript
Supplier<String> supplier = () -> "Hello Lambda!!";
System.out.println(supplier.get());
```
***

### Consumer <T> - 매개변수 T, 반환 X
```javascript
Consumer<String> consumer = (str) -> System.out.println(str.split(" ")[0]);
consumer.andThen(System.out::println).accept("Hello Lambda!!");
```

***

### Function <T> - 매개변수 T, 코드 수행 후 R로 반환
```javascript
Function<String, Integer> function = (str) -> str.length();
System.out.println(function.apply("Hello Lambda!!"));
```

***

### Predicate <T> - 매개변수 T, 반환 Boolean
```javascript
Predicate<String> predicate = (str) -> str.equals("Hello Lambda!!");
System.out.println(predicate.test("hello lambda!!"));
```

***
## 람다는 무조건 기본적으로 제공되는 함수형 인터페이스에 기반해서 사용해야 하냐?
위의 내용을 보다보면 "아니 람다 쓰려면 무조건 함수형 인터페이스를 써야하나?"
라는 생각이 들수도있다.

하지만 함수형 인터페이스는 우리가 정의할 수도 있는데 바로 ```@FunctionalInterface```을 사용하는 방법이다.

```javascript
@FunctionalInterface
interface MyLambdaFunction {
    int multiply(int a, int b);
}

public static void main(String[] args) {
    MyLambdaFunction myLambdaFunction = (int a, int b) 
        -> Math.multiplyExact(a, b);
    
    System.out.println(myLambdaFunction.multiply(10, 30));
}
```

이런 식으로 하나의 추상 메서드를 지정하는 메서드를 만들어서 ```@FunctionalInterface```로 지정해주면
```사용자가 정의한 함수형 인터페이스```가 되는 것이다.

***

## 길이좀 줄이자;
람다식을 사용하다 보면 코드가 약간 길어질 수 있다.

```javascript
Function<String, Integer> function = (str) -> str.length();
```
위와 같이 매개변수를 던져주고 그 길이를 반환하는 람다식이다.
하지만 **::**를 사용하면 메서드의 길이를 줄일 수 있다.

```javascript
Function<String, Integer> funciton = String::length;
```

같은 역할을 하는 메서드인데 더 짧게 만들어졌다.

하지만 무작정 메서드 참조 단축 표현을 사용한다면 
오히려 그 길이가 더 길어질 수 있는데, 다음과 같은 상황이다.

```javascript
int length1 = "abcd".length();

Function<String, Integer> shortFunction2 = String::length;
Integer length2 = shortFunction2.apply("abcd");
```

단순히 문자열 "abcd"의 길이를 구하는 메서드이지만 굳이
함수형 인터페이스까지 쓰면서 메서드 단축 표현을 사용하면 코드가 훨씬 길어지는 사태가 발생할 수 있다.

결론은 람다식을 사용하면 메서드의 길이가 길어질 수 있고, 이는 **::** 로 줄일 수 있다.

하지만 굳이 사용하지 않아도 되는 곳에서 무작정 쓰려고하면 오히려 코드가
길어지는 상황이 발생할 수 있으니 생각해보고 사용하자

***
## 마지막 문제
![](../../../../../../var/folders/ms/14322fys69xdtw3zrnlz5wd80000gn/T/TemporaryItems/NSIRD_screencaptureui_Oa7TtR/스크린샷 2022-06-22 오후 1.52.41.png)