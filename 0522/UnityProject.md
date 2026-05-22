# 유니티

### 유니티 돌아가는 방식

```
using UnityEngine;

public class EventTest : MonoBehaviour
{
    private void Awake()
    {
        Debug.Log("[1] Awake 실행");  // 1회만 실행, 가장먼저 실행함.
    }

    private void Start()
    {
        Debug.Log("[2] Start 실행");  // 1회만 실행
    }

    private void OnEnable()
    {
        Debug.Log("[7] OnEnable 실행");  // (활성화 될 때마다)1회만 실행
    }

    private void FixedUpdate()
    {
        Debug.Log("[3] FixedUpdate 실행");  // 1초에 50번 고정 호출, 물리연산
    }

    private void Update()
    {
        Debug.Log("[4] Update 실행");  // 매 프레임마다 호출, 게임 로직 연산
    }

    private void LateUpdate()
    {
        Debug.Log("[5] LateUpdate 실행");  // update 실행 바로 뒤에 따라서 실행, 카메라 연산 등
    }

    private void OnDisable()
    {
        Debug.Log("[7-1] OnDisable 실행");  // (비 활성화 될 때마다)1회만 실행
    }

    private void OnDestroy()
    {
        Debug.Log("[6] OnDestroy 실행");  // 소멸 시 마지막으로 실행
    }
}
```
### 의자를 앞으로 이동하게 하는 코드

```
using UnityEngine; // 유니티 엔진의 기능을 사용하기 위해 꼭 필요해요.

namespace MySample
{
    public class ChairMove : MonoBehaviour
    {
        // [변수 설정]
        // moveSpeed는 의자가 움직이는 속도를 결정해요.
        // 5.0f라고 적으면 '초당 5미터' 정도로 생각하시면 됩니다.
        // [SerializeField]를 쓰면 유니티 에디터에서 이 속도를 직접 조절할 수 있어요.
        [SerializeField] private float moveSpeed = 5.0f;

        // Update 함수는 매 프레임마다 한 번씩 실행되는 '심장' 같은 함수입니다.
        // (보통 게임은 초당 60프레임을 목표로 하니, 초당 60번 실행될 수도 있어요!)
        void Update()
        {
            // [이동 명령]
            // 1. transform.Translate는 이 오브젝트를 움직이라는 명령어입니다.
            // 2. Vector3.forward는 "앞쪽(Z축)"을 나타내는 미리 정의된 방향입니다. (이미지의 파란 화살표!)
            // 3. * moveSpeed는 지정한 속도만큼 곱해주는 것입니다.
            // 4. * Time.deltaTime은 아주 중요해요! 
            //    프레임과 무관하게 '초' 단위로 일정한 움직임을 만들기 위해 사용합니다.
            //    (성능이 좋은 컴퓨터나 안 좋은 컴퓨터나 똑같이 초당 moveSpeed만큼 가게 해줘요.)

            transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime);
        }
    }
}
```

## 유니티 스토어

https://assetstore.unity.com/ko-KR?srsltid=AfmBOoqDRwf9PS5kL3NKyIcJyC2X2JoB89TDUyBwyB4B6wOC0bOsPeAK

유니티 패키지 내보내는 방법

<img width="361" height="622" alt="image" src="https://github.com/user-attachments/assets/29c417c8-112e-45f3-ad83-71ccd46b2ab6" />
이거 누르기

<img width="396" height="380" alt="image" src="https://github.com/user-attachments/assets/817a6a38-09da-4c00-81d9-9b205d514084" />
이게 뜨는데 아래에 인클루드 올 스크립트 체크 해제

만들면, 만든 경로에 package 생성

**Scene도 저장하고 포함해서 마찬가지로 생성도 가능**

저장 후, 에셋파일 우클릭, 위에 누른거 누르면
<img width="401" height="376" alt="image" src="https://github.com/user-attachments/assets/c3dff0df-e2a9-42af-8f08-09374ecbeb55" />

이런식으로 다뜸. 그럼 저게 전체로 패키지 만든거임. 올ㅋ
