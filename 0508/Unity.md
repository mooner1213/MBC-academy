# 함수 2

### Default Parameter
* 기본 매개변수(선택적 매개변수) : 매개변수를 선언할때 초기화 한것

```
using UnityEngine;

// 기본 매개변수 (DefaultParameter, 선택적 매개변수) : 매개변수를 선언할때 초기화 한것
public class DefaultParameter : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        PrintError("입장 실패.", 4);
        // 기본 매개변수가 있는 함수 사용

        PrintError("입장 실패.") // <- 이렇게만 해도됨
    }

    // 매개변수를 들어온 에러메세지(문자열)와 레벨(정수)을 출력하는 함수
    void PrintError(string message, int Level = 1)
    {
        if (Level < 50)
        { 
        Debug.Log($"Error : {message}, 플레이어의 레벨({Level})이 권장레벨(50)이 아닙니다.");
        }
    }
}
```

### Method Overload

```
using UnityEngine;

// 메서드(함수) 오버로드 : 동일한 이름의 메서드를 매개변수를 달리하여 생성
public class MethodOverload : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 1234 출력
        PrintNumber(1234);
        PrintNumber(12.34F);
        PrintNumber(1234L);

        // 인사하기
        Hi();
        Hi("반갑습니다?");
        Hi("또 만나용", 5);
    }

    // 매개변수로 숫자(여러 타입의 정수, 실수)를 입력받아 출력하는 함수(PrintNumber)
    void PrintNumber(int number)
    {
        Debug.Log($"int32 : {number}");
    }

    void PrintNumber(float number)
    {
        Debug.Log($"실수형F : {number}");
    }
    
    void PrintNumber(long number)
    {
        Debug.Log($"int64 : {number}");
    }

    // 인사하는 함수
    void Hi()
    {
        Debug.Log("안녕하세요.");
    }

    void Hi(string message)
    {
        Debug.Log(message);
    }

    // 매개변수로 인사횟수를 입력받아 count 만큼 인사하기
    void Hi(string message, int count)
    {
        for (int i = 0; i < count; i++)
        {
            Debug.Log(message);
        }
    }
}
```

### 전역변수 지역변수

```
using UnityEngine;

// 변수 : 데이터를 저장해 놓는 그릇
// 전역 변수, 지역 변수 : 변수 선언의 위치에 따라 분류
public class FunctionScope : MonoBehaviour
{
    // FunctionScope 함수 안에서 선언된 변수 : 지역변수
    public string message = "전역 변수 메세지";

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 함수 호출
        ShowMessage(); // 지역변수 메세지

        PrintMessage(); // 전역변수 메세지

        Debug.Log(message); // 전역변수 메세지
    }

    // message를 출력하는 함수
    void ShowMessage()
    {
        string message = "지역 변수 메세지";
        // 전역변수와 지역변수 이름이 같으면 지역변수로 인식
        Debug.Log(message);

        // 전역변수 메세지 출력
        Debug.Log(this.message);
    }

    // 다른 message를 출력하는 함수
    void PrintMessage()
    {
        Debug.Log(message);
    }
}
```

# Struct : 구조체

```
using UnityEngine;

// [1] 구조체 정의, 선언
// 명함 데이터를 관리하는 구조체
struct BusinessCard
{
    public string name;    // 이름 저장하는 변수
    public int age;        // 나이 저장하는 변수
    public string address; // 주소 저장하는 변수
    // public 키워드 : 코드블록 밖에서 사용이 가능하도록 함.
    // BusinessCard가 아닌 다른 클래서에서 사용이 가능하도록 함.
}

public class StructDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        /*
        // [2] 구조체 형식의 변수 선언
         BusinessCard MyCard;

         // [3] 구조체에 속해 있는 변수들의 초기화
         MyCard.name = "홍길동";
         MyCard.age = 20;
         MyCard.address = "서울시 강동구";

         // [4] 구조체 사용
         //Debug.Log($"이름 : {MyCard.name}, 나이 : {MyCard.age}, 주소 : {MyCard.address}");

         PrintUserInfo(MyCard.name, MyCard.age);
         PrintUserInfo(MyCard);
        */

        // [5] 구조체 형식의 배열 변수 선언, 요소수 생성

        BusinessCard[] cards = new BusinessCard[2];

        // [6] 구조체에 속해 있는 변수들 초기화
        cards[0].name = "백두산";
        cards[0].age = 25;
        cards[0].address = "인천광역시";

        cards[1].name = "임꺽정";
        cards[1].age = 35;
        cards[1].address = "경기도 수원시";

        // [7] 사용
        for (int i = 0; i < cards.Length; i++)
        {
            // PrintUserInfo(cards[i].name, cards[i].age);
            PrintUserInfo(cards[i]);
        }

    }

    // 매개변수로 이름과 나이를 입력받아 출력하는 함수
    void PrintUserInfo(string name, int age)
    {
        Debug.Log($"이름 : {name}, 나이 : {age}");
    }

    // 매개변수로 구조체(BusinessCard)를 입력 받아 이름과 나이를 출력하는 함수
    void PrintUserInfo(BusinessCard bizcard)
    {
        Debug.Log($"이름 : {bizcard.name}, 나이 : {bizcard.age}, 주소 : {bizcard.address}");
    }
}


/*
변수 : 프로그램에서 사용할 데이터를 저장해 놓는 그릇, 단일
배열 : 하나의 이름으로 같은 데이터 형식을 여러개 보관해놓는 그릇, 복수(같은 데이터 방식)
데이터 형식 : int, long, bool, float, double, string, char
변수 선언 시 : (데이터 형식) 변수 이름;

구조체(Struct) : 하나의 이름으로 서로 다른 데이터와 함수들을 묶어 관리하는 데이터 구조
사용자 정의 데이터 형식 : 개발자가 만든 데이터 형식
변수 선언 : (개발자가 만든 구조체) 변수 이름;

구조체 형식
struct (구조체 이름)
{
    서로 다른 형식의데이터들
    함수들
}
*/
```

# Enum

```
using UnityEngine;

// 동물들을 구분하는 열거형 정의, 선언 
enum Animal
{
    Mouse,  // 0
    Cow = 5,// 5
    Tiger,  // 6
    Dog,
    Cat
}

public class EnumDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [2] 열거형(Animal) 변수 선언하고 초기화
        Animal animal = Animal.Tiger;
        Debug.Log(animal);

        int number = (int)animal;
        Debug.Log($"{animal}: {number}");
        /*if (animal == Animal.Tiger)
        {
            Debug.Log("호랑이");
        }
        else
        {
            Debug.Log("아님말고");
        }*/

        // PrintAnimal(animal);
        
    }
    // 매개변수로 들어온 enum 값에 따라 동물 이름 출력
    void PrintAnimal(Animal Ani)
    {
        switch (Ani)
        {
            case Animal.Mouse:
                Debug.Log("쥐");
                break;
            case Animal.Cow:
                Debug.Log("소");
                break;
            case Animal.Tiger:
                Debug.Log("호랑이");
                break;
            case Animal.Dog:
                Debug.Log("강아지");
                break;
            case Animal.Cat:
                Debug.Log("고양이");
                break;
        }
    }
}

/*
Enum (열거형, Enumeration) : 하나의 이름으로 서로 관련있는 정수 값을 갖는 상수들의 집합
: 사용자 정의 데이터 형식 - 변수처럼 사용
: enum의 변수에는 정의에서 열거된 상수 이름만 저장된다.

: enum 선언 시, 맨 위에 있는 상수 이름의 상수 값은 0이다.
: 맨 위에 있는 상수를 제외한 다른 상수들의 값은 바로 위에 있는 상수의 값 + 1
: 각각의 상수 이름들은 선언시 상수값을 초기화 할 수 있다.

변수 사용
 
(개발자가 만든 enum) 변수 이름;


Enum 형식

enum (enum이름)
{
    상수 이름,  // 상수값 0
    상수 이름,  // 상수값 1
    상수 이름,  // 상수값 2
    ...
}

*/
```
