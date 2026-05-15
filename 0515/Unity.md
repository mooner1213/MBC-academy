# 생성자와 소멸자

```
using UnityEngine;

namespace Constructor
{
    public class ConstructorDemo : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            // Student 클래스의(생성자를 호출하여) 객체(인스턴스)를 생성
            // Student student = new Student();

            // Dog 클래스의 객체(인스턴스)를 생성
            // 매개변수가 있는 생성자를 이용하여 객체 생성
            /* Dog happy = new Dog("해피");
             Debug.Log($"강아지 이름 : {happy.GetName()}");

             // Dog 클래스의 다른 객체(인스턴스)를 생성
             Dog worry = new Dog("워리");
             Debug.Log($"강아지 이름 : {worry.GetName()}");*/

            // User 클래스의 객체(인스턴스) 생성
            // [1] 기본생성자 호출
            User user1 = new User();
            user1.ShowUserInfo();

            // [2] 매개변수가 있는 생성자 호출
            User user2 = new User("백두산");
            user2.ShowUserInfo();

            User user3 = new User("장길산", 25);
            user3.ShowUserInfo();
        }
    }
}


/*
 
 Constructor(생성자) : 클래스가 사용될 때 제일 먼저 호출되는 메서드
: 객체를 생성할 때 호출된다.
: 클래스의 필드의 기본값을 설정하는 역할(필드 초기화), 인스턴스(객체) 초기화

Constructor(생성자) 형식 - 메서드 
- 클래스 이름과 동일한 이름으로 함수 이름을 사용
- 접근제한자는 public 을 사용한다.
- 반환값도 없으며, void 도 없다.

- 생성자를 만들지 않으면, 닷넷에서 기본 생성자를 자동으로 만들어준다.
// 기본 생성자
    public Dog()
    {
        
    }
- 모든 필드는 기본값으로 초기화 된다. : 값형 - 0(zero), 참조형 - null, 

class Dog(클래스이름)
{
    // 생성자
    public Dog()
    {
        
    }
}
 
 */
```

student 클래스
```
using UnityEngine;

namespace Constructor
{
    public class Student
    {
        // 생성자
        public Student()
        {
            Debug.Log("Student 객체(인스턴스)가 생성되었습니다.");
        }
    }
}
```

dog 클래스
```
using UnityEngine;

namespace Constructor
{
    // 강아지를 관리하는 클래스
    public class Dog
    {
        // [1] 필드
        private string name;    // 이름

        // [2] 생성자 - 필드 초기값 설정
        // 매개변수로 문자열을 받아서 name 값에 대입
        // 생성자 호출 시 강아지 이름을 만들어 준다.
        public Dog(string str)
        {
            name = str;
        }

        // [3] 메서드 - 강아지 이름을 반환하는 함수
        public string GetName()
        {
            return name;
        }
    }
}
```

User 클래스
```
using UnityEngine;

namespace Constructor
{
    // 유저를 관리하는 클래스
    public class User
    {
        // [1] 필드
        private string name;
        private int age;

        // [2] 생성자 - 매개변수 X (기본 생성자)
        public User()
        {
            name = "홍길동";
            age = 20;
        }

        // [3-1] 생성자 - 매개변수가 있는 생성자
        /*public User(string _name)
        {
            name = _name;
            age = 20;
        }*/

        // [3-2] 생성자 - 매개변수가 있는 생성자
        public User(string name, int age = 20)
        {
            this.name = name;
            this.age = age;
        }
        
        // [4] 이름을 반환하는 함수
        public string GetName()
        {
            return name;
        }

        // [5] 유저 정보를 출력하는 함수
        public void ShowUserInfo()
        {
            Debug.Log($"이름은 {name}, 나이는 {age}");
        }
    }
}
```

### 소멸자

```
using UnityEngine;

namespace Constructor
{
    public class DestructorDemo : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            // 소멸자 테스트
            // DestructorTest클래스의 인스턴스 생성

            DestructorTest destructorTest = new DestructorTest();
            // 인스턴스 사용
            destructorTest.Run();

            // 소멸자 호출 - 가비지 켈렉터(GC)가 대신 해준다.
            // ~DestructorTest();

            // Car 클래스의 인슽언스 생성
            // 하얀차, 파란차, 빨간차 만들기

            Car whiteCar = new Car();
            whiteCar.Run();

            Car blueCar = new Car("파랑");
            blueCar.Run();

            Car redCar = new Car("빨간");
            redCar.Run();

            // 폐차는 GC가 알아서 함.
        }
    }
}

/*
 
Destructor(소멸자) : 클래스가 사용된 후 가장 마지막에 호출되는 메서드
: 생성된 객체(인스턴스)가 메모리상에서 없어질 떄 호출
: 클래스에서 사용되는 메모리 해제 등

c# 메모리 해제 : 가비지 컬렉터(GC)가 알아서 함
 
 class Dog(클래스이름)
{
    // 생성자
    public Dog()
    {
        
    }

    // 소멸자
    ~Dog()
    {
        // 개체가 소멸할 때 필요한 기능 수행
    }

}
 
 */
```

dog 클래스
```
using UnityEngine;

namespace Method
{
    // 강아지를 관리하는 클래스
    public class Dog
    {
        // [1] 필드
        public int weight = 20; // 인스턴스 멤버 변수
        public static int point = 10;   // 정적 멤버 변수

        // [2] 인스턴스 메서드 : public
        public void Eat()
        {
            Debug.Log("[1] 밥을 먹는다.");

            Digest();
        }

        // [3] 정적 메서드
        public static void Drink()
        {
            Debug.Log("[2] 물을 마신다.");
        }

        // [4] 인스턴스 메서드 : private
        private void Digest()
        {
            Debug.Log("[4] 소화 시킨다.");
        }
    }
}
```

Car 클래스
```
using UnityEngine;

namespace Constructor
{
    // 자동차를 관리하는 클래스
    public class Car
    {
        // 필드
        private string color;

        // 기본 생성자

        public Car()
        {
            color = "하양";
            Debug.Log($"자동차의 색깔 : {color}");
        }

        // 매개변수가 있는 생성자
        public Car(string color)
        {
            this.color = color;
            Debug.Log($"자동차의 색깔 : {this.color}");
        }

        // 메서드
        public void Run()
        {
            Debug.Log($"자동차의 색깔 : {this.color}");
        }

        // 소멸자

        ~Car()
        {
            Debug.Log($"{this.color}색 자동차를 폐기합니다.");
        }
    }
}
```

### 메서드

```
using UnityEngine;

namespace Method
{
    public class MethodDemo : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            // Dog 클래스의 인스턴스 생성
            Dog dog = new Dog();

            dog.Eat();          // public 인스턴스 메서드
            // dog.Digest();    // error, private 인스턴스 메서드

            // dog.Drink();     // error, 정적 메서드, 인스턴스 이름으로 호출 불가
            Dog.Drink();        // 클래스 이름.메서드() 호출
        }
    }
}

/*
 
method(메서드, 함수, function)
: 클래스가 수행하는 기능을 하나의 이름으로 묶어서 관리하는 코드블록
: 클래스의 기능 구현

= 메서드 네이밍
: 동사 + 명사
: GetName, SetName, GetHp

[1] 메서드 구성요소

public(private) static(x) void(반환값, int, string, bool, object) 메서드 이름(매개변수
{
    // 실행 명령문들
}

 */
```

### 파라미터
```
using UnityEngine;

public class ParameterIn : MonoBehaviour
{
    // [1] 값 전달 방법
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int num = 10;
        Debug.Log($"[1] : {num}");  // [1] : 10

        PrintNumber(num);

        Debug.Log($"[3] : {num}");  // [3] : 10

    }

    // 매개변수로 전달된 정수 값을 출력하는 함수
    private void PrintNumber(int num)
    {
        num = 20;
        Debug.Log($"[2] : {num}");        // [2] : 20
    }

}

/*

Parameter(매개변수) : 연산에 필요한 데이터를 함수 호출 시, 전달해준다.
= 매개변수 전달 방법 분류

[1] 값 전달 방법 : (int num)
[2] 참조 전달 방법 : (ref int num)
[3] 반환형 전달 방법 : (out int num)

[4] 가변형 전달 방법 : (params int[] numbers)
 
*/
```
참조 전달 방법
```
using UnityEngine;

namespace Method
{
    // [2] 참조 전달 방법 : (ref int num)
    public class ParameterRef : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            int num = 10;
            Debug.Log($"[1] : {num}");        // [1] : 10

            // 참조 전달 형식 메서드 호출
            PrintNumber(ref num);

            Debug.Log($"[3] : {num}");        // [3] : 20
        }

        // 매개변수로 참조 전달된 정수값을 출력하는 함수
        private void PrintNumber(ref int num)
        {
            num = 20;
            Debug.Log($"[2] : {num}");        // [2] : 20
        }
    }
}
```
반환형 전달방식
```
using UnityEngine;

namespace Method
{
    public class ParameterOut : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            // 정수형 변수 선언, 초기화 x
            int num;    // 반환형 전달방식의 매개변수로 사용되는 변수는 반드시 초기화 할 필요가 없음.

            // 반환형 전달 방식 메서드 호출
            PrintNumber(out num);

            Debug.Log($"[3] : {num}");        // [3] : 20
        }

        // 매개변수로 반환형으로 전달된 정수값을 출력하는 함수
        // 메모리 동작 방식은 ref와 동일하다.
        // 반환형 전달 방식에서 사용되는 매개변수는 반드시 함수 내부에서 초기화(값)을 저장해야함.
        private void PrintNumber(out int num)
        {
            num = 20;   // out일 경우 초기화 필수
            Debug.Log($"[2] : {num}");        // [2] : 20
        }
    }
}
```

매서드 축약형
```
using UnityEngine;

namespace Method
{
    // 매서드 축약형
    public class MethodExpression : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            Work();
            Hello();
            Debug.Log(DoubleValue(4));
            Debug.Log(Plus(5,8));
        }

        // [1] 매서드 - 기본형식
        void Work()
        {
            Debug.Log("Work 실행");
        }

        // [1] 메서드 축약형 - 실행 명령문 1줄
        void Hello() => Debug.Log("Hello");

        // 매개변수로 입력받은 정수 값을 두배로 반환하는 함수
        int DoubleValue(int value) => value * 2;

        // 매개변수로 입력받은 두 정수의 합을 반환하는 함수
        int Plus(int a, int b) => a + b;
    }
}
```
