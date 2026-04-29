### 실수형 데이터

* float : 32비트 실수형 데이터 형식
* double : 64비트 실수형 데이터 형식
* decimal : 128비트 실수형 데이터 형식

```
using UnityEngine;

public class DoubleDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] float형 변수 선언하고 초기화하기
        float f = 3.14f; // float형 변수는 숫자 뒤에 f를 붙여야한다.
        Debug.Log(f);

        // [2] double형 변수 선언하고 초기화하기
        double d = 3.141592; // double형 변수는 숫자 뒤에 아무것도 붙이지 않아도 되지만, d를 붙여도 된다.
        Debug.Log(d);

        // [3] decimal형 변수 선언하고 초기화하기
        decimal m = 3.141592m; // decimal형 변수는 숫자 뒤에 m을 붙여야한다.
        Debug.Log(m);
    }
}
```

대부분 float를 사용하며, double까지 사용한다.

### 논리형 데이터

* bool : 논리형 데이터(참, 거짓)

```
using UnityEngine;

public class BooleanDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] bool형 변수 선언하고 초기화하기
        bool bIn = true; // 참
        Debug.Log("bIn: " + bIn);

        bool isOut = false; // 거짓
        Debug.Log("isOut: " + isOut);
    }
}
```

### 문자형 데이터

* char : 문자형 데이터(하나의 문자만 가능, '' 를 써줘야함.)

```
using UnityEngine;

// char : 문자형 데이터 형식
public class CharacterDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] char형 변수 선언하고 초기화하기
        char grade = 'A';
        char kor = '한';

        Debug.Log("grade: " + grade);
        Debug.Log("kor: " + kor);
    }
}
```

### 문자열 데이터

* string : 문자열 데이터(문장, 단어 등)

```
using UnityEngine;

// string : 문자열 데이터 형식
public class StringDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] string형 변수 선언하고 초기화하기
        string name = "홍길동";

        // [1-1] int 상수 선언하고 초기화하기
        const int AGE = 20;

        // [2] string형 변수에 저장된 데이터 값 사용하기
        Debug.Log("name: " + name); // 문자열 + 문자열 => 문자열 더하기 연산
        Debug.Log($"내 이름은 {name}"); // 문자열 보간법 =>  $" {변수이름} "
    }
}
```

Q. 연습하기 : 문자열 보간법으로 콘솔창에 안녕하세요 홍길동 입니다. 를 출력하기

A. Debug.Log($"안녕하세요 {name}입니다.");

Q. 연습하기 2 : 이름은 홍길동, 나이는 20살 입니다.

A. Debug.Log($"이름은 {name}, 나이는 {AGE}살 입니다.");

Q. // 연습하기 3 : 이름은 이순신, 나이는 40살 입니다.

A. 
```
name = "이순신";
const int AGE2 = 40;
Debug.Log($"이름은 {name}, 나이는 {AGE2}살 입니다.");
```

### 형식 변환

```
using UnityEngine;

// TypeConversion : 형식 변환
public class TypeConversionDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] long형 변수 선언하고 변수가 저장할 수 있는 가장 큰 수로 초기화하기
        long l = long.MaxValue;
        Debug.Log($"l의 값 : {l}");

        // [2] int 형식의 변수에 l 변수에 있는 값을 저장하기(초기화)
        int i = (int)l; // long 변수의 값을 int 변수 저장시 오류 발생
        Debug.Log($"i의 값 : {i}"); // -1 (오버플로우 발생)
    }
}
```

```
using UnityEngine;

// 형식변환실습
public class TypeConversionNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // double형 변수 d를 선언하고 12.34로 초기화하기
        double d = 12.34; // 실수형 64bit
        // int 형 변수 i를 선언하고 1234 초기화하기
        int i = 1234; // 정수형 32bit

        // [1] d 에 i 값 저장하기 : double > int 묵시적(암묵적, 암시적) 형식변환
        d = i;
        Debug.Log($"암묵적 형식변환: {d}"); // 1234


        d = 12.34;
        i = 1234;

        // [2] i에 d 값 저장하기 : int > double 명시적(명백한) 형식변환
        i = (int)d; // () 캐스트 연산자
        Debug.Log($"명시적 형식변환: {i}"); // 12 (소수점 이하 버림)

        d = 12.34;
        i = 1234;

        // [3] 숫자가 아닌 다른 형식간의 변환
        // 문자열 변수 선언하고 초기화
        string s = "";      // 빈값으로 초기화
        // s 에 d 값 저장하기
        s = d.ToString(); // ToString() : 숫자를 문자열로 형식변환
        Debug.Log($"형식 변환 : {s}");
    }
}
```

### 변수의 타입 알기

* GetType : 변수의 타입

```
using UnityEngine;

public class GetTypeDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 변수의 타입 알아보기
        int i = 1234;
        string s = "안녕하세요";
        char c = 'a';
        double d = 3.14;

        Debug.Log(i.GetType()); // i 변수의 타입을 콘솔창에 출력
        Debug.Log(s.GetType()); // s 변수의 타입을 콘솔창에 출력
        Debug.Log(c.GetType()); // c 변수의 타입을 콘솔창에 출력
        Debug.Log(d.GetType()); // d 변수의 타입을 콘솔창에 출력
    }
}
```

### Var

* 암시적으로 형식화된 로컬 변수

```
using UnityEngine;

// var : 암시적으로 형식화된 로컬 변수
public class VarDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // name 변수 선언하고 "홍길동"으로 초기화하기
        var name = "홍길동"; // 초기화된 "홍길동" 값을 보고 name 변수의 타입을 string 형식으로 결정
        Debug.Log(name);
        Debug.Log("name type : " + name.GetType());
        
        // version 변수 선언하고 8.5으로 초기화하기
        var version = 8.5; // 초기화된 8.5 값을 보고 version 변수의 타입을 double 형식으로 결정
        Debug.Log(version);
        Debug.Log("version type : " + version.GetType());

        // car 변수 선언하고 100으로 초기화하기
        var car = 100; // 초기화된 100 값을 보고 car 변수의 타입을 int 형식으로 결정
        Debug.Log(car);
        Debug.Log("car type : " + car.GetType());
    }
}
```
