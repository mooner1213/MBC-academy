# Unity 개발환경 세팅

### Copilot 연결

### Layout

<img width="256" height="144" alt="image" src="https://github.com/user-attachments/assets/03699a25-300d-4b4d-b5a4-137d6af0592f" />

**ctrl + shift + c : console**

* Layout을 본인 입맛에 맞게 설정하자. 그리고 save layout으로 현재 layout을 저장할 수 있다.

### 플레이 세팅

play 인지 아닌지 헷갈리기 때문에 플레이 중일때, 레이아웃들 색을 설정해주겠다.

<img width="380" height="671" alt="image" src="https://github.com/user-attachments/assets/9a6178df-ea6b-4082-b68f-cb1db245c681" />
<img width="521" height="20" alt="image" src="https://github.com/user-attachments/assets/dcacbc08-c3cb-4cb8-b8a7-2543e1c66aee" />
color 를 들어간 뒤,

사진을 따라가자. 저 색을 바꿔주면 된다.

바꾼뒤 플레이를 누르면?

<img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/e728af6e-9a47-47d5-84e8-be1c42188471" />

짜잔 색이 변한다.

그리고 preferences 온김에 이것도 확인해야한다.
<img width="690" height="576" alt="image" src="https://github.com/user-attachments/assets/b7d6a74d-acf0-4131-a148-d0dc7290a61f" />
visual studio 연결이 되어있는가? 를 확인해야한다.

그리고 늘 마지막엔 Hello,World 를 찍어야 마무리가 되었다고 할 수 있다ㅎㅎ

Assets폴더 안에 Scripts 폴더를 만들자.

그리고 이제 c# 파일이 많아질것이기 때문에, 폴더링을 귀찮더라도 꼭 하자.

Scripts 파일 안에 Hello,Unity 파일을 만들고

그안에 C# 파일을 만들자. C# 파일의 이름은 Hello,World 로 정했다.

만드는 방법은 이것이다.
<img width="581" height="785" alt="image" src="https://github.com/user-attachments/assets/cb011f54-bd64-45a4-9d39-4d3ff29b3134" />

만들었다면, 파일을 더블클릭하여, C#파일을 켜보자.

<img width="247" height="69" alt="image" src="https://github.com/user-attachments/assets/3091c19e-9eff-454a-ba88-1846578a3a8c" />
Start 에다가

Debug.Log("Hello, World");

를 쳐넣자. Debug.Log 는 Unity 에서 시작 시, 콘솔에서 뜨게끔 하는 것이다.

그 후, 저장한 뒤, 플레이 해보면....

어라? 아마 콘솔에서 안나올 것이다.

왜냐하면, 그 C# 명령을 적용시키기 위해서는, 스크립트가 게임내 오브젝트에 적용이 되어 있어야만 하기 때문이다.

고로, cube를 하나 만들고, 거기에 스크립트를 적용시켜 보자.

그럼 아마 될거임ㅋ

Like This
<img width="951" height="91" alt="image" src="https://github.com/user-attachments/assets/33f973a3-a833-4f33-b1f5-7db74f61c48b" />

오마갓 지져쓰

**Hello, World 에서의 문법 해석**

설명할 줄 알아야 함.
```
//[1] 네임 스페이스 선언부
using UnityEngine; // 현재 cs 파일에서 UnityEngine 네임스페이스를 사용

// [2] 클래스 선언부
public class HelloWorld : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    // [3] Start 메서드 선언, 정의 : 프로그램을 시작할때 1번만 실행
    void Start()
    {
        //[5] 명령문 : 콘솔에 "Hello, Unity!" 문자열 출력
        Debug.Log("Hello, Unity!");
    }

    // Update is called once per frame
    // [4] Update 메서드 선언, 정의 : 프로그램 시작후에 매 프레임마다 실행
    void Update()
    {
        
    }
}
```
만약, 네임스페이스를 사용하지않는다면...
<img width="711" height="309" alt="image" src="https://github.com/user-attachments/assets/228debcb-dd0d-4e0e-9c8b-7bf1ccf5f923" />

사진과 같이 매번 UnityEngine. 을 앞부분에 작성해 줘야한다. 7ㅐ불편한거 ㅇㅈ?

### 과제 등장

Q. 콘솔창에 아래 내용을 출력하라.

Hello, Game
123456789

### 개 쉬 움.

두가지 방법이 있다.

코드 안에

 Debug.Log("Hello, Game");
 Debug.Log("123456789");

 이렇게 쓰는 것이 있고,

 Debug.Log("Hello, Game\n123456789");

 이렇게 쓰는 것이 있는데

 차이점은, 처음 건
 <img width="236" height="75" alt="image" src="https://github.com/user-attachments/assets/89b75ff1-d3ee-4dbd-a9d4-d03eb3ec17a5" />

이렇게 두개의 콘솔 명령어로 표현이 되고,

다음 건
<img width="227" height="33" alt="image" src="https://github.com/user-attachments/assets/06d2fb21-63c2-4a98-98f0-1340d1cf983e" />

한 콘솔내에서 줄바꿈을 하여, 둘 다 표현이 가능하다.

아무튼 혹시 몰라서 둘다 넣어뒀다ㅋ 난 똑똑해

과제까지 마무리했고, 오늘의 Unity 학습은 여기까지다.
