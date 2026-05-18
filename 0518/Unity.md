# 파라미터

### 가변형

```
using UnityEngine;

namespace Method
{
    // [4] 가변형 전달 방법 (params int[] numbers)
    public class ParameterParam : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            Debug.Log(sumAll(3, 5));
            Debug.Log(sumAll(3, 5, 7));
            Debug.Log(sumAll(3, 5, 7, 9));
        }

        // 매개변수로 받은 정수들의 합을 구하는 메서드
        // 가변형
        int sumAll(params int[] numbers)
        {
            int sum = 0;
            for(int i = 0; i < numbers.Length; i++)
            {
                sum += numbers[i];
            }
            return sum;
        }
    }
}
```

### 몬스터 공방전

```
using UnityEngine;

namespace Method
{
    // 몬스터 전투를 관리하는 클래스
    public class ParameterNote : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            // 몬스터 생성
            Monster monster1 = new Monster(100, 10);
            Monster.monsterCount++;
            Monster monster2 = new Monster(200, 20);
            Monster.monsterCount++;

            // 생성된 몬스터 숫자
            Debug.Log($"몬스터 수 : {Monster.monsterCount}");

            // 전투
            // 몬스터 1 - atk -> 몬스터 2
            //monster2.TakeDamage(monster1.atk);
            MonsterBattle(monster1 , monster2);

            // 몬스터 2 - atk -> 몬스터 1
            //monster1.TakeDamage(monster2.atk);
            MonsterBattle(monster2 , monster1);

            Debug.Log($"현재 몬스터 1의 체력 : {monster1.hp}, 공격력 : {monster1.atk}");
            Debug.Log($"현재 몬스터 2의 체력 : {monster2.hp}, 공격력 : {monster2.atk}");
        }

        // 몬스터 전투 구현
        // 공격하는 몬스터, 방어하는 몬스터를 매개변수로 입력받아 공방식 적용

        public void MonsterBattle(Monster atkMonster, Monster defMonster)
        {
            defMonster.hp -= atkMonster.atk;
        }
    }
}
```

몬스터 관리 클래스
```
using UnityEngine;

namespace Method
{
    // 몬스터를 관리하는 클래스
    public class Monster
    {
        // 필드, 멤버변수
        // 정적 멤버 변수 : 단 하나만 존재하는 값
        public static int monsterCount; // 게임에서 생성된 몬스터의 수

        public int hp; // 체력
        public int atk; // 공격력

        // 생성자 - 매개변수로 들어온 값으로 hp, atk 초기화
        public Monster(int hp, int atk)
        {
            this.hp = hp;
            this.atk = atk;
        }

        // 데미지 입는 함수
        public void TakeDamage(int dmg)
        {
            hp -= dmg;
        }
    }
}
```

### Property : 속성
> 교수님 너무 빨라요 진짜 좀만 천천히 제발

일단 데모 제작

```
using UnityEngine;

namespace Property
{
    public class PropertyDemo : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            /*// person 클래스의 인스턴스 생성
            Person person = new Person();

            // 메서드 사용
            person.SetName("홍길동");
            Debug.Log($"이름은 {person.GetName()}");

            // property (속성) 사용 - 사용 시 변수와 동일한 방법으로 사용
            person.Name = "백두산";
            Debug.Log($"이름은 {person.Name}");*/

            /* Truck truck1 = new Truck();
             truck1.Name = "덤프트럭";
             Debug.Log(truck1.Name);

             Truck truck2 = new Truck();
             truck2.Name = "카고트럭";
             truck2.Color = "Red";
             truck2.Number = 9876;
             Debug.Log($"이름 : {truck2.Name}, 색 : {truck2.Color}, 번호 : {truck2.Number}");*/

            /*// User 클래스의 인스턴스 생성
            User user = new User("홍길동");
            user.BirthYear = 2000;
            Debug.Log($"이름 : {user.Name}, 나이 : {user.Age} ");*/

            // 속성 초기화
            // Student 클래스의 인스턴스 생성
            Student s1 = new Student();
            s1.Name = "홍길동";
            s1.Age = 20;
            Debug.Log($"이름 : {s1.Name}, 나이 : {s1.Age}, 번호 : {s1.Number}");

            // 개체 이니셜 라이져를 사용하여 개체 초기화
            Student s2 = new Student() { Name = "백두산", Age = 25, Number = 2 };
            // 주소는 함수를 이용하여 쓴다.
            s2.SetAddress("서울시");
            Debug.Log($"이름 : {s2.Name}, 나이 : {s2.Age}, 번호 : {s2.Number}, 주소 : {s2.GetAddress()}");
        }
    }
}

/*
 
Property(속성) : 필드의 값을 읽거나 쓰거나 연산하는 방법을 제공하는 클래스 멤버
: 필드는 기본적으로 private (외부에서 접근 제한)
: 속성은 제한된 외부에서 읽거나 쓰기가 가능하도록 해줌.
: 변수와 동일한 방법으로 사용

네이밍 : 속성이름은 첫 문자를 대문자로 쓺.

Property 형식
public [반환 타입] 속성이름
{
    get;
    get;
}
 
ex)
        public string Name
        {
            get { return name; } : 필드값 반환

            person.Name = "백두산";
            set { name = value; } : value 값을 필드에 저장
        }

*/
```

Person.cs
```
using UnityEngine;

namespace Property
{
    // 사람을 관리하는 클래스
    public class Person
    {
        // 필드
        private string name;    // 사람 이름

        // 속성
        // public한 property를 이용하여 private한 name을 외부에서 읽고 쓰기 구현
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        // 메서드
        // public 한 메서드를 이용, private한 name 을 외부에서 읽고 쓰기 구현

        public string GetName()
        {
            return name;
        }

        public void SetName(string newName)
        {
            name= newName;
        }
    }
}
```

Truck.cs
```
using UnityEngine;

namespace Property
{
    // 트럭을 관리하는 클래스
    // 이름, 색상, 번호 데이터 관리
    public class Truck
    {
        // 필드
        private string name;

        // [1] 전체 속성 : 필드를 읽고 쓰는 속성
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        // [2] 자동 속성 : 필드가 없는 속성
        public string Color { get; set; }

        // [3] 자동 속성 선언과 동시에 초기화
        public int Number { get; set; } = 1234;
    }
}
```

User.cs
```
using UnityEngine;

namespace Property
{
    // 유저정보를 관리하는 클래스
    public class User
    {
        // 필드
        private int birthYear; // 생년

        // 자동 속성
        public string Name { get; set; }

        // 읽기 전용 속성 : 외부에서 set으로 접근 불가, 내부에선 접근 가능
        public string Messege { get; private set; } = "읽기 전용 속성";

        // 쓰기 전용 속성 : 식
        public int BirthYear
        {
            set 
            {
                // 입력값 검증식 넣기
                if (value >= 1900)
                {
                    { birthYear = value; }
                }
                else
                {
                    birthYear = 0;
                }
            }
        }

        // 나이를 반환하는 읽기 전용 속성
        public int Age
        {
            get
            {
                // 계산식 결과 반환하기
                return (System.DateTime.Now.Year - birthYear);
            }
        }

        // 생성자 - 매개변수 받아서 속성 초기화
        public User(string name)
        {
            Name = name;
        }
    }
}
```

Student.cs
```
using UnityEngine;

namespace Property
{
    // 학생 정보를 관리하는 클래스
    public class Student
    {
        // 필드
        private string name;
        private string address;

        // 속성
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        // 자동 속성
        public int Age { get; set; }
        public int Number {  get; set; } = 1;

        // 함수
        public string GetAddress()
        {
            return address;
        }
        public void SetAddress(string value)
        {
            address = value;
        }
    }
}
```

### Indexer : 인덱서

```
using UnityEngine;

namespace Indexer
{
    public class IndexerDemo : MonoBehaviour
    {
        // Start is called once before the first execution of Update after the MonoBehaviour is created
        void Start()
        {
            /* // Catalog클래스의 인스턴스 생성
             Catalog ca = new Catalog();

             Debug.Log(ca[0]);
             Debug.Log(ca[1]);
             Debug.Log(ca[2]);
             Debug.Log(ca[3]);
             Debug.Log(ca[4]);
             Debug.Log(ca[5]);*/


            // Car 클래스의 인스턴스 생성
            Car cars = new Car(3);

            cars[0] = "아반떼";
            cars[1] = "그랜져";
            cars[2] = "소나타";

            /*// 인덱서 사용
            for (int i = 0; i < cars.Length; i++)
            {
                Debug.Log(cars[i]);
            }*/
            foreach (var car in cars)
            {
                Debug.Log(car);
            }
        }
    }
}

/*
 
Indexer(인덱서) : 클래스의 인스턴스(객체)를 배열처럼 []을 사용할 수 있도록 해주는 구문
인스턴스[0], 인스턴스[1], 인스턴스[2]
클래스에 있는 필드(배열, 컬렉션)의 값을 인덱서를 이용하여 사용(쓰기, 읽기)이 가능하게 해주는 구문

인덱서 형식

Class Car
Car cars = new Car(3);
cars[0] = "a";
cars[1] = "b";
cars[2] = "c";
 
*/
```

Catalog.cs
```
using UnityEngine;

namespace Indexer
{
    // 인덱서 예제
    public class Catalog
    {
        // 인덱스 값을 입력받아 짝수, 홀수 판별하여 리턴해주는 인덱서

        public string this[int index]
        {
            get
            {
                return (index % 2 == 0) ? $"{index}는 짝수" : $"{index}는 홀수";
            }
        }
    }
}

```

Car.cs
```
using UnityEngine;
using System.Collections;

namespace Indexer
{
    // 인덱서 예제
    public class Car
    {
        // 필드
        private string[] names;

        // 속성
        public int Length
        {
            get {  return names.Length; }
        }

        // 생성자 - 매개변수로 길이를 입력받아 요소수 생성
        public Car(int length)
        {
            names = new string[length];
        }

        // 인덱서
        public string this[int index]
        {
            get { return names[index]; }
            set { names[index] = value; }
        }

        // 반복기 - 인덱서를 foreach문에서 사용하기위해 정의
        public IEnumerator GetEnumerator()
        {
            for (int i = 0; i < names.Length; i++)
            {
                yield return names[i];
            }
        }
    }
}
```
