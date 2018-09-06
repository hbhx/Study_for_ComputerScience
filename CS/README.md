# 개발 상식
- 객체 지향 프로그래밍이란 무엇인가?
- 함수형 프로그래밍이란?

<br><br>

# 객체 지향 프로그래밍이란 무엇인가?

**OOP(Object Oriented Programming)**
- 추상화 (Abstraction)
  - 공통의 속성이나 기능을 묶어 이름을 붙이는 것
  - OOP 관점에서 클래스를 정의하는 것
  - 물고기, 사자, 토끼 뱀 등의 객체를 하나의 동물이라는 객체로 정의함
- 캡슐화 (Encapsulation)
  - 데이터 구조와 데이터를 다루는 방법을 결합시켜 묶는 것
  - 즉, 변수와 함수를 묶는 것을 말함
  - 객체가 맡은 역할을 수행하기 위한 하나의 목적을 한데 묶는다고 생각
  - 외부에서을 직접 접근을 막고 오로지 객체의 함수를 통해서만 접근하도록함
- 재사용 (Inheritance)
  - 상위 개념의 특징을 하위 개념이 물려받는 것
  - 부모클래스의 변수, 메소드 등을 자식클래스가 상속받아 사용
- 다형성 (Polymorphism)
  - 부모클래스에서 물려받은 가상 함수를 자식 클래스 내에서 오버라이딩(Overriding) 되어 사용하는 것


<br><br>


# 함수형 프로그래밍이란?

![FM](../assets/images/FP.png)

**함수형 프로그래밍(Functional Programming)이란?**

> Avoids changing State and Mutable data

- 상태와 Data를 변경하는 것을 피하면서 프로그래밍 하는 것
- 즉, 대입문(Assignment Statements)없이 프로그래밍 하는 것


<br>

**순수 함수란?**

- 같은 입력이 주어지면 항상 같은 출력을 반환한다
- 부작용이 없음

~~~javascript
var z = 10;
function add(x,y){
  return x+y;
}
~~~

- 만약 add() 함수가 변수 z를 사용한다면 더이상 순수함수가 아니다

<br>

**FP(Function Programming)의 특징**

- 불변성(Immutability)
- First-class, higher-order functions
- Lazy Evaluation

**불변성(Immutability)**
- FP는 변경 가능한 상태를 최대한 제거하려고 노력한 프로그래밍
- 함수 내부에 상태가 존재하지 않으며, 함수의 출력은 항상 함수의 입력 값의 영향만 받음

**First-class, higher-order functions**

> 함수형 프로그래밍에서 함수는 일등 시민(first-class citizen) 이다

- 함수가 Argument로 전달될 수 있다
- Return값이 함수가 될 수 있다
- 함수를 값처럼 할당하기도, 수정도 할 수 있다

**Lazy Evaluation**

> 📛 지연 연산(Lazy Evaluation)<br>
\- 어떤 값이 실제로 쓰이기 전까지 그 값의 계산을 최대한 미루는 것<br>
\- 값을 미리 계산하여 저장하지 않기 때문에 공간을 절약할 수 있고, 그렇기 때문에 프로그램의 성능도 좋아진다

- FP에서는 지연 연산을 지원한다
