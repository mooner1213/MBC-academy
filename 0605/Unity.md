# UI 구현

<img width="1029" height="621" alt="image" src="https://github.com/user-attachments/assets/12bdb48d-9427-4caf-9bd4-838cf1bec511" />

### 코드

```
using UnityEngine;
using TMPro; // TextMeshPro 기능 사용

namespace MySample
{
    /// <summary>
    /// UI 샘플 예제 - 버튼 호출 함수 구현
    /// </summary>
    public class UITest : MonoBehaviour
    {
        #region Variables
        private int n = 0; // 점프 횟수 변수
        public int Score = 0; // 점수 변수

        public TextMeshProUGUI ScoreText; // 점수를 화면에 보여주는 텍스트
        #endregion

        #region Custom Methods
        // Fire 버튼 클릭 시 호출 되는 함수(등록되는 함수)
        // : public void 버튼이름() { 실행할 코드 }
        public void Fire()
        {
            Debug.Log("발사!"); // 콘솔창에 로그 출력
        }

        // Jump 버튼 클릭 시 호출 되는 함수
        // 버튼을 누를 때 마다 점수(Score)가 10점씩 증가
        public void Jump()
        {
            Score += 10;
            n++;
            Debug.Log($"{n}번 점프하였습니다.");
            
            if (ScoreText != null)
            {
                ScoreText.text = $"Score : {Score}";
            }
        }
        #endregion
    }
}
```

### 과제

<img width="721" height="402" alt="image" src="https://github.com/user-attachments/assets/59fe6711-c681-4cee-a962-46cd725ebc65" />

BuildManager.cs
```
using UnityEngine;

namespace MyDefence
{
    public class BuildManager : MonoBehaviour
    {
        public static BuildManager Instance; // 싱글톤 패턴으로 BuildManager 클래스의 인스턴스(객체)를 담을 정적(static) 변수 선언

        #region Variables
        [Header("타워 프리팩 프리셋")]
        public GameObject TurretPrefab;      // 1번 머신건 타워 프리팹을 담을 바구니 (오타 Prefeb -> Prefab 수정)
        public GameObject AnotherTowerPrefab; // 4번 다른 타워 프리팹을 담을 바구니

        // 현재 유저가 어떤 타워를 선택했는지 '기억'하는 임시 보관 바구니예요. (선택 안 했을 땐 null)
        private GameObject towerToBuild = null;
        #endregion

        void Awake()
        {
            Instance = this;
        }

        #region Custom Methods (UI 버튼에서 호출할 함수들)
        // 2-2) 첫 번째 머신건 타워 버튼 클릭 시 호출
        public void SelectMachineGun()
        {
            towerToBuild = TurretPrefab;
            Debug.Log("머신건 타워를 선택 하였습니다!!");
        }

        // 4-1) 두 번째 다른 타워 버튼 클릭 시 호출
        public void SelectAnotherTower()
        {
            towerToBuild = AnotherTowerPrefab;
            Debug.Log("다른 타워 선택 하였습니다!");
        }
        #endregion

        #region Public Methods (Tile에서 확인할 기능들)
        // 현재 선택된 타워가 있는지 없는지 알려주는 함수 (null이 아니면 true)
        public bool HasSelectedTower()
        {
            return towerToBuild != null;
        }

        // 현재 선택된 타워 프리팹을 타일에 전달해주는 함수
        public GameObject GetTowerToBuild()
        {
            return towerToBuild;
        }
        #endregion
    }
}
```

Tile.cs
```
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems; // 마우스 이벤트 및 UI 감지 기능 사용

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
        private GameObject MyTurret;    // 타일에 실제로 설치된 터렛을 담두는 바구니
        private PointerEventData _eventData;
        private List<RaycastResult> _raycastResults = new List<RaycastResult>();
        #endregion

        #region Unity Event Method
        void Start()
        {
            rend = GetComponent<Renderer>();    // 이 오브젝트의 랜더러 컴포넌트를 꺼내와서 rend에 저장
            StartColor = rend.material.color;   // 현재 색을 StartColor에 저장
        }

        private bool IsPointerOverUI()
        {
            // 매번 new하지 않고 기존에 만들어둔 바구니 알맹이만 초기화해서 재사용합니다.
            if (_eventData == null) _eventData = new PointerEventData(EventSystem.current);
            _eventData.position = Input.mousePosition;

            _raycastResults.Clear(); // 예전 영수증은 싹 지우기
            EventSystem.current.RaycastAll(_eventData, _raycastResults);

            // 가급적 foreach 대신 메모리를 안 먹는 for문을 씁니다.
            for (int i = 0; i < _raycastResults.Count; i++)
            {
                if (_raycastResults[i].gameObject.layer == LayerMask.NameToLayer("UI"))
                    return true;
            }

            return false;
        }

        public void OnPointerEnter(PointerEventData eventData)
        {
            // [3번 과제] UI 위에 있으면 색 변경 안 함
            if (IsPointerOverUI()) return;

            if (!BuildManager.Instance.HasSelectedTower()) return;

            rend.material.color = EndColor;
        }

        public void OnPointerExit(PointerEventData eventData)   // 마우스가 타일에서 나갔을 때 실행
        {
            rend.material.color = StartColor;   // 기존색을 저장해뒀던 StartColor로 다시 적용
        }

        public void OnPointerClick(PointerEventData eventData)
        {
            // [3번 과제] UI 위에 있으면 타일 클릭 무시
            if (IsPointerOverUI()) return;

            if (isOccupied) return;

            if (!BuildManager.Instance.HasSelectedTower())
            {
                Debug.Log("타워를 설치하지 못했습니다.!!");
                return;
            }

            Debug.Log("마우스 클릭 - 여기에 터렛 설치");    // 콘솔창에 클릭할때마다 로그 출력

            // BuildManager에서 현재 유저가 선택한 타워 프리팹을 가져옵니다.
            GameObject towerPrefab = BuildManager.Instance.GetTowerToBuild();

            // 가져온 타워를 내 위치에 생성하고 MyTurret 변수에 담아 기억합니다.
            MyTurret = Instantiate(towerPrefab, transform.position, Quaternion.identity);

            isOccupied = true;

            // 타워가 설치되면 하이라이트 색상을 풀고 원래 색상으로 돌려줍니다.
            rend.material.color = StartColor;
        }
        #endregion
    }
}
```

**OnMouseEvent로는 불가능 하다. 레이캐스트 써야함. 내가 모르는걸지도 암튼 안되던데**

