# 반복문

### for

for demo 튜토리얼이다.

(원래 안녕하세요 3번만 하랬는데, 카운팅까지 했다. 난 할줄알기 때문이지 캬캬)
```
using UnityEngine;

public class ForDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        for (int i = 0; i < 3; i++)
        {
            Debug.Log($"{i+1}번째 인사입니다. 안녕하세요.");
        }
    }
}

/*
제어문 : 순차문, 조건문(if, switch), 반복문(for, while, ...)

== for

for(초기식; 조건식; 증강식)

초기식 -> 조건식 판별(참) -> 반복 명령문 실행 -> 증감식 -> 조건식 판별(참) -> 반복 명령문 실행 -> 증감식

초기식 -> 조건식 판별(거짓) -> for문 종료

{
    // 반복 실행문
}
// 초기식 : 조건식에서 사용하는 변수의 초기값 설정(초기화)
// 조건식 : 조건식을 참, 거짓으로 판별, 참일 경우 반복문 1회 실행, 거짓일 경우 for 문 종료
// 증강식 : 조건식의 변수를 다시 연산해주는 식, 반목문을 실행할때 마다 실행한 직후 실행
*/
```

하지만 카운트를 또 한다. 당연하긴 해


ForCount
```
using UnityEngine;

// 1부터 5까지 1씩 증가하면서 값을 출력하는 프로그램 구현

public class ForCounter : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        for (int i = 0; i < 5; i++)
        {
            Debug.Log($"Count : {i + 1}");
        }
    }
}
```

다음은 반복해서 더하는 식이다.

여기부턴 확실히 잘 알아두는게 좋다.

ForSum
```
using UnityEngine;

// 1 부터 20 까지의 합을 구하는 프로그램 구현
public class ForSum : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int n = 20;
        int sum = 0;
        for (int i = 1; i <= n; i++)
        {
            sum = sum + i;
        }
        Debug.Log($"1~20까지의 합은 {sum}입니다.");
    }
}
```

ForSum 연습하기
```
 // 1부터 10까지의 정수중 짝수들의 합을 구하는 프로그램 구현

 int n = 10;
 int sum = 0;

 for (int i = 1; i <= n; i++)
 {
     if (i % 2 == 0) // 짝수 판별식
     {
         sum = sum + i;
     }
 }
```

이번엔 팩토리얼이다.

4!을 출력하는 프로그램인데, 내가 바꿨다ㅋ 더 어렵게ㅋ

입력받는 값의 팩토리얼 값을 출력하는 프로그램이다.
```
using UnityEngine;

public class ForFactorial : MonoBehaviour
{
    public int factorial = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 4! 값을 구하는 프로그램 구현...인데 내 입맛대로 바꿈ㅋ
        // 입력받은 값의 팩토리얼 값을 출력하는 프로그램임.

        int sum = 1;
        for (int i = 1; i <= factorial; i++)
        {
            sum = sum * i;
        }
        Debug.Log($"{factorial}!의 값은 {sum}입니다.");
    }
}
```

while 문이다.

```
using UnityEngine;

public class WhileDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 안녕하세요를 3번 출력하는 프로그램 구현
        int i = 0;
        while (i < 3) // 조건식
        {
            Debug.Log("안녕하세요.");
            i++;
        }
    }
}

/*
제어문: 순차문, 조건문, 반복문(for, While...)
    == while
    while(조건식)
    {
        // 반복 실행문
    }

조건식 판별(참) -> 반복문 실행 -> 조건식 판별(참) -> 반복문 실행
조건식 판별(거짓) -> while 반복문 종료


조건식이 참이면 반복문을 실행, 거짓이면 while 문 종료

 */
```

while 문 응용이다.
```
using UnityEngine;

public class WhileSum : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // while 문을 이용해서 1~100까지의 합을 구하는 프로그램 구현

        int i = 1;
        int sum = 0;
        while (i <= 100)
        {
            sum = sum + i;
            i++;
        }
        Debug.Log(sum);

        // 짝수의 합만 구하기
        int j = 1;
        int sum2 = 0;

        while (j < 100)
        {
            if(j % 2 == 0)
            {
                sum2 = sum2 + j;
                j++;
            }
        }
        Debug.Log(sum2);
    }
}
```

list 연습이다.
```
using UnityEngine;

// 1부터 100까지의 정수 중에 3의 배수 or 4의 배수를 구해서 합하는 프로그램을 구현
// 응용함. i부터 j까지의 정수를 받겠음. x는 입력 받아야함.
public class SumPractice : MonoBehaviour
{
    public int i = 0;
    public int j = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int sum = 0;

        if (j < i)
        {
            Debug.Log("다시 숫자를 설정해주세요.");
        }
        else
        {
            int si = i;
            for (int n = i; n <= j; n++)
            {
                if (n % 3 == 0 || n % 4 == 0)
                {
                    sum = sum + n;
                }
            }
            Debug.Log($"{i}에서 {j}까지의 정수 중 3 또는 4의 배수의 합은 {sum}입니다.");
        }
    }
}
```
