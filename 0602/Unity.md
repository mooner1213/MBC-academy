# My Defence

tile.cs
```
using UnityEngine;
using UnityEngine.EventSystems; // 마우스 이벤트 감지 기능 사용
namespace MyDefence
{
    // IPointerEnterHandler = 마우스가 올라왔을 때 감지
    // IPointerExitHandler = 마우스가 나갔을 때 감지
    // IPointerClickHandler = 마우스 클릭했을 때 감지
    public class Tile : MonoBehaviour, IPointerEnterHandler, IPointerExitHandler, IPointerClickHandler
    {
        #region variables
        private Color StartColor;   // 타일의 원래 색깔 기억
        public Color EndColor = Color.green;    // 마우스가 올라왔을 때 바뀔 색깔
        private Renderer rend;  // 타일의 색을 실제로 바꿔줄 컴포넌트
        private bool isOccupied = false;    // 타일에 터렛이 설치가 되어있는지에 대한 여부
        private GameObject MyTurret;    // 타일에 실제로 설치된 터렛을 담아두는 바구니
        public GameObject turretPrefab; // 설치할 타일 프리펩

        #endregion

        #region Unity Event Method
        void Start()
        {
            rend = GetComponent<Renderer>();    // 이 오브젝트의 랜더러 컴포넌트를 꺼내와서 rend에 저장
            StartColor = rend.material.color;   // 현재 색을 StartColor에 저장
        }

        public void OnPointerEnter(PointerEventData eventData)  // 마우스가 타일 위로 올라왔을 때 실행
        {
            rend.material.color = EndColor; // 타일의 색을 EndColor로 적용
        }

        public void OnPointerExit(PointerEventData eventData)   // 마우스가 타일에서 나갔을 때 실행
        {
            rend.material.color = StartColor;   // 기존색을 저장해뒀던 StartColor로 다시 적용
        }

        public void OnPointerClick(PointerEventData eventData)  // 마우스가 타일을 클릭했을 때 실행
        {
            Debug.Log("마우스 클릭 - 여기에 터렛 설치");    // 콘솔창에 클릭할때마다 로그 출력

            if (isOccupied) return;

            BuildManager.Instance.BuildTurret(transform.position); // BuildManager한테 위임
            isOccupied = true;
        }
        #endregion
    }
}
```

### 심플톤 디자인
```
using UnityEngine;

namespace MyDefence
{
    public class BuildManager : MonoBehaviour
    {
        public static BuildManager Instance; // 싱글톤 패턴으로 BuildManager 클래스의 인스턴스(객체)를 담을 정적(static) 변수 선언

        public GameObject TurretPrefeb; // 빌드할 터렛 프리팹을 담을 바구니

        void Awake()
        {
             Instance = this;
        }

        public void BuildTurret(Vector3 position)
        {
            Instantiate(TurretPrefeb, position, Quaternion.identity);
        }
    }
}
```

### 키 입력

```
using UnityEngine;

namespace MySample
{
    /// <summary>
    ///  old Input test 예제
    /// </summary>
    public class OldInputTest : MonoBehaviour
    {
        #region Variables
        #endregion

        #region Unity Event Method
        private void Update()
        {
            // 키 입력 체크 - w키 입력
            if (Input.GetKey("w"))
            {
                Debug.Log("W키를 누르고 있습니다.");
            }

            if (Input.GetKeyDown("w"))
            {
                Debug.Log("W키를 눌렀습니다.");
            }

            if (Input.GetKeyUp("w"))
            {
                Debug.Log("W키에서 손을 눌렀다가 뗐습니다.");
            }

            // GetButton - Input Manager에 정의되어 있는Buttons(Axis)의 이름을 가져와서 체크하는 방식
            // 버튼의 이름은 문자열로 가져온다.
            if (Input.GetButton("Jump"))
            {
                Debug.Log("점프 버튼을 누르고 있습니다.");
            }

            if (Input.GetButtonDown("Jump"))
            {
                Debug.Log("점프 버튼을 눌렀습니다.");
            }

            if (Input.GetButtonUp("Jump"))
            {
                Debug.Log("점프 버튼에서 손을 눌렀다가 뗐습니다.");
            }

            // GetAxis - Input Manager에 정의되어 있는 Axis(Buttons)의 이름을 가져와서 체크하는 방식
            // a, left : -1 ~ 0
            // d, right : 0 ~ 1
            float hValue = Input.GetAxis("Horizontal");
            Debug.Log($"Horizontal : {hValue}");

            float vValue = Input.GetAxis("Vertical");
            Debug.Log($"Vertical : {vValue}");

            // 스크린상의 마우스 위치값 가져오기
            float mouseX = Input.mousePosition.x;
            float mouseY = Input.mousePosition.y;
            Debug.Log($"Mouse Position : ({mouseX}, {mouseY})");
        }
        #endregion
    }
}
```
