# 다형성
> 인터페이스와 이어짐

하나의 객체가 여러개의 자료형 타입을 가질 수 있는 것
```
경비원은 동물을 짖게 하여 건물을 지킨다.
```
*Bouncer.java*
```java
public class Bouncer {
  public void barkAnimal(Animal animal) {
    if (animal instanceof Tiger) {
      System.out.println("어흥");
    } else if (animal instanceof Lion) {
      System.out.println("으르렁");
    }
  }

  public static void main(String[] args) {
    Tiger tiger = new Timger();
    Lion lion = new Lion();

    Bouncer bouncer = new Bouncer();
    bouncer.barkAnimal(tiger);
    bouncer.barkAnimal(lion);
  }
}
```
> `instanceof`는 특정 객체가 특정 클래스의 객체인지를 조사할 때 사용되는 자바 내장 키워드.
`animal instanceof Tiger` == "animal 객체가 `new Tiger`로 만들어진 객체인가?"

barkAnimal 메소드는 동물이 추가될 때마다 수정되어야 한다.
```java
public void barkAnimal(Animal animal) {
  if (animal instanceof Tiger) {
    System.out.println("어흥");
  } else if (animal instanceof Lion) {
    System.out.println("으르렁");
  } else if (animal instanceof Crocodile) {
    System.out.println("쩝쩝");
  } else if (animal instanceof Leopard) {
    System.out.println("캬옹");
  }
}
```
NO!!!! 인터페이스를 배웠으므로 바꾸자.  

*Barkable.java*
```java
public interface Barkable {
  public void bark();
}
```
*Tiger.java*
```java
public class Tiger extends Animal implements Predator, Barkable {
  public String getFood() {
    return "apple";
  }

  public void bark() {
    System.out.println("어흥");
  }
}
```
*Lion.java*
```java
public class Lion extends Animal implements Predator, Barkable {
  public String getFood() {
    return "banana";
  }

  public void bark() {
    System.out.println("으르렁");
  }
}
```
*Bouncer.java* 의 `barkAnimal`메소드
```java
public void barkAnimal(Barkable animal) {
  animal.bark();
}
```
**getFood 메소드와 bark 메소드를 모두 사용하고 싶다면?**
1. Tiger로 선언된 tiger 객체 이용
2. getFood, bark 메소드를 포함하는 새로운 인퍼테이스 만들어서 사용

*BarkablePredator.java*
```java
public interface BarkablePredator extends Predator, Barkable {}
```
Lion 클래스를 BarkablePredator 인터페이스 구현하도록 수정해 보자.  

*Lion.java*
```java
public class Lion extends Animal implements BarkablePredator {
  public String getFood() {
    return "banana";
  }

  public void bark() {
    System.out.println("으르렁");
  }
}
```
## refer
[점프 투 자바 > 05-7.다형성](https://wikidocs.net/269)
> 인터페이스에다 상속의 연속 ㅠㅡㅠ 역시 나는 아직 초보인가보다....ㅎㅎ 내가 이렇게 객체지향적으로 생각할 수 있을 때까지 연습하자 ~~!
