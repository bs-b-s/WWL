[모던 자바 인 액션 - YES24 www.yes24.com](http://www.yes24.com/Product/Goods/77125987)

---

## **👉🏾 스트림이란 무엇인가?** 

스트림은 자바 8 API에 새로 추가된 기능. 선언형(즉, 데이터를 처리하는 임시 구현 코드 대신 질의로 표현할 수 있다)으로 컬렉션 데이터를 처리할 수 있다. 멀티스레드 코드를 구현하지 않아도 데이터를 투명하게 병렬로 처리할 수 있다. _간단하게 이야기해서 컬렉션 반복을 멋지게 처리하는 기능_

## 👉🏾 스트림 유무에 따른 코드 차이 💻

저칼로리의 요리명을 반환하고 칼로리순으로 정렬하는 코드를 스트림 없이 기존의 방법으로, 스트림으로 각각 구현해보겠다. 비교해보자.

**👇🏾 스트림이 없는 기존의 방법으로**

```
List<Dish> lowCaloricDishes = new ArrayList<>();

for ( Dish dish : menu ) {
   if (dish.getCalories() < 400)
       lowCaloricDishes.add(dish);
}
  
Collections.sort(lowCaloricDishes, new Comparator<Dish>() {
    @Override
    public int compare(Dish dish1, Dish dish2) {
        return Integer.compare(dish1.getCalories(), dish2.getCalories());
    }
});

List<String> lowCaloricDishesName = new ArrayList<>();

for(Dish dish : lowCaloricDishes) {
   lowCaloricDishesName.add(dish.getName());
}
```

**👇🏾 스트림으로**

```
List<String> lowCaloricDishesName = menu.stream()
            .filter(d -> d.getCalories() < 400)
            .sorted(Comparator.comparing(Dish::getCalories))
            .map(Dish::getName)
            .collect(Collectors.toList());
```
![](https://velog.velcdn.com/images/leekyukin/post/e4860113-6ed4-41c0-8fff-2f21445000b2/image.png)



## **👉🏾 자바 스트림 API의 특징** 

위 두 코드를 보면 확실히 느껴질 것이다.

1\. **선언형** : 더 간결하고 가독성이 좋아진다.

> 즉, 반복문과 조건문 없이 '저칼로리 요리만 선택해라' 같은 수행을 지정할 수 있다.

2. **조립할 수 있음 🧱** : 유연성이 좋아진다.

> 즉, 여러 연산(filter, sorted, map, collect)을 파이프라인으로 연결해도 여전히 가독성과 명확성이 유지된다. 각 연산의 결과를 다음 연산으로 전달한다.

3. **병렬화** : 성능이 좋아진다.

> 즉, 스레드와 락을 걱정할 필요가 없다. (~병렬화는 나중에 자세히 다뤄보겠다~

---

## 👉🏾 **스트림 시작하기 🎬**

> **스트림이란 '데이터 처리 연산을 지원하는 소스에서 추출된 연속된 요소'**

잉 뭐라노? ~~필자는 부산사람입니다 ㅎㅎ~~  완벽한 이해를 위해 정의를 하나씩 뜯어보자.

-   **연속된 요소** : 특정 요소 형식으로 이루어진 연속된 값 집합의 인터페이스를 제공한다.
-   **소스** : 컬렉션, 배열, I/O 자원 등의 데이터 제공 소스로부터 데이터를 소비한다.
-   **데이터 처리 연산** : 함수형 프로그래밍 언어에서 지원하는 연산, DB와 비슷한 연산을 지원한다. (filter, map, find, match, sort 등) 스트림 연산은 순차적 또는 병렬적으로 실행할 수 있다.

## 👉🏾 **스트림의 중요한 특징 두가지 ✌🏿**

-   **파이프라이닝** : 스트림 연산은 스트림 연산끼리 연결해서 커다란 파이프라인을 구성할 수 있도록 스트림 자신을 반환한다. 덕분에 게으름, 쇼트서킷 같은 최적화도 얻을 수 있다. (~~이는 후에 자세히 다루도록 하겠다~~) 연산 파이프라인은 데이터 소스에 적용하는 DB 질의와 비슷하다.

![](https://velog.velcdn.com/images/leekyukin/post/8c01445b-e6c4-46dd-b1d8-9fa57bd66c2a/image.png)


-   **내부 반복** : 반복문으로 반복하는 컬렉션과 달리 스트림은 내부 반복을 지원한다.

## 👉🏾 **예제로 확인하기 💻**

**앞으로 스트림 예제에 쓰일 class 👇🏾**

```
public class Dish {
    private final String name;
    private final boolean vegetarian;
    private final int calories;
    private final Type type;

    public Dish(String name, boolean vegetarian, int calories, Type type) {
        this.name = name;
        this.vegetarian = vegetarian;
        this.calories = calories;
        this.type = type;
    }
    public String getName() {
        return name;
    }

    public boolean isVegetarian() {
        return vegetarian;
    }

    public int getCalories() {
        return calories;
    }

    public Type getType() {
        return type;
    }

    @Override
    public String toString() {
        return "Dish{" +
                "name='" + name + '\'' +
                '}';
    }

    public enum Type { MEAT, FISH, OTHER };

    // 예시 데이터들
    static List<Dish> getDishes() {
        return Arrays.asList(
                new Dish("pork", false, 800, Dish.Type.MEAT),
                new Dish("beef", false, 700, Dish.Type.MEAT),
                new Dish("chicken", false, 400, Dish.Type.MEAT),
                new Dish("french fries", true, 530, Type.OTHER),
                new Dish("rice", true, 350, Type.OTHER),
                new Dish("season fruit", true, 120, Dish.Type.OTHER),
                new Dish("pizza", true, 550, Type.OTHER),
                new Dish("prawns", false, 300, Type.FISH),
                new Dish("salmon", false, 450, Type.FISH)
        );
    }
}
```

**스트림 예제 👇🏾**

```
List<Dish> menu = Dish.getDishes();
List<String> threeHighCaloricDishNames = menu.stream()  // 메뉴에서 스트림을 얻음
		.filter(d -> d.getCalories() > 300)	//코칼로리 요리를 필터링한다.
		.map(Dish::getName)			// 요리명 추출
		.limit(3)				// 선착순 세 개만 선택
		.collect(Collectors.toList());		// 결과를 다른 리스트로 저장
        
System.out.println(threeHighCaloricDishNames);		// 결과 : [pork, beef, chicken]
```

-   **데이터 소스** : menu (요리 리스트)
-   **연속된 요소** : 데이터 소스는 연속된 요소를 스트림에 제공한다.
-   **데이터 처리 연산** (~~자세한 내용은 추후에 다루도록 하겠다~~)
    -   **filter** : 람다를 인수로 받아 스트림에서 특정 요소를 제외시킨다.
    -   **map** : 람다로 한 요소를 다른 요소로 변환하거나 정보를 추출한다.
    -   **limit** : 정해진 개수 이상의 요소가 스트림에 저장되지 못하게 스트림 크기를 자른다.
    -   **collect** : 스트림을 다른 형식으로 변환한다. (예제에서는 리스트로 변환함)
-   **파이프라인** : collect 제외 모든 연산은 파이프라인 형성을 위해 스트림을 반환한다.