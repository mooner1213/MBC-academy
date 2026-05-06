# Break, Continue

### break

반복문의 코드블록을 빠져나오게끔 하는 명령어(강제종료)

```
using UnityEngine;

// break : 반복문(for, while)의 {} 을 빠져나오는 명령문
//       : 반복문(for, while)을 강제 종료
public class BreakDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // for문 break
        // 안녕하세요 5번 반복 출력하기, 단i가 2일때 for문을 종료

        for(int i = 0; i < 5; i++)
        {
            Debug.Log("안녕하세요.");
            if (i == 2)
            {
                break;
            }
        }
    }
}
```

연습!
```
using UnityEngine;

// 1부터 10까지 정수의 합을 구하는 프로그램 구현
// 단 합을 구하다가 합이 22이상이되면 더이상 합을 구하지않고 합을 출력
public class BreakPractice : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int i = 1;
        int sum = 0;
        for(; ; )
        {  
        sum = sum + i;
        i++;
            if( sum >= 22)
            {
                break;
            }
        }
        Debug.Log($"sum의 합 : {sum}");
    }
}
```

### Continue

```
using UnityEngine;

// continue문 : 반복 실행문에서 continue가 있는 라인의 아래 실행문을 실행하지않고,
// 다음 반복문의 조건을 체크한 뒤, 다음 다음반복문 실행
public class ContinueDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 1부터 10까지 홀수만 출력하는 프로그램 구현
        /*for (int i = 1; i <= 10; i++)
        {
            if ( i % 2 != 0)
            {
                Debug.Log($"i : {i}");
            }
        }*/

        // 짝수는 출력 x
        for (int i = 0; i <= 10; i++)
        {
            if (i % 2 == 0)
            {
                continue;
            }
            Debug.Log($"i : {i}");
        }
    }
}
```

연습

```
using UnityEngine;

// [Q] 1부터 100까지의 합을 구하는 프로그램 구현
// 단, 1부터 100까지 중 3의 배수는 합에서 제외
public class ContinuePractice : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int sum = 0;
        for (int i = 1; i <= 100; i++)
        {
            if( i % 3 != 0)
            {
                sum += i;
            }
            else
            {
                continue;
            }
        }
        Debug.Log($"3의 배수를 제외한 100까지의 합 : {sum}");
    }
}
```

### 이중, 삼중 for 문

```
using UnityEngine;

// 이중 for문 : for(){ for () {} }
// 삼중 for문 : for(){ for () {for () } } }

public class ForStar : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // * 로 삼각형 만들기
        for (int i = 1; i <= 5; i++)
        {
            Debug.Log($"*을 {i}개 만큼 찍는다.");
            for(int j = 0; j < i; j++)
            {
                Debug.Log("*");
            }
        }
    }
}
```

### array (배열)

```
using UnityEngine;

// array (배열) : 하나의 이름으로 같은 데이터 형식을 여러개 보관해놓는 그릇
// 선언 : 데이터 타입[] + 변수 이름
public class ArrayDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 배열선언, 배열 만들기
        int[] numbers;

        // [2] 배열의 요소수 생성, 배열 크기(길이) 결정 - 그릇(방)의 개수 n개 지정
        // 배열 크기 결정이 되면, 각각의 방이 0으로 초기화
        numbers = new int[10]; // 배열의 방 번호 0 ~ n-1(0번부터 n개를 만든다는 뜻)

        // [3] 배열 초기화 - 배열 변수에 값 저장
        numbers[0] = 3480;
        numbers[1] = 2160;

        // [4] 배열 사용
        Debug.Log($"{numbers[0]} * {numbers[1]} * {numbers[2]} = {numbers[0] * numbers[1] * numbers[2]}");

    }
}
```

연습!

```
using UnityEngine;

// 정수형 배열을 만들고, 3개의 방을 만든다.
// 1번째 방 1저장, 2번째 방은 2저장, 3번째 방은 3저장 후, 이들을 콘솔창에 출력하라.
public class ArrayPractice : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        int[] nums;
        nums = new int[3];
        nums[0] = 1; 
        nums[1] = 2; 
        nums[2] = 3;

        // Debug.Log($"1번방 : {nums[0]}, 2번방 : {nums[1]}, 3번방 : {nums[2]}");
        for (int i = 0; i < 3; i++)
        {
            Debug.Log($"{i}번째 방의 값은 {nums[i]}이다.");
        }
    }
}
```

배열 간편하게 축소하기
```
using UnityEngine;

public class ArrayNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 배열 선언 및 요소수(개수) 생성, 초기화
        // int[] intArray = new int[3] { 1, 2, 3 };

        // [1-1] 배열 선언 및 요소수(개수) 생성 생략, 초기화
        //int[] intArray = new int[] { 1, 2, 3 };

        // [1-2] 배열 선언과 동시에 값 초기화
        int[] intArray = { 1, 2, 3, 4 };

        // [2] 배열 사용
        for (int i = 0; i < 3; i++)
        {
            Debug.Log($"intArray [{i}] : {intArray[i]}");
        }
    }
}
```
