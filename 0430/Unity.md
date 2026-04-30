# 연산자

### 단항 연산자와 이항연산자

```
using UnityEngine;

// Opertator, 연산자 : +, -, *, /, % 등과 같은 연산을 수행하는 기호
public class OperatorDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] Unary Operator (단항 연산자) : +, - 
        int value = 0; // 정수형 변수 value 선언하고 0으로 초기화하기

        value = 8; // 정수형 변수 value 에 8 저장
        value = +value; // 정수형 변수 value 에 +value 값 저장하기
        Debug.Log(value); // 8

        value = -8; // 정수형 변수 value 에 -8 저장
        value = +value; // 정수형 변수 value 에 +value 값 저장하기
        Debug.Log(value); // -8

        value = 8; // 정수형 변수 value 에 8 저장
        value = -value; // 정수형 변수 value 에 -value 값 저장하기
        Debug.Log(value); // -8

        value = -8; // 정수형 변수 value 에 -8 저장
        value = -value; // 정수형 변수 value 에 -value 값 저장하기
        Debug.Log(value); // 8

        // [2] Binary Operator (이항 연산자) : +, -, *, /, %

        int i = 5;
        int j = 3;
        
        int k;

        k = i + j; // 5 + 3 = 8
        Debug.Log(k);

        k = i - j; // 5 - 3 = 2
        Debug.Log(k);

        k = i * j; // 5 * 3 = 15
        Debug.Log(k);

        k = i / j; // 5 / 3 = 1
        Debug.Log(k);

        k = i % j; // 5 % 3 = 2
        Debug.Log(k);
    }
}
```

### 추가기능

```
using UnityEngine;

// + 더하기 연산의 추가 기능 : 문자열 더하기
public class OperatorNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        Debug.Log("Hello" + "World"); // HelloWorld
        Debug.Log("Hi" + " " + "EveryOne"); // Hi EveryOne

        Debug.Log("123" + "456"); // 문자열 + 문자열 = 문자열 취급
        Debug.Log("123" + 456); // 문자열 + 숫자 = 문자열 취급
        Debug.Log(123 + "456" + 789 + 890); // 숫자 + 문자열 + 숫자 + 숫자
        Debug.Log(123 + 456); // 숫자 + 숫자 = 산술 연산

        Debug.Log("123" + true); // 문자열 + bool 형식 = 문자열 취급

        // Debug.Log("123" - 456); // 오류 발생 : 문자열과 숫자 사이의 뺄셈은 불가능
    }
}
```

### 할당 연산자(대입)

* 변수의 값을 저장한다. (ex. =, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=)
```
[Q]
 +, - 다른 연산 없이 변수 i, j의 값을 서로 바꾸어서 저장하세요.
 
 [output]
처음에 저장하는 값

i = 100
j = 200

변경시 결과

i = 200
j = 100
```

정답
```
[A]
using UnityEngine;


public class SwapDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int i = 100;
        int j = 200;

        Debug.Log($"i = {i}");
        Debug.Log($"j = {j}");

        int k = i;
        i = j;
        j = k;

        Debug.Log($"i = {i}");
        Debug.Log($"j = {j}");
    }
}
```

### 축약식

```
using UnityEngine;

public class incrementNumber : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 정수형 변수의 값을 1씩 증가하기
        // 정수형 변수 num을 선언하고 10으로 초기화
        int num = 10;
        // num의 값을 1씩 증가시키고, 증가 후 다시 num에 저장
        num = num + 1;

        Debug.Log(num); // 11

        // [2] 정수형 변수의 값을 1씩 감소하기
        // num의 값을 1씩 감소시키고, 감소 후 다시 num에 저장
        num = num - 1;

        Debug.Log(num); // 10

        // [3] 증가식, 감소식 축약해서 사용하기 (+=, -=, *=, /=, %=)
        int x = 3;
        x = x + 2; // 2씩 증가시키는 증가식
        Debug.Log(x); // 5

        int y = 3;

        y += 2; // 축약 식
        Debug.Log(y); // 5

        // [4] 누적식 (+=, -=, *=, /=, %=)
        int a = 3;
        int b = 5;

        // 누적 : b변수에 a변수의 값을 누적
        // b = b + a;
        b += a; // 축약 식
        Debug.Log(b); // 8

        // b 변수에 a 변수의 값을 감산 누적
        // b = b - a;
        b -= a; // 축약 식
        Debug.Log(b); // 5
    }
}
```

### 증가, 감소 연산자

```
using UnityEngine;

// 증가 연산자 (++) : 정수형 변수의 값을 1씩 증가
public class IncrementOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 증가 연산자
        int num = 100;

        // 1씩 증가
        // num = num + 1;
        // num += 1;
        ++num; // 전위 증가 연산자

        Debug.Log($"num : {num}"); // 101

        // [2] 감소 연산자
        --num; // 전위 감소 연산자
        Debug.Log($"num : {num}"); // 100
    }
}
```

### 전위, 후위 증감 연산자

```
using UnityEngine;

// PrefixOperator : 전위연산자 - 앞에 위치하는 증감 연산자
// PostfixOperator : 후위연산자 - 뒤에 위치하는 증감 연산자
public class PrefixOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 전위 증가 연산자
        int i = 3;
        int j = ++i; // i가 먼저 증가한 후 j에 대입

        Debug.Log($"i : {i}"); // 4
        Debug.Log($"j : {j}"); // 4

        j = i++; // j에 먼저 i의 값이 대입된 후 i가 증가

        Debug.Log($"i : {i}"); // 5
        Debug.Log($"j : {j}"); // 4
    }
}
```

### 관계형 연산자(비교 연산자)

```
using UnityEngine;

// RelationalOperator : 관계 연산자(비교 연산자) - <, >, <=, >=, ==, !=
// 연산 결과 : true 또는 false (논리형 데이터)
public class RelationalOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int a = 3; int b = 5;

        Debug.Log(a < b); // a는 b보다 작은가? : 결과 값 - true
        Debug.Log(a <= b); // a는 b보다 작거나 같은가? : 결과 값 - true
        Debug.Log(a > b); // a는 b보다 큰가? : 결과 값 - false
        Debug.Log(a >= b); // a는 b보다 크거나 같은가? : 결과 값 - false
        Debug.Log(a == b); // a는 b와 같은가? : 결과 값 - false
        Debug.Log(a != b); // a는 b와 다른가? : 결과 값 - true

        Debug.Log("AAA" == "aaa"); // 문자열 비교 : 결과 값 - false

    }
}
```

### And 연산자 (&&)

```
using UnityEngine;

// AndOperator (And 연산자, &&) 두 개의 조건이 모두 참이면, 참을 반환한다.
// 결과 : true, false
// bool 형이 두개 합쳐서 연산할 때, 둘다 참이면 참이다. 외에는 모두 거짓.
public class AndOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 둘 다 참일때

        Debug.Log(true && true); // true

        // [2] 둘 중 하나라도 거짓일 때
        
        Debug.Log(true && false); // false
        Debug.Log(false && true); // false

        // [3] 둘 다 거짓일 때

        Debug.Log(false && false); // false
    }
}
```

### Or 연산자 (||)

```
using UnityEngine;

// OrOperator (Or 연산자, ||) 두 개의 조건 중 하나라도 참이면, 참을 반환한다.
// 결과 : true, false
// bool 형이 두개 합쳐서 연산할 때, 둘 중 하나라도 참이면 참. 둘 다 거짓일 때만 거짓이다.
public class OrOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        
        // [1] 둘 다 참일 때
        
        Debug.Log(true || true); // true
        
        // [2] 둘 중 하나라도 참일 때
        
        Debug.Log(true || false); // true
        Debug.Log(false || true); // true
        
        // [3] 둘 다 거짓일 때
        
        Debug.Log(false || false); // false
    }
}
```

### Not 연산자(!)

```
using UnityEngine;

// NotOperator (부정 연산자, !) 참이면 거짓이 되며, 거짓이면 참이 된다.
// 결과 : true, false
public class NotOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        Debug.Log(!true); // false
        Debug.Log(!false); // true

        bool isOut = false;

        Debug.Log(!isOut); // true
        Debug.Log(!!isOut); // false
        Debug.Log(!!!isOut); // true

    }
}
```

### Logical 연산자(위에 했던것들)

연습
```
using UnityEngine;

public class LogicalOperator : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int i = 3;
        int j = 5;
        bool isR = false;

        isR = (i == 3) && (j != 3);
        Debug.Log($"isR : {isR}"); // true

        isR = (i != 3) || (j == 3);
        Debug.Log($"isR : {isR}"); // false

        isR = (i >= 5);
        Debug.Log($"isR : {isR}"); // false

        Debug.Log((1 == 1) || (1 != 1)); // true

        Debug.Log(!(1 == 1)); // false
    }
}
```
