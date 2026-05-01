# 제어문


1. 순차문 + 설명

```
using UnityEngine;

// 순차문 : 위에서 아래로 순서대로 명령문을 실행
public class SequenceDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 국어점수와 영어점수로 총점을 구하고 평균을 구하는 프로그램

        int kor = 100;
        int eng = 90;
        
        int total = 0;
        double avg = 0.0;

        total = kor + eng;// 총점 구하기
        avg = total / 2.0;// 평균 구하기

        Debug.Log($"총점 : {total}");
        Debug.Log( $"평균 : {avg:F1}"); // 소수 첫째 자리까지 출력
    }
}

/*
= 제어문 : 프로그램의 흐름(순서)를 정하는 명령문.
    - 순차문 : 위에서 아래로 순서대로 명령문을 실행
    - 조건문 : 조건에 맞는 명령문을 실행
    - 반복문 : 정해진 숫자만큼 명령문을 반복하여 실행
    - 기타 : 기타 제어문
*/
```

2. 조건문

**if 문**

```
using UnityEngine;

// 조건문 : 조건에 맞는 명령문을 실행
// if, switch
public class ifDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 만약 점수가 60점 이상이면 합격, 그렇지 않으면 불합격
        /*
        int score = 60;

        if (score >= 60) // 조건식
        {
            Debug.Log("합격"); // 실행문
        }
           Debug.Log("불합격");
        */

        /*
        만약 실행문이 하나라면 {} 생략 가능 
        
        if(score >= 60) // 조건식
            Debug.Log("합격"); // 실행문
        */

        // 중첩 if문 : if문 안에 if문이 있는 형태
        string name = "홍길동";
        int age = 20;

        // 만약 이름이 "홍길동"이라면, 실행문 실행
        if (name == "홍길동")
        {
            // 실행문 : 만약 나이가 20살이라면, 실행문 실행
            if (age == 20)
            {
                Debug.Log($"이름은 {name}, 나이는 {age}");
            }
        }
    }
}

/*
if문

조건식이 참일때 실행문을 실행
조건식이 거짓이면 실행문을 실행하지 않음

만약 조건식이 참이면 {} 안에 있는 실행문을 실행하라.
if(조건식)
{
    // 실행문1
    // 실행문2
    //......
}

else문 : if문과 함께 사용
- 만약 조건식이 참이라면 실행문1만 실행, else문의 실행문2는 실행하지 않음
- 만약 조건식이 거짓이라면 실행문2만 실행, if문의 실행문1은 실행하지 않음

if()
{
    // 실행문1
}
else
{
    // 실행문2
}
// 실행문3

1. 조건식이 참
실행문1 -> 실행문3 실행

2. 조건식이 거짓
실행문2 -> 실행문3 실행

*/
```

else 문 연습

```
using UnityEngine;

// 점수가 60점 이상이면 합격 출력, 아니라면 불합격 출력
public class ElseDemo : MonoBehaviour
{
    // 점수 입력
    public int score = 0; // 직접 입력 받기
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        if (score >= 60) // 점수가 60점 이상이면
        {
            Debug.Log("합격"); // 합격 출력

        }
        else // 아니라면
        {
            Debug.Log("불합격"); // 불합격 출력
        }
    }
}
```

else if 문 연습

```
using UnityEngine;

// 학점을 출력하는 프로그램
// 점수가 90 이상이면 A, 80이상이면 B, 70이상이면 C, 60이상이면 D, 나머지는 F
public class ElseIfDemo : MonoBehaviour
{
    public int score = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        if (score >= 90)
        {
            Debug.Log($"당신의 학점은 A 입니다.");
        }
        else if (score >= 80)
        {
            Debug.Log($"당신의 학점은 B 입니다.");
        }
        else if (score >= 70)
        {
            Debug.Log($"당신의 학점은 C 입니다.");
        }
        else if (score >= 60)
        {
            Debug.Log($"당신의 학점은 D 입니다.");
        }
        else
            Debug.Log($"당신의 학점은 F 입니다.");
    }
}
```

else if 문 연습 2

```
using UnityEngine;

public class IfElseAll : MonoBehaviour
{
    public int num = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 숫자 판별

        // 짝수 판별식 - 입력 받은 수가 짝수면 num은 짝수 출력, 아니라면 num은 홀수 출력
        /*
        if (num % 2 == 0)
        {
            Debug.Log($"입력한 정수는{num}이고, 짝수 입니다.");
        }
        else
        Debug.Log($"입력한 정수는{num}이고, 홀수 입니다.");
        */

        // 입력 받은 수를 3의 배수, 5의 배수, 7의 배수인지 판별하라.
        // num은 3의 배수, num은 5의 배수, num은 7의 배수, num은 3,5,7의 배수가 아닌 수

        if (num % 3 == 0)
        {
            Debug.Log($"{num}은 3의 배수");
        }
        else if (num % 5 == 0)
        {
            Debug.Log($"{num}은 5의 배수");
        }
        else if (num % 7 == 0)
        {
            Debug.Log($"{num}은 7의 배수");
        }
        else
        {
            Debug.Log($"{num}은 3, 5, 7의 배수가 아닌 수");
        }
    }
}
```

**Switch 문**

```
using UnityEngine;

//
public class SwitchDemo : MonoBehaviour
{
    public int num = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // num 이 1이면,num 은 1입니다. 라고 출력
        // num 이 2이면,num 은 2입니다. 라고 출력
        // 다른 수 이면 반응 x

        switch (num) // num data 판별
        {
            case 1:
                Debug.Log("num은 1입니다.");
                break;

            case 2:
                Debug.Log("num은 2입니다.");
                break;
        }
    }
}
/*

switch 문
조건 Data 값에 따라 명령문을 실행

switch(조건 data)
{
    case 1번 :
        // 실행문1
        break;

    case 2번 :
        // 실행문2
        break;

    case 3번 :
        // 실행문3
        break;

    default : // 모든 경우가 아니라면
        // 실행문4
        break;
}

*/
```

연습 1

```
using UnityEngine;

public class SwitchNote : MonoBehaviour
{
    public int answer = 0;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 1번 답을 선택했습니다., 2번 답을 선택했습니다., 3번 답을 선택했습니다., 4번 답을 선택했습니다.
        // 4개 다 아니면, 잘못 선택 하셨습니다. 출력

        switch (answer)
        {
            case 1:
                Debug.Log($"{answer}번 답을 선택했습니다.");
                break;

            case 2:
                Debug.Log($"{answer}번 답을 선택했습니다.");
                break;

            case 3:
                Debug.Log($"{answer}번 답을 선택했습니다.");
                break;

            case 4:
                Debug.Log($"{answer}번 답을 선택했습니다.");
                break;

            default:
                Debug.Log("잘못된 답을 선택했습니다. 다시 선택해 주세요.");
                break;
        }
    }
}
```

