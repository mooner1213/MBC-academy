# Array

### 배열 인덱스

```
using UnityEngine;

public class ArrayIndex : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 크기가 3인 정수형 배열 선언하고 1,2,3으로 초기화
        int[] numbers = new int[3] { 1, 2, 3 };
        
        // 배열의 인덱스를 관리하는 변수 선언 : 0~2, 0으로 초기화
        int index = 0;

        Debug.Log(numbers[index++]); // 1
        Debug.Log(numbers[index++]); // 2
        Debug.Log(numbers[index++]); // 3

        Debug.Log(numbers[--index]); // 3
        Debug.Log(numbers[--index]); // 2
        Debug.Log(numbers[--index]); // 1
    }
}
```

### 문자열 String도 배열이다.

```
using UnityEngine;

// string : 문자열 데이터 -> 문자의 배열
public class ArrayString : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 문자열 변수 선언하고 초기화
        string arr = "C#8";

        Debug.Log(arr[0]);
        Debug.Log(arr[1]);
        Debug.Log(arr[2]);

        // 문자열 길이
        Debug.Log($"문자열 길이 : {arr.Length}");
    }
}
```

### 2중 배열

```
using UnityEngine;

// 2차원 배열 : 행과 열로 이뤄진 배열
public class ArrayTwo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        /*
        // [1] 배열 선언
        int[,] IntArray;

        // [2] 배열의 요소수(크기) 생성
        IntArray = new int[2,3];

        // [3] 배열 초기화
        IntArray[0, 0] = 1;
        IntArray[0, 1] = 2;
        IntArray[0, 2] = 3;

        IntArray[1, 0] = 4;
        IntArray[1, 1] = 5;
        IntArray[1, 2] = 6;
        */

        // 배열 선언 및 크기 생성 및 초기화

        int[,] IntArray = new int[2, 3] { { 1, 2, 3 }, { 4, 5, 6 } };

        // 배열 사용하기
        for (int i = 0; i < 2; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                Debug.Log(IntArray[i, j]);
            }
        }
    }
}
```

### 가변형 배열

```
using UnityEngine;

// 가변형 배열 : 두번째 요소의 길이가 가변적이다.
public class ArrayTwo2 : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 가변형 배열 선언 후, 첫 번째 요소수만 먼저 생성
        // 정수형 배열을 관리하는 배열이고 정수형 배열이 2개의 방을 가진다.
        int[][] IntArray = new int [3][];

        // [2] 두번째 요소수를 각각 생성하고 초기화
        IntArray [0] = new int[3] { 1,2,3 };
        IntArray [1] = new int[2] { 4, 5 };
        IntArray [2] = new int[10];

        // [3] 사용하기
        for (int i = 0; i < IntArray.Length; i++)
        {
            for (int j = 0; j < IntArray[i].Length; j++)
            {
                Debug.Log(IntArray[i][j]);
            }
            Debug.Log("=================");
        }
    }
}
```

# 함수

### 함수 기초

```
using UnityEngine;

public class FunctionDemo : MonoBehaviour
{
    // [1] 함수 만들기(선언, 정의) - 매개변수가 없는 함수
    void Hi()
    {
        Debug.Log("안녕하세요.");
    }

    // [3] 매개변수(Parameter)가 있는 함수 만들기(선언, 정의)
    // 매개 변수를 통해 들어온 문자열을 출력하는 함수
    void ShowMessage(string message)
    {
        Debug.Log(message);
    }

    // [4] 반환값이 있는 함수 만들기(선언, 정의)
    // 문자열 반환하는 함수
    string GetString()
    {
        // return 키워드로(데이터 타입에 맞게) 반환
        return "반환값(Return value)";
    }

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [2] 함수 사용하기, 호출하기
        Hi();
        Hi();
        Hi();

        ShowMessage("반갑습니다.");
        ShowMessage("또만나영");

        // 반환값과 같은 게이터 타입의 변수로 반환값을 저장한다.
        string reValue = GetString();
        Debug.Log(reValue);
    }
}

/*
함수 (Function, 메서드, Method)
: 반복해서 사용하도록 만들어진 하나 이상의 명령문을 포함하고 있는 코드 블록
: 가장 작은 단위의 프로그래밍
: 입력 -> 연산 -> 출력
== 함수의 종류
- 내장 함수: C# 에서 제공하는 함수, 유니티에서 제공하는 함수
- 사용자 함수: 유저(개발자)가 만드는 함수

: 매개변수가 없는함수
: 매개변수가 있는함수
: 반환값이 있는 함수

void 함수이름()
{
    // 하나 이상의 명령문
}

void 함수이름(매개변수)
{
    // 하나 이상의 명령문
}

// 반환값의 데이터 타입
(데이터 타입) 함수이름()
{
    // 하나 이상의 명령문

    return (데이터 타입)변수;
}
 
 */
```

### 함수사용

```
using UnityEngine;

// 두 수 (a, b)를 입력받아 두수중 작은 수, 큰 수를 찾는 프로그램 구현
public class FunctionMinMax : MonoBehaviour
{
    public int a = 0;
    public int b = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        /* int result = Min(-4, 2);
         Debug.Log(result);

         Debug.Log(Max(5, 3));*/

        // a,b 의 작은 값,큰 값 구하기

        int MinValue = Min(a, b);
        int MaxValue = Max(a, b);
        Debug.Log($"작은 값은 {MinValue}, 큰 값은 {MaxValue}");
    }

    // 매개변수로 입력받은 두 수중 작은 수를 반환하는 함수

    int Min(int x, int y)
    {
        if (x < y)
        {
            return x;
        }
        else
        {
            return y;
        }

    }

    // 매개변수로 입력받은 두 수중 큰 수를 반환하는 함수

    int Max(int x, int y)
    {
        /*int MaxValue = 0;
        if (x > y)
        {
            MaxValue = x;
        }
        else
        {
            MaxValue = y;
        }*/

     /*   // 3항 연산자
        // (조건식) ? 참일때 반환 값 : 거짓일때 반환 값
        int MaxValue = (x > y) ? x : y;*/

        return (x > y ? x : y);
    }
}
```

### 3항연산자

```
int Abs(int number)
{
    /*if (number < 0)
    {
        return -number;
    }
    else
    {
        return number;
    }*/

    return (number < 0) ? -number : number;
}
```

### 연습!

Q. 함수를 사용하여, 두개의 정수를 입력받아, 사칙연산 및 나머지 값을 구하는 프로그램을 구현하라.

```
using UnityEngine;

// 두개의 정수를 입력받아 사칙연산, + 나머지값을 구하는 프로그램 구현
// 0으로 나누는 것 제외
public class FunctionPractice : MonoBehaviour
{
    public int a, b = 1;

    int Plus(int a, int b)
    {
        return a + b;
    }

    int Minus(int a, int b)
    {
        return a - b;
    }

    int X(int a, int b)
    {
        return a * b;
    }

    int Slice(int a, int b)
    {
        return a / b;
    }

    int trash(int a, int b)
    {
        return a % b;
    }

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int Psum = Plus(a, b); 
        int Msum = Minus(a, b);
        int Xsum = X(a, b);
        int Ssum = Slice(a, b);
        int Tsum = trash(a, b);

        Debug.Log($"두 수의 더한 값은 {Psum}, 뺀 값은 {Msum}, 곱한 값은 {Xsum}, 나눈 값은 {Ssum}, 나눈값의 나머지는 {Tsum} 입니다.");
    }
}
```
