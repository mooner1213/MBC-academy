### Generic

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GenericDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] Stack<T> 클래스 인스턴스 생성 : 문자열 전용
        Stack<string> stack = new Stack<string>();

        // [2] 데이터 넣기
        stack.Push("Ten");
        stack.Push("10");

        // [3] 데이터 꺼내기

        Debug.Log(stack.Pop());
        Debug.Log(stack.Pop());

        // [1] 컬렉션
        Stack st1 = new Stack();
        st1.Push(1234);
        int number1 = (int)st1.Pop();
        Debug.Log(number1);

        // [2] 제네릭 사용 : int 전용
        Stack<int> st2 = new Stack<int>();
        st2.Push(4567);
        int number2 = st2.Pop();
        Debug.Log(number2);

        // [3] 제네릭 클래스의 장점
        // 1. 형식의 안정성
        Stack o = new Stack();
        o.Push(9871);
        o.Push("Hello");
        Debug.Log(o.Pop());
        Debug.Log(o.Pop());

        // 2. 성능, 최적화
        o.Push(1234);   // 1234(값형) -> object형식에 저장 : boxing(박싱)
        int nunber3 = (int)o.Pop(); // object형 -> number3 (값형) : unboxing(언박싱)
        Debug.Log(nunber3);

        Stack<int> i = new Stack<int>();
        i.Push(1);
        // i.Push("Hi");    // 에러
        Debug.Log(i.Pop());

        
    }
}

/*
 
클래스 : 하나의 이름으로 서로 다른 형식의 데이터들과 함수들을 묶어 관리하는 데이터 구조
제네릭 클래스 : 형식 매개 변수 T에 지정한 데이터 형식으로 클래스에 멤버의 성질을 결정
  - Cup<T> : 컵 오브 티, 전용 컵 
 
 */
```

List 를 제너릭으로 해보기

```
using UnityEngine;
using System.Collections.Generic;

// 제네릭 리스트
public class ListOfint : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 배열 - 정수형 배열 변수 선언하고 요소수(크기) 생성
        int[] arrNumbers = new int[3];
        
        // 배열 초기화
        arrNumbers[0] = 10;
        arrNumbers[1] = 20;
        arrNumbers[2] = 30;

        // 배열 사용
        for (int i = 0; i < arrNumbers.Length; i++)
        {
            Debug.Log(arrNumbers[i]);
        }

        Debug.Log("======================");

        // 제네릭 리스트 사용 : int 전용 <int>
        // List<T> 의 인스턴스를 int 전용으로 생성하고 리스트에 40, 50, 60 을 저장하라

        List<int> ListNumber = new List<int>();

        // 리스트에 값 넣기
        ListNumber.Add(40);
        ListNumber.Add(50);
        ListNumber.Add(60);

        // 리스트 사용
        for (int i = 0; i < ListNumber.Count; i++)
        {
            Debug.Log(ListNumber[i]);
        }

        Debug.Log("======================");

        ListNumber.Add(80);

        // 리스트 사용
        for (int i = 0; i < ListNumber.Count; i++)
        {
            Debug.Log(ListNumber[i]);
        }

        // [3] 제네릭 리스트 클래스 (List<T>) : List<int>, List<String>, ...
        // <String> 전용 리스트 인스턴스 생성
        List<string> ListStr = new List<string>();
        // 리스트에 데이터 넣기
        ListStr.Add("R");
        ListStr.Add("G");
        ListStr.Add("B");

        // 리스트 사용
        foreach (var c in ListStr)
        {
            Debug.Log(c);
        }

        for (int i = 0;i < ListStr.Count;i++)
        {
            Debug.Log(ListStr[i]);
        }
    }
}
```

directionary 사용
```
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.InputSystem.LowLevel;

public class DictionaryDemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] Dictionary 제네릭 클래스
        // dictionary<TKey, Tvalue> 인스턴스 생성 : IDictionary(인터페이스) 로 생성
        IDictionary<string, string> data = new Dictionary<string, string>();

        // [2] 데이터 입력 : 키, 값을 매칭하여 입력
        data.Add("도", "경기도");
        data.Add("시", "수원시");

        // [3] 데이터 삭제 (키만 입력해도 삭제됨)
        data.Remove("도");

        //[4] 데이터 입력 2 : 인덱서를 사용하여 입력
        data["구"] = "장안구";

        // [5] 키값이 중복 불가 : 에러가 발생
        try
        {
            data.Add("구", "수성구");
        }
        catch(System.Exception ex)
        {
            Debug.Log(ex.Message);

            // [6] dictionary 사용
            foreach(KeyValuePair<string, string> item in data)
            {
                Debug.Log($"{item.key}, {item.Value}");
            }
        }

        // [6] dictionary 사용 2 : 인덱스

        Debug.Log(data["구"]);

    }
}
```

Linq 사용
```
using UnityEngine;
using System.Linq;

// Linq : 컬렉션 형태의 데이터를 가공할 때, 유용한 메서드를 많이 있다.
// 특정 형식에 원래 없던 기능을 덕붙이는 개념으로 제공하는 함수
public class Linqdemo : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // [1] 정수형 배열 선언하고 초기화
        int[] numbers = { 1, 2, 4 };

        // [2] 배열 사용하기
        int count = numbers.Count();
        Debug.Log($"count: {count}");

        int sum = numbers.Sum();
        Debug.Log($"sum: {sum}");

        double avg = numbers.Average();
        Debug.Log($"avg: {avg:#.##}");

        int Max = numbers.Max();
        Debug.Log($"Max: {Max}");

        int Min = numbers.Min();
        Debug.Log($"Min: {Min}");
    }
}
```

연습
```
using UnityEngine;
using System.Linq;
using System.Collections.Generic;

public class LinqNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 불형 배열 변수 선언하고 초기화
        bool[] isOuts = {true, false, true, false, true};

        // 배열의 개수 구하기, 배열의 값중에 true의 개수, 또는 false의 개수
        Debug.Log(isOuts.Count());

        // true의 갯수
        Debug.Log(isOuts.Count(x => x == true));

        // false의 갯수
        Debug.Log(isOuts.Count(y => y == false));

        // 정렬
        string[] colors = { "Red", "Green", "Blue" };

        // 오름차순 정렬(사전순서)
        IEnumerable<string> sortedColors =  colors.OrderBy(s => s);
        foreach (string color in sortedColors)
        {
            Debug.Log(color);
        }

        // 내림차순 정렬(사전순서)
        IEnumerable<string> sortedColors2 = colors.OrderByDescending(s => s);
        foreach(string color in sortedColors2)
        {
            Debug.Log(color);
        }

        // 리스트 사용
        List<string> allColors = new List<string> { "Red", "Green", "Blue" };
        var sColors = allColors.OrderByDescending(s => s);
        foreach (string color in sColors)
        {
            Debug.Log(color);
        }
    }
}
```

연습 2
```
using UnityEngine;
using System.Linq;
using System.Collections.Generic;

public class LinqWhere : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 정수형 배열 선언하고 초기화
        int[] numbers = { 1, 2, 3, 4, 5 };

        // numbers의 요소중에서 3보다 크고 짝수인 수를 구해서 리스트를 만들어 넣기
        List<int> listNumbers = numbers.Where(n => n > 3 && n % 2 == 0).ToList();

        foreach(int number in listNumbers)
        {
            Debug.Log(number);
        }
    }
}
```

### 오브젝트

클래스 one
```
using UnityEngine;

public class classOne
{
    // 정적(static) 멤버 메서드 : 클래스 이름. 메서드 이름()
    public static void Hi()
    {
        Debug.Log("안녕하세요.");
    }
}
```

클래스 two
```
using UnityEngine;

public class ClassTwo
{
    // [1] 정적(static) 멤버 함수
    public static void Hi()
    {
        Debug.Log("반갑습니다.");
    }

    // [2] 인스턴스(instance) 멤버 메서드 : static 키워드가 없는 함수
    public void Hello()
    {
        Debug.Log("또 만나요.");
    }

}
```

class 들을 가지고 와서 호출
```
using UnityEngine;

public class ClassNote : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        // 다른 클래스의 멤버 호출
        // [1] 정적(static) 멤버 함수 호출 : 클래스 이름.메서드 이름()

        classOne.Hi(); // 안녕하세요 출력

        ClassTwo.Hi(); // 반갑습니다 출력

        // [2] 인스턴스(instance) 멤버 호출
        // 멤버가 속한 클래스의 인스턴스(객체) 생성 : 인스턴스 이름. 메서드 이름()

        ClassTwo ct = new ClassTwo();
        ct.Hello();
    }
}
```
