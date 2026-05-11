#Class

```
using UnityEngine;

public class ClassDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 정적(Static) 메서드 호출 : 클래스 이름.메서드이름
        // (클래스이름). 메서드이름, (클래스이름). 변수이름

        ClassMember.StaticMethod();

        // [2] 인스턴스(Instance) 메서드 호출
        // 클래스의 객체를 생성 : new 키워드로 생성
        // (객체이름). 메서드 이름, (객체이름). 변수이름

        ClassMember member = new ClassMember();
        member.InstanceMethod();

    }
}

/*

변수 : 프로그램에서 사용할 데이터를 저장해 놓는 그릇, 단일
배열 : 하나의 이름으로 같은 데이터 형식을 여러개 보관해놓는 그릇, 복수(같은 데이터 방식)
데이터 형식 : int, long, bool, float, double, string, char
변수 선언 시 : (데이터 형식) 변수 이름;
배열 선언 시 : (데이터 형식)[] 변수이름;

구조체(Struct) : 하나의 이름으로 서로 다른 데이터와 함수들을 묶어 관리하는 데이터 구조

클래스 (Class) : 하나의 이름으로 서로 다른 형식의 데이터들과 함수들을 묶어 관리하는 데이터 구조
닷넷에서 사용하는 기본 구문
사룡자 정의 데이터 형식 : 개발자가 만든 데이터 형식
클래스 객체(개체, 인스턴스) 생성(변수 선언) - new 키워드로 새로운 객체를 생성
: (클래스 이름) 변수이름 = new 클래스이름(); <= 변수


// 클래스 선언, 정의
public class 클래스 이름
{
}

클래스에 있는 함수(Funciton, Method) 사용

*/
```

### 연습

```
using UnityEngine;
using System;

// Ramdom 클래스 : 랜덤값 구하는 함수들이 있는 클래스
public class RamdomDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // Random 클래스의 인스턴스 생성
        // 클래스이름 객체이름 = new 클래스이름();
        System.Random random = new System.Random();

        // Random 값 구하기
        Debug.Log(random.Next());       // 임의의 정수를 반환하는 함수
        Debug.Log(random.Next(5));      // 0 ~ 4 사이의 정수 값중 랜덤값 반환
        Debug.Log(random.Next(1, 10));  // 1 ~ 9 사이의 정수 값중 랜덤값 반환
    }
}
```

```
using UnityEngine;

// 기본 클래스
public class ClassMember
{
    // [1] 정적(static) 메서드
    public static void StaticMethod()
    {
        Debug.Log("[1] 정적메서드");
    }

    // [2] 인스턴스 메서드
    public void InstanceMethod()
    {
        Debug.Log("[2] 인스턴스 메서드");
    }
}
```

### 로또 프로그램 만들기
```
using UnityEngine;
using System;

// 로또 생성기
public class RandomPractice : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int[] num = new int[6]; // 6개의 방을 만듬

        System.Random random = new System.Random();
        for (int i = 0; i < num.Length; i++) // 배열의 길이만큼 반복해라
        {
            num[i] = random.Next(1, 46); // 배열에 있는 방마다 1 ~ 45사이의 랜덤 정수를 집어 넣기
            
            for (int j = 0; j < i; j++) // 중복검사
            {
                if (num[i] == num[j]) // 만약 배열안의 값이 다른 배열 안의 값과 같다면
                {
                    i--; // 뒤로 돌아가세요
                }
            }
        }
        
        Debug.Log($"로또 번호는 : {num[0]}, {num[1]}, {num[2]}, {num[3]}, {num[4]}, {num[5]} 입니다.");

    }
}

/*

[1] 6개 번호
[2] 1 ~ 45 사이의 랜덤 번호
[3] 6개 번호끼리 중복 금지

3가지의 조건이 들어 맞는 6개의 번호를 출력하는 프로그램 구현

[1] 임의의 숫자 6개 번호 생성(1 ~ 45 사이의 랜덤 값)
[2] 임의의 숫자 6개 번호 저장
[3] 임의의 숫자가 저장된 6개 번호 출력
[4] 중복 제거 기능 추가

*/
```

