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

