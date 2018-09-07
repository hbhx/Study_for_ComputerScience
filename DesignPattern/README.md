# Design Pattern
- Singleton Pattern

# 싱글톤 패턴(Singleton Pattern)

> 애플리케이션이 시작될 때, 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴

- 즉, 단  하나의 인스턴스를 생성해 사용하는 디자인패턴을 말한다
- 주로 공통된 객체를 여러개 생성해서 사용하는 DBCP(DataBase Connection Pool)에서 사용한다

~~~java
public class Singleton {
  private static Singleton singleton = null;

  private Singleton(){
    System.out.println("최초의 인스턴스 생성!");
  }

  // singleton 인스턴스가 이미 생성되어 있는지 검사
  // 만약 인스턴스가 없다면 생성자를 호출해 인스턴스 생성
  // 만약 인스턴스가 이미 있다면 기존 singleton 인스턴스 반환
  public static Singleton getInstance(){
    if(singleton == null){
      singleton = new Singleton();
    }
    return singleton;
  }
}
~~~

> 📛 Static : 정적 메서드, 정적 변수 <br><br>
\- 구체적인 인스턴스에 속하는 영역이 아니고 클래스 자체에 속한다는 의미<br>
\- 또한 클래스의 인스턴스가 생성될 때마다 생성되는 것이 아니라 딱 한번만 생성되며 클래스의 인스턴스가 생성되기 전에 초기화 된다<br>
\- 정적 메서드, 정적 변수는 클래스에서 생성된 모든 인스턴스들에게 공유된다<br>
\- 따라서 클래스의 인스턴스를 통하지 않고서도 메서드,변수를 사용할 수 있다