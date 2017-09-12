# 인터페이스
```
난 동물원의 사육사이다.
육식동물이 들어오면 난 먹이를 던져준다.
호랑이가 오면 사과를 던져준다.
사자가 오면 바나나를 던져준다.
```
- 동물마다 먹이 메소드를 추가하는건 너무 번거롭다.
- 인터페이스 == 규칙!
- 추후 어떤 동물이 추가되어도 `implements`하면 된다.  

*Animal.java*
```java
public class Animal {
  String name;
  public void setName(String name) {
    this.name = name;
  }
}
```
*Tiger.java*
```java
public class Tiger extends Animal implements Predator {
  public String getFood() {
    return "apple";
  }
}
```
*Lion.java*
```java
public class Lion extends Animal implements Predator {
  public String getFood() {
    return "banana";
  }
}
```
*ZooKeeper.java*
```java
public class ZooKeeper {
  public void feed(Predator predator) {
    System.out.println("feed " + predator.getFood());
  }
  public static void main(String[] args) {
    Zookeeper zooKeeper = new ZooKeeper();
    Tiger tiger = new Tiger();
    Lion lion = new Lion();
    zooKeeper.feed(tiger);
    zooKeeper.feed(lion);
  }
}
```
*Predator.java*
```java
public interface Predator {
  public String getFood();
}
```
## 핵심
육식 동물들의 종류만큼의 feed 메소드가 필요했던 ZooKeeper 클래스를 Predator 인터페이스를 이용하여 구현했더니 단 한개의 feed 메소드로 구현이 가능해졌다. 여기서 중요한 점은 메소드의 갯수가 줄어들었다는 점이 아니라 ZooKeeper클래스가 동물들의 종류에 의존적인 클래스에서 동물들의 종류와 상관없는 독립적인 클래스가 되었다는 점이다. 바로 이 점이 인터페이스의 핵심이다.
## refer
[점프 투 자바 > 05-6.인터페이스](https://wikidocs.net/217)
> 인터페이스는 잘 사용할줄 안다면 편해보이는데 내가 구현하고자 하면 어렵다 .. 얼마 전에 유지보수 하면서 switch던가 if문 써서 경우의 수 죄다 나눠놨던 프로젝트 생각나네 ㅎㅎㅎ... 이렇게 인터페이스로 바꿔 보아야 겠다. 문제만 보고 구현할 수 있도록 연습하자 ~~~~!
