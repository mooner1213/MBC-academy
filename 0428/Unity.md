# 코딩 기초 1

Gem 만들어 두기

### 코딩 컨벤션 : 코딩 스타일
* 가독성있는 코드를 작성하기 위한 공통의 코드 작성 가이드라인
* 여러명의 개발자가 소스코드를 공유하거나 함께 관리할 때 유용
* 코딩을 잘하는지 판단하는 척도로도 사용

**공통 항목은 반드시 준수하고, 다른 항목은 통일성 있게 작성할 것**

### 주요 C++ 코딩 스타일 가이드라인
* ISOCPP C++ 가이드라인
* Google C++ 가이드라인
* PPP Style 가이드라인

### 명명규칙
> 타입, 변수, 함수 등의 이름은 의미를 알 수 있는 형태로 구성
> 너무 단순하거나 지나치게 장황한 이름은 자제

ex
```
int a1, a2, a3, a, b, c; //Bad
int i, j, k //Good, not bad
``` 

**타입이름 (클래스, 구조체, 타입별칭, 열거형 등)**
* 타입이름은 가급적 대문자로 시작
* 여러 단어로 이뤄진 이름의 경우, 각 단어는 대문자로 시작하고, 밑줄은 사용하지 않음.

ex
```
Class StudentInfo
{
  private:
    std::string name;
    int age;
};

std::string table_name; //OK
std::string tableName; //Bad
```

**변수 이름 & 함수이름**
* 변수와 함수 이름은 가급적 모두 소문자와 밑줄을 사용
* 상수, 매크로 이름은 대문자와 밑줄로 구성

ex
```
void print_tabels(...){}
#define MAX_STDENTS 30
```

### 공백

**공백**

**중괄호**
* 클래스 이름과 { 사이에 공백 삽입
* **if, for, switch, while**문에서 { 앞에 공백 삽입
* 클래스 이름과 { 사이에 줄바꿈 가능
* **for, switch, if, while**문과 { 사이에 줄바꿈 가능

ex
```
class box{
public:
  int x,y,width,height;
};
int range_sum ( int a, int b )
{
  int sum=0;
  for( int i=a ; i<= b ; i++ ){
    sum+=i;
  }
  return sum;
}
```

**소괄호**
* 함수 이름과 ( 사이에 공백 제거
* **if, for, switch, while**키워드와 ( 사이에 공백 삽입
* 함수 인자 또는 if, for, switch,while 문에서 여는 괄호 뒤, 닫는 괄호 앞에 공백 제거

**공백**

**쉼표, 세미콜론, 콜론, 연산자**
* 쉼표와 세미콜론 앞에는 공백 제거, 뒤에는 공백 삽입
* 범위기반 for 문에서 콜론 앞뒤에 공백 삽입
* 대입연산자, 이항연산자 앞뒤에 공백 삽입

### 기타
**기타 코딩 컨벤션**
* 들여쓰기는 Tab 또는 space bar 4개 권장
* 변수는 선언과 동시에 초기화
* 가급적 전역 변수의 사용은 자제
* "Magic constant"는 가급적 사용 자제
* 특정 숫자를 갑작스럽게 사용금지
* 의미를 알 수 있는 상수 변수 선언 권장
* **if, for, while**문에 하나의 문장만 있더라도 다음 줄에 작성
* 중괄호로 블록 지정하는 것이 좋음

### 알고리즘 성능 분석
**잘 해결하는가?**
* 정확성 테스트
* 수학적 귀납법
* 다양한 테스트 케이스 사용

**좋은 알고리즘인가?**
* 효율성 테스트
* 알고리즘의 자원 사용량을 분석 : 실행 시간, 메모리 사용량, 통신 용량 등
* 보통 실행 시간에 대한 분석만 다룸
* 대용량 입력 데이터에 대한 처리 능력 판단

### 시간 복잡도(오랜만이다 너)
**입력의 크기**가 커짐에 따라 **연산 시간**이 얼마나 증가하는 지를 **근사적**으로 표현
* 연산의 실행 횟수를 입력데이터의 크기(n)에 관한 함수형태로 표현
* 알고리즘을 직접 구현하지 않고도 알고리즘의 효율성을 가늠할 수 있음

**실행 시간 측정 방법의 한계**
* 알고리즘을 구현한 프로그램의 실행 시간은 실행 환경에 따라 달라지므로 절대적인 실행 시간 비교는 성능 파악에 한계가 있음

**빅오 표기법O(f(n))**
* 대표적인 시간 복잡도 표현 방법
* 연산 횟수를 구체적인 수식으로 표현하지 않고, 최고차항의 차수만으로 표현
* 점근 표기법의 한 방법으로 실행 시간의 상한을 표기

### 유니티 문법

위에서 한 내용이나, 코드로 정리 해주셨다.

```
using UnityEngine;

// 문법(Syntax) : 문법은 반드시 지켜야 하는 규칙이다.
// 코딩 컨벤션(코딩 스타일) : 프로그래밍 작성 가이드, 약속이다.
public class SyntaxDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 들여쓰기(Indentation)
        Debug.Log("들여쓰기는 공백 4칸 혹은 Tap을 사용한다.");

        // 공백 (White space) : C# 공백 무시
        Debug.Log("C#");
        Debug.Log( "C#" );
        Debug.
            Log(
            "C#"
            );
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

// 주석문(Comment) : 주석문은 컴파일, 실행에 영향을 주지 않는 코드

// : 한줄 주석

// 다중 주석문(Multi Comment)
/*
    여러 줄에 걸친 주석문
    여러 줄에 걸친 주석문
*/
```
### Debug.Log
**Debug.Log** 는 코드가 정상적으로 작동하고 있는지를 확인할 때 주로 사용한다.

```
using UnityEngine;

public class HelloUnity : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        Debug.Log("Start 함수 호출"); // 현재 이프로그램이 잘 되는지 확인하고 싶다면, 이렇게 로그를 찍어보는것이 좋은 방법이다.
    }

    // Update is called once per frame
    void Update()
    {
        Debug.Log("Update 함수 호출");
    }
}
```
이렇게 start 와 update 를 같이 쓰면,
<img width="948" height="161" alt="image" src="https://github.com/user-attachments/assets/9d4ea210-eaad-4bfc-9569-0718cab70ad7" />
이런식으로 콘솔이 출력된다.

하지만 우리는 update를 사용하지 않을 것이라고 하신다.

### 변수(variable)
**프로그램에서 사용할 데이터를 저장하는 공간, 혹은 그릇**

```
using UnityEngine;

// 변수 (Variable) : 프로그램에서 사용할 데이터를 저장할 수 있는 공간, 혹은 그릇

public class VariableNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 변수 만들기(선언)
        int i; // i 라는 이름으로 정수형 변수를 만든다. (정수형 : 소수점이 없는 숫자, 양수, 음수 모두 가능)

        // [2] 변수에 값 저장하기(대입, 할당, 초기화)
        i = 1234; // i 라는 변수에 1234 라는 값을 저장한다.

        // [3] 변수에 저장된 값 사용하기(참조)
        Debug.Log(i); // i 라는 변수에 저장된 값을 콘솔창에 출력한다.
    }
}
```
결과 콘솔창은 이렇다.
<img width="266" height="83" alt="image" src="https://github.com/user-attachments/assets/82baad83-8549-4a05-8db8-c1b734eecfb1" />

오랜만에 봐서 그런가 반갑네ㅎ

얘는 변수를 가지고 가능한 것의 기본이다.
```
using UnityEngine;

public class VariableDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 변수 선언과 동시에 값 대입하기 - 초기화
        int number = 7;
        Debug.Log(number);

        // [2] 여러개의 변수를 한줄에서 선언하기
        int number1 = 1, number2 = 2, number3 = 3;
        Debug.Log(number1 + number2 + number3);

        // [3] 여러개의 변수를 한줄에서 선언하고, 같은 값으로 초기화하기
        int a, b, c;
        a = b = c = 10;
        Debug.Log(a +"," + b +"," + c);
    }
}
```

### 데이터 값(변수에 저장할 데이터 값의 종류)

int - 정수형 변수
double - 실수형 변수
bool - 부울형 변수, 논리형 변수
string - 문자열 변수
char - 문자형 변수

```
using UnityEngine;

// 데이터 값 (Literal) : 변수에 저장할 데이터 값의 종류
public class VariableLiteral : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 변수 만들기(선언)
        int num; // 정수형 변수(-1, 0, 1)
        double su; // 실수형 변수(3.141592)
        bool flag; // 부울형 변수(논리형 변수 / 참, 거짓 판별)
        string str; // 문자열 변수("Hello")
        char c; // 문자형 변수('A', '문')

        // [2] 변수에 데이터 값 저장하기
        num = 1234;
        su = 3.141592;
        flag = true;
        str = "반갑습네다.";
        c = 'B';

        // [3] 변수에 저장된 데이터 값 사용하기
        Debug.Log("num:" + num);
        Debug.Log("su:" + su);
        Debug.Log("flag:" + flag);
        Debug.Log("str:" + str);
        Debug.Log("c:" + c);
    }
}
```

**문자열은 "" 로 표시, 문자형은 ''로 표시**

<img width="268" height="238" alt="image" src="https://github.com/user-attachments/assets/0e5a201d-7b3e-4492-bd4c-5604673b2317" />


### 상수(Constant)

**저장된 데이터 값이 변하지 않는 변수, 읽기 전용 변수**

```
using UnityEngine;

// 상수(Constant) : 저장된 데이터 값이 변하지 않는 변수, 읽기 전용 변수
public class ConstantDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 정수형 상수 만들기 : 선언과 동시에 초기화
        const int MAX = 100;

        // [2] 상수 사용하기 (참조)
        Debug.Log("MAX : " + MAX);
    }
}
```
<img width="255" height="92" alt="image" src="https://github.com/user-attachments/assets/5c0561e1-90f9-4fbf-ac48-37fb67772f6b" />
결과 값은 이렇게 된다.

### 정수형 타입

1 byte = 8 bit

1 bit : 0 또는 1 데이터를 저장하는 단위

**SignedInteger** : 부호가 있는 정수형 데이터 형식

sbyte = -128 ~ 127
short = -32768 ~ 32767
int = -2147483648 ~ 2147483647
long = 2경이 넘어감

**UnsignedInteger** : 부호가 없는 정수형 데이터 형식

byte = 0 ~ 255
short = 0 ~ 65,535
int = 0 ~ 약 4억
long = 0 ~ 엄청 큰 양수

```
using UnityEngine;

// 숫자 데이터 형식 사용하기 : 정수형, 실수형
// 정수형(Integer) : 소수점이 없는 숫자 데이터 형식, 양수와 음수 모두 표현 가능

public class IntegerDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // SignedInteger : 부호가 있는 정수형 데이터 형식
        sbyte isbyte = 127;
        short iInt16 = 32767;
        int iInt32 = 2147483647;
        long iInt64 = long.MaxValue;

        Debug.Log("sbyte : " + isbyte);
        Debug.Log("short : " + iInt16);
        Debug.Log("int : " + iInt32);
        Debug.Log("long : " + iInt64);

        // UnsignedInteger : 부호가 없는 정수형 데이터 형식
    }
}


/*
1 byte = 8 bit
1 bit : 0 또는 1 데이터를 저장하는 단위

8 bit
-> -128

0000 0000 -> 0
0000 0001 -> 1
0000 0010 -> 2
0000 0011 -> 3
.
.
.
1111 1111 -> 255

-> 127

* 왜 -128 이고 양수는 127일까? = - 부호를 표현하는 앞자리 0중에서도 정수 '0'을 포함하기 때문

sbyte : -128 ~ 127
byte : 0 ~ 255
*/
```

