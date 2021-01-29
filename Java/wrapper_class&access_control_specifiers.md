# Wrapper class | 접근 제어 지시자

## 📌 Wrapper class

기본 자료형(Primitive data type)에 대한 클래스 표현을 Wrapper class 라고 한다. `Integer`, `Float`, `Boolean` 등이 Wrapper class 의 예이다. int 를 Integer 라는 객체로 감싸서 저장해야 하는 이유가 있을까? 일단 컬렉션에서 제네릭을 사용하기 위해서는 Wrapper class 를 사용해줘야 한다. 또한 `null` 값을 반환해야만 하는 경우에는 return type 을 Wrapper class 로 지정하여 `null`을 반환하도록 할 수 있다. 하지만 이러한 상황을 제외하고 일반적인 상황에서 Wrapper class 를 사용해야 하는 이유는 객체지향적인 프로그래밍을 위한 프로그래밍이 아니고서야 없다. 일단 해당 값을 비교할 때, Primitive data type 인 경우에는 `==`로 바로 비교해줄 수 있다. 하지만 Wrapper class 인 경우에는 `.intValue()` 메소드를 통해 해당 Wrapper class 의 값을 가져와 비교해줘야 한다.

### AutoBoxing

JDK 1.5 부터는 `AutoBoxing`과 `AutoUnBoxing`을 제공한다. 이 기능은 각 Wrapper class 에 상응하는 Primitive data type 일 경우에만 가능하다.

```java
List<Integer> lists = new ArrayList<>();
lists.add(1);
```

우린 `Integer`라는 Wrapper class 로 설정한 collection 에 데이터를 add 할 때 Integer 객체로 감싸서 넣지 않는다. 자바 내부에서 `AutoBoxing`해주기 때문이다.

기본 자료형을 객체 타입의 자료형으로 변환이 필요할 때 주로 사용한다.

- 사용 용도
  - 객체로 저장해야 할 경우
  - 매개변수로 객체가 요구될 경우(ex. 제네릭, Collection의 타입)
  - 객체 간의 비교가 필요할 경우
  - 제네릭이나 컬렉션에서 사용할 경우, 기본형을 쓸 수 없기 때문에 이를 Wrapping한 형태를 사용해야 한다.
- 특징
  - 산술 연산을 위한 클래스가 아니기 때문에 `Immutable`하다.(불변)
  - 불변 객체이기 때문에 값에 대한 변경은 불가능하고 새로운 값(객체)의 할당이나 참조만 가능하다.
  - Boxing : 기본 자료형 -> Wrapper Class
  - UnBoxing : Wrapper Class -> 기본 자료형
  - JDK 1.5부터 오토 박싱, 오토 언박싱을 지원한다.
  - 언박싱 시 사용되는 메소드는 다음과 같은 형태를 갖는다.
    - intValue : 객체 -> int 값으로 변환.

문자를 숫자로 바꾸거나, 숫자를 문자를 바꿀 때 두 가지 방식의 차이점이 존재한다.

[Code]

```java
// 문자열 -> 기본형
int number1 = Integer.parseInt("100");

// 문자열 -> wrapper class
Integer number2 = Integer.valueOf("100");
```

위에서 언급했듯이, JDK 1.5부터 오토 박싱과 오토 언박싱이 지원되기 때문에 반환값이 기본형이든, wrapper class이든 차이가 없어졌다. 그래서 굳이 구별하지 않고 `valueOf()`를 사용해도 된다.

단, 성능을 비교하면 valueOf()가 조금 더 느리다고 한다.

## 📌 접근 제어 지시자

자바에서 기본적인 부분이지만, 실제로 사용할 때 의미를 파악하지 않고 남발하는 경우가 많아 정리하려 한다.

- public : public으로 선언된 멤버는 어떤 클래스에서라도 접근이 가능하다. public 메소드는 private 멤버와 프로그램 사이의 인터페이스 역할을 수행하기도 한다.
- protected : protected 멤버를 포함하는 클래스가 정의되어 있는 해당 패키지 내 그리고 해당 클래스를 상속 받은 외부 패키지의 자식 클래스에서 접근이 가능하다.
- private : private으로 선언된 멤버는 해당 멤버를 선언한 클래스에서만 접근이 가능하다. public 메소드를 이용한다면 해당 객체의 private 한 멤버에 접근이 가능하다.
- Default(package private) : 같은 클래스의 멤버와 해당 클래스가 정의되어 있는 패키지 내에서만 접근이 가능하다.

### 참고

1. private의 경우

Private 멤버나 메소드를 가지고 있는 클래스를 A라고 하자.

그리고 B라는 클래스가 A를 상속받는다. 이 경우, B 클래스는 private으로 선언된 멤버 혹은 메소드에 접근할 수 없다.

따라서 상속을 받더라도 private한 멤버에는 접근이 불가능 하다.

대신, public 메소드 통해 getter를 만들면 private 멤버를 사용할 수 있다.

1. protected의 경우

Protected 멤버나 메소드를 가지고 있는 클래스를 A라고 하자.

마찬가지로 B라는 클래스가 A를 상속받는다. 이 경우, B 클래스는 protected로 선언된 멤버 혹은 메소드에 접근이 가능하다. B 라는 클래스가 다른 패키지에 선언되었을지라도 A 클래스의 멤버에 접근이 가능하다.

하지만, 다른 패키지의 A 클래스를 상속받지 않은 클래스는 A 클래스의 멤버에 접근할 수 없다. 마치 private 처럼 말이다.

| 지시자    | 클래스 내부 | 동일 패키지 | 상속받은 클래스 | 이외의 영역 |
| --------- | ----------- | ----------- | --------------- | ----------- |
| private   | ●           | X           | X               | X           |
| default   | ●           | ●           | X               | X           |
| protected | ●           | ●           | ●               | X           |
| public    | ●           | ●           | ●               | ●           |



 



출처: https://rank01.tistory.com/41 [JAVA FOR JAVA]