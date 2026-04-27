# 혼자 게임 만들어보기

## 0421 시작

### 무지성 유니티 코딩 시작

아무것도 모르니까 **ai**를 이용해서 만들어본다.

**2d 횡스크롤 슈팅게임**을 만들어 보겠다.

일단 어떤걸 만들고 싶은지를 최대한 설명했다. 아참, AI는 **Claude ai**를 쓰고있다.
<img width="761" height="454" alt="image" src="https://github.com/user-attachments/assets/324a666b-4f1f-472d-b53a-acc0e6c6c6d1" />

### 플레이어 만들기

일단 플레이어를 만들어야 해서, 대충 2d object를 트라이앵글로 만들어서 플레이어를 대체했다.

그리고 우측으로 돌렸다. 2d 횡스크롤이기때문..

일단 추후에 피격이나 타격을 만들어야하므로 rigidbody 2d 컴포넌트를 추가했다.
<img width="445" height="346" alt="image" src="https://github.com/user-attachments/assets/73ae95a2-25b6-4912-9c53-93c842244053" />

Freeze rotation Z 를 체크했다. 물어보니까, 피격받았을때 회전 할 가능성을 없앤다고 하더라.
<img width="237" height="56" alt="image" src="https://github.com/user-attachments/assets/300831ea-e2c9-4264-af29-e1f41fee7750" />

그 후에, 이것도 추가하라던데
<img width="442" height="253" alt="image" src="https://github.com/user-attachments/assets/f3a1978f-b52d-44cf-b65d-143f6e8bacb3" />

일단 **isTrigger**를 체크하기 위함이 아닐까? 라고 생각한다.

후에 cs 파일을 추가해서 붙혔다. cs 내용은 이와같다.

```csharp
using UnityEngine;
using System.Collections;

public class Player : MonoBehaviour
{
    [Header("이동")]
    public float moveSpeed = 5f;

    [Header("슈팅")]
    public GameObject bulletPrefab;
    public float bulletSpeed = 10f;
    public float fireRate = 0.2f;

    [Header("체력")]
    public int maxHp = 10;
    private int currentHp;

    [Header("무적")]
    public float invincibleDuration = 1f;
    private bool isInvincible = false;

    private float nextFireTime;
    private SpriteRenderer spriteRenderer;
    private Camera mainCamera;

    void Start()
    {
        currentHp = maxHp;
        spriteRenderer = GetComponent<SpriteRenderer>();
        mainCamera = Camera.main;
    }

    void Update()
    {
        Move();
        ClampPosition();
        Shoot();
    }

    // ───────────────────────────────
    // 이동
    // ───────────────────────────────
    void Move()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        transform.Translate(new Vector3(h, v, 0) * moveSpeed * Time.deltaTime);
    }

    // ───────────────────────────────
    // 화면 밖으로 못 나가게 제한
    // ───────────────────────────────
    void ClampPosition()
    {
        // 카메라 기준으로 화면 경계 계산
        float camHeight = mainCamera.orthographicSize;
        float camWidth = camHeight * mainCamera.aspect;

        float x = Mathf.Clamp(transform.position.x, -camWidth, camWidth);
        float y = Mathf.Clamp(transform.position.y, -camHeight, camHeight);
        transform.position = new Vector3(x, y, 0);
    }

    // ───────────────────────────────
    // 슈팅
    // ───────────────────────────────
    void Shoot()
    {
        if (Input.GetKey(KeyCode.Z) && Time.time > nextFireTime)
        {
            nextFireTime = Time.time + fireRate;
            GameObject bullet = Instantiate(bulletPrefab, transform.position, Quaternion.identity);

            // 오른쪽으로 발사 (비행체가 오른쪽을 바라보므로)
            Rigidbody2D rb = bullet.GetComponent<Rigidbody2D>();
            rb.linearVelocity = Vector2.right * bulletSpeed;
        }
    }

    // ───────────────────────────────
    // 피격 처리
    // ───────────────────────────────
    void OnTriggerEnter2D(Collider2D other)
    {
        if (isInvincible) return;

        if (other.CompareTag("EnemyBullet") || other.CompareTag("Enemy"))
        {
            TakeDamage(2);
        }
    }

    void TakeDamage(int damage)
    {
        currentHp -= damage;
        Debug.Log($"플레이어 HP: {currentHp}");

        if (currentHp <= 0)
        {
            Debug.Log("게임 오버!");
            // 나중에 GameManager.Instance.GameOver() 연결
            gameObject.SetActive(false);
            return;
        }

        StartCoroutine(InvincibleRoutine());
    }

    // ───────────────────────────────
    // 무적 + 깜빡임
    // ───────────────────────────────
    IEnumerator InvincibleRoutine()
    {
        isInvincible = true;

        float elapsed = 0f;
        float blinkInterval = 0.1f;

        while (elapsed < invincibleDuration)
        {
            spriteRenderer.enabled = !spriteRenderer.enabled;
            yield return new WaitForSeconds(blinkInterval);
            elapsed += blinkInterval;
        }

        // 무적 끝나면 스프라이트 확실히 보이게
        spriteRenderer.enabled = true;
        isInvincible = false;
    }

    // ───────────────────────────────
    // 현재 HP 외부에서 읽기용
    // ───────────────────────────────
    public int GetCurrentHp() => currentHp;
}
```
뭐가 많은데, 나중에 추가하기 귀찮아서 **기능을 최대한** 생각나는대로 넣었다.

**이동, 체력, 탄막, 피격, 피격시 무적, 무적시 깜박거림, hp표시** 등등... 아마 이것도 모자라겠지

그런데 뭔가 이상했다. 플레이 하니까 방향키로 안움직이는거임;;

그래서 물어봤다.
<img width="739" height="714" alt="image" src="https://github.com/user-attachments/assets/bf684520-d671-4713-b360-751e8ab7b47f" />

**1,2,3,4 전부 아니었다.** 혹시몰라서 하나하나 다 찍어보냈는데, 다른게 없었거든... 당연히 플레이버튼은 눌렀는데 이자식이
<img width="719" height="352" alt="image" src="https://github.com/user-attachments/assets/8b85ce79-cf94-47a3-b304-1d07c3962441" />

**나를 무시하잖슴.**

그래서 플레이를 하고 뭔가 문제가 없나, 찾아보는데,,

플레이 화면 아래쪽에 **빨간글씨**로 뭔가 떠있는거임!!
<img width="1373" height="40" alt="image" src="https://github.com/user-attachments/assets/ff0a460c-ae61-474f-b333-53f9b5f8473d" />

잘은 안보이겠지만, 뭔가가 잘못되었다는건 알겠음..

그래서 물어보니까,
<img width="715" height="464" alt="image" src="https://github.com/user-attachments/assets/d7d2d9ac-e4ef-4b09-89f4-45e8a7edcdd7" />
라고한다. 1번을 따라서 해보니 바로 해결되었으나,,,

또 다른 **문제**가 생겼다.

아니 플레이어가 우측을 바라보고 있는데, 위 방향키를 누르니 **우측으로 돌진**하는 것이 아닌가!!!!!!!!!!!!!!!!!

그래서 이것도 물어봐서 해결했다.
<img width="724" height="484" alt="image" src="https://github.com/user-attachments/assets/cac45da6-b029-469d-9aca-82b5059ee3ea" />

"역시 ai야 금방 해결해주는구나?"

### 총알 만들기 + 쏘는 것까지

이제는 **총알 부분**을 한번 만들어 보겠다.
<img width="617" height="199" alt="image" src="https://github.com/user-attachments/assets/b3838750-925e-49e0-86d3-cf3b8d1274cb" />

바로 질문을 했다. 역시 점점 복잡해질것 같아서, 먼저 총알을 만들었다.

일단, **PlayerBullet.cs**

```
using UnityEngine;

public class PlayerBullet : MonoBehaviour
{
    [HideInInspector] public float speed = 15f; // Player.cs에서 설정됨

    void Update()
    {
        // 월드 기준 오른쪽으로 이동
        transform.Translate(Vector3.right * speed * Time.deltaTime, Space.World);

        // 화면 밖으로 나가면 삭제
        if (transform.position.x > Camera.main.orthographicSize * Camera.main.aspect + 2f)
        {
            Destroy(gameObject);
        }
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Enemy"))
        {
            // 적 HP 깎기
            Enemy enemy = other.GetComponent<Enemy>();
            if (enemy != null)
            {
                enemy.TakeDamage(1);
            }
            Destroy(gameObject);
        }
    }
}
```

그리고 **player.cs를 수정**했다.

```
[Header("슈팅")]
public GameObject bulletPrefab;
public float bulletSpeed = 15f;  // 탄속 (높을수록 빠름)
public float fireRate = 0.08f;   // 연사속도 (낮을수록 빠름)

private float nextFireTime;
```

```
void Shoot()
{
    if (Input.GetKey(KeyCode.Z) && Time.time > nextFireTime)
    {
        nextFireTime = Time.time + fireRate;

        GameObject bullet = Instantiate(bulletPrefab, transform.position, Quaternion.identity);
        PlayerBullet pb = bullet.GetComponent<PlayerBullet>();
        if (pb != null)
        {
            pb.speed = bulletSpeed; // Player에서 설정한 탄속 전달
        }
    }
}
```

그리고, 새로운 **enemy.cs**를 만들었다.

```
using UnityEngine;

public class Enemy : MonoBehaviour
{
    public int hp = 10;

    public void TakeDamage(int damage)
    {
        hp -= damage;
        Debug.Log($"적 HP: {hp}");

        if (hp <= 0)
        {
            Destroy(gameObject);
        }
    }
}
```
이건 **데미지를 미리 준비**하는 건데, 없으니까 오류뜨더라.(그럼 미리 만들라고하ㄱ라고!!!)

그리고 가장 중요한 **prefabs** 세팅...
<img width="736" height="337" alt="image" src="https://github.com/user-attachments/assets/ba339bbe-a9bf-4f0b-a2d1-85887b4d3288" />

만약 이걸 보는 초보가있다면, **prefabs세팅**을 꼭 제대로 하도록하자.

이걸 안해서 1시간동안 죽쒔다.

**그 내용을 지금 간략히 공개하겠다.**

난 prefabs가 아니라 그냥 플레이어 만드는 곳 **hieratchy에 만들어두고 prefabs에 뒀다고!!!** 이러고 있었음ㅋㅋ;;

그래서 AI가 **"아니 (불경한 욕) 그럴리가없는데 이거해봐, 저거해봐"** 하는데 다 안됨ㅋㅋㅋㅋ

<img width="617" height="61" alt="image" src="https://github.com/user-attachments/assets/436bb82d-a62f-41aa-a8ef-f3cb51736702" />
<img width="724" height="539" alt="image" src="https://github.com/user-attachments/assets/e185397c-1cbd-44cc-8bc5-9ea1501fc270" />
<img width="727" height="171" alt="image" src="https://github.com/user-attachments/assets/394c9f0a-7b02-49bd-94bf-faa7c495a8ad" />
<img width="721" height="140" alt="image" src="https://github.com/user-attachments/assets/2a19e65e-4ea1-4c22-bc96-f3bfedcc2fb2" />
<img width="716" height="169" alt="image" src="https://github.com/user-attachments/assets/e3418ad5-a79e-44b2-b617-9bceba170fb2" />
<img width="685" height="136" alt="image" src="https://github.com/user-attachments/assets/f6e67a6f-7e2f-46ed-839e-1089eab28c6a" />
<img width="689" height="130" alt="image" src="https://github.com/user-attachments/assets/fa922791-da41-4d9b-980b-01d8bec31866" />

**그동안 AI를 고생시킨 흔적... 안믿어줘서 미안하다.**

<img width="729" height="310" alt="image" src="https://github.com/user-attachments/assets/af99bc02-cc28-41a1-9a92-82a175f22ad4" />

저 위에 사진들... 일부만 발췌한거임...ㅋ

0421 오늘 하루, 게임 기획과 게임에 대한 과거에 대해 많은 수업을 들었지만, 대부분 선생님의 말씀이 대부분을 이뤄서,

짬내가며 만들어보았다. 정리하는 것도 일이네... 그래도 최대한 다 적어가며, 기록해가며 해보겠다.

0421에는 여기까지 만드는걸로~~


## 0422 시작

이번엔 AI를 고생시키지 않겠다고 다짐하며... 시작했다.

### 적 만들기

내가 과한 부탁을 했다. 이전에 했던 부탁까지 싸그리 다 적었나보다. 나보고 뭐라함..

<img width="726" height="258" alt="image" src="https://github.com/user-attachments/assets/9d8c4f23-9921-4608-8301-cee3706dde99" />

그래서 얘가 이동방식과 기본 탄막 패턴을 물어봐서, 둘다 제한을 두지 않았으면 좋겠다고 했다.

그렇게 하니까 얘가 나보고 야망있단다ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ 너 사람이지

아무튼 그래서 확장하기 쉽게끔 하기 위해, 베이스클래스 구조를 만들어주었다.

**EnemyBase.cs**
```
using UnityEngine;
using System.Collections;

public class EnemyBase : MonoBehaviour
{
    [Header("체력")]
    public int hp = 10;

    [Header("탄막")]
    public GameObject bulletPrefab;
    public float bulletSpeed = 4f;

    protected virtual void Start()
    {
        StartCoroutine(MoveRoutine());
        StartCoroutine(ShootRoutine());
    }

    // ───────────────────────────────
    // 이동 패턴 (자식 클래스에서 override)
    // ───────────────────────────────
    protected virtual IEnumerator MoveRoutine()
    {
        yield break; // 기본은 가만히
    }

    // ───────────────────────────────
    // 탄막 패턴 (자식 클래스에서 override)
    // ───────────────────────────────
    protected virtual IEnumerator ShootRoutine()
    {
        yield break; // 기본은 발사 안 함
    }

    // ───────────────────────────────
    // 피격 처리
    // ───────────────────────────────
    public void TakeDamage(int damage)
    {
        hp -= damage;

        if (hp <= 0)
        {
            OnDeath();
        }
    }

    protected virtual void OnDeath()
    {
        Destroy(gameObject);
    }

    // ───────────────────────────────
    // 플레이어 총알에 닿으면
    // ───────────────────────────────
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("PlayerBullet"))
        {
            TakeDamage(1);
            Destroy(other.gameObject);
        }
    }

    // ───────────────────────────────
    // 총알 발사 헬퍼 함수
    // ───────────────────────────────
    protected void FireBullet(Vector2 direction)
    {
        if (bulletPrefab == null) return;

        GameObject bullet = Instantiate(bulletPrefab, transform.position, Quaternion.identity);
        Rigidbody2D rb = bullet.GetComponent<Rigidbody2D>();
        if (rb != null)
        {
            rb.linearVelocity = direction.normalized * bulletSpeed;
        }
    }
}
```

그리고, 적의 총알도 만들어야 하지 않는가?

**EnemyBullet.cs**
```
using UnityEngine;

public class EnemyBullet : MonoBehaviour
{
    void Start()
    {
        // 10초 후 자동 삭제 (화면 밖 나가도 안전하게)
        Destroy(gameObject, 10f);
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            Destroy(gameObject);
        }
    }
}
```

휴 많은 걸 만들어줬지만, 막상 만들어지니, 또 어떻게 해야할지 모르겠더라ㅋㅋㅋㅋ

그래서 이 맘씨좋은 AI친구가 첫번째 적 예시를 줬다.

**EnemyA.cs**
```
using UnityEngine;
using System.Collections;

public class EnemyA : EnemyBase
{
    [Header("EnemyA 이동")]
    public float moveSpeed = 2f;

    protected override IEnumerator MoveRoutine()
    {
        // 오른쪽에서 왼쪽으로 직선 이동
        while (true)
        {
            transform.Translate(Vector2.left * moveSpeed * Time.deltaTime, Space.World);

            // 화면 왼쪽 밖으로 나가면 삭제
            if (transform.position.x < -Camera.main.orthographicSize * Camera.main.aspect - 2f)
            {
                Destroy(gameObject);
            }

            yield return null;
        }
    }

    protected override IEnumerator ShootRoutine()
    {
        yield return new WaitForSeconds(1f); // 등장 후 1초 뒤 발사 시작

        while (true)
        {
            FireBullet(Vector2.left); // 왼쪽으로 직선 발사
            yield return new WaitForSeconds(1.5f);
        }
    }
}
```
이제 유니티 안의 세팅을 해야하지.

저번에 prefabs 실수 한거때문에 이자식이 확실하게 챙겨준다ㅋㅋ 개웃김

<img width="714" height="526" alt="image" src="https://github.com/user-attachments/assets/f3e026eb-d184-4388-a535-e5954e72849f" />

추후에, 어떻게 확장을 하는건지도 알려준다.

<img width="720" height="150" alt="image" src="https://github.com/user-attachments/assets/9f8c8008-a8c8-4bcc-916d-ed59bb8a9169" />

친절해..

생각해보니, 적군이 스폰되지않으면 적이 등장하지않잖아..?

그래서 물어봤는데,

<img width="752" height="242" alt="image" src="https://github.com/user-attachments/assets/cba2c9bb-98d6-4750-b638-aa989118deb8" />

미리 말하라고!!!! 날 놀려?

그래서 스폰매니저 만들어준다고 한다. 아무튼 고마워 AIAI야~

**SpawnManager.cs**
```
using UnityEngine;
using System.Collections;

public class SpawnManager : MonoBehaviour
{
    [System.Serializable]
    public class EnemySpawnData
    {
        public GameObject enemyPrefab;  // 적 프리팹
        public float spawnInterval;     // 등장 간격 (초)
        public int maxCount;            // 최대 동시 등장 수
    }

    [Header("스폰 설정")]
    public EnemySpawnData[] enemyTypes; // 적 종류 목록
    public float startDelay = 2f;       // 게임 시작 후 첫 등장까지 대기시간

    private Camera mainCamera;

    void Start()
    {
        mainCamera = Camera.main;

        // 각 적 종류마다 스폰 코루틴 시작
        foreach (var enemy in enemyTypes)
        {
            StartCoroutine(SpawnRoutine(enemy));
        }
    }

    IEnumerator SpawnRoutine(EnemySpawnData data)
    {
        yield return new WaitForSeconds(startDelay);

        while (true)
        {
            // 현재 씬에 해당 적이 몇 마리인지 확인
            int currentCount = GameObject.FindGameObjectsWithTag("Enemy").Length;

            if (currentCount < data.maxCount)
            {
                SpawnEnemy(data.enemyPrefab);
            }

            yield return new WaitForSeconds(data.spawnInterval);
        }
    }

    void SpawnEnemy(GameObject prefab)
    {
        if (prefab == null) return;

        // 화면 오른쪽 밖에서 랜덤 Y 위치로 등장
        float camHeight = mainCamera.orthographicSize;
        float camWidth = camHeight * mainCamera.aspect;

        float spawnX = camWidth + 1f;
        float spawnY = Random.Range(-camHeight + 0.5f, camHeight - 0.5f);

        Instantiate(prefab, new Vector3(spawnX, spawnY, 0), Quaternion.identity);
    }
}
```

그리고 유니티 세팅이다.

<img width="726" height="511" alt="image" src="https://github.com/user-attachments/assets/cd93ab53-ee97-4f20-ac6b-bdb679916120" />

플레이 해보니 정상적으로 작동하기 시작했다.

그러나 데미지 피격을 테스트하는 과정에서 적과 겹쳐있으면 무적시간이 끝났음에도

피격 데미지가 들어오지 않는 것이었다. 그래서 물어봤지 또ㅋㅋ

<img width="716" height="646" alt="image" src="https://github.com/user-attachments/assets/4397bba7-8b29-4669-bc42-e6988e965cff" />

이렇게 하란다. 하니까 본인도 지워버린 TakeDamage 함수를 까먹었었나보다.

다시 추가해달라고 한다.

<img width="715" height="467" alt="image" src="https://github.com/user-attachments/assets/c00c8280-f0f4-4806-9a4f-0f3fb6a1b8e6" />

어느정도 적을 만들면 되고, 탄막 다양성도 내가 추가하면 되는 상태가 되었다!

이제 필요한건 플레이어 본인의 Hp현황과 나중에 추가할 상점의 기능을 하기위한 코인이라는 기능을

추가할 것이다.

### Hp 시스템과 Coin

이 두부분은 UI부분이다. 그래서 기존과 많이 다를 줄 알았는데, 또 그건 아니더라ㅋㅋ

명령어를 익숙하게 입력했슴.

<img width="601" height="105" alt="image" src="https://github.com/user-attachments/assets/f451e722-b36d-492c-8ac6-dba5bf7977f3" />

그러니까 얘가 또 코드를 쫘악 뱉는게 아닌가?

열심히 받아 적었찌ㅎ

**GameManager.cs(코인관리)**
```
using UnityEngine;
using TMPro;

public class GameManager : MonoBehaviour
{
    public static GameManager Instance;

    [Header("코인")]
    public int coin = 0;
    public TextMeshProUGUI coinText;

    void Awake()
    {
        Instance = this;
    }

    public void AddCoin(int amount)
    {
        coin += amount;
        UpdateCoinUI();
    }

    void UpdateCoinUI()
    {
        if (coinText != null)
            coinText.text = $"Coin: {coin}";
    }
}
```

**HealthBar.cs(Hp바 관리)**

```
using UnityEngine;
using UnityEngine.UI;

public class HealthBar : MonoBehaviour
{
    public Slider hpSlider;
    private Player player;

    void Start()
    {
        player = FindObjectOfType<Player>();

        if (hpSlider != null && player != null)
        {
            hpSlider.maxValue = player.maxHp;
            hpSlider.value = player.maxHp;
        }
    }

    void Update()
    {
        if (hpSlider != null && player != null)
        {
            hpSlider.value = player.GetCurrentHp();
        }
    }
}
```

**EnemyBase.cs 수정**

```
protected virtual void OnDeath()
{
    // 코인 추가
    if (GameManager.Instance != null)
        GameManager.Instance.AddCoin(3);

    Destroy(gameObject);
}
```

이 후, 유니티 세팅까지 받아냈다.

<img width="717" height="383" alt="image" src="https://github.com/user-attachments/assets/1f66b4f1-dd64-4e2c-9e2c-f431e3417df7" />

<img width="720" height="248" alt="image" src="https://github.com/user-attachments/assets/a7fd78eb-d2e9-42a5-b441-b5769b9b7906" />

<img width="722" height="284" alt="image" src="https://github.com/user-attachments/assets/8415fb76-739d-47ed-b173-f1934e555b2d" />

그리고, Hp 바의 위치나 UI의 위치를 어떻게 설정 하는지에 대해서도 알게되었다.

이러니까 또 괜찮아진거같네ㅋㅋ

<img width="1100" height="504" alt="image" src="https://github.com/user-attachments/assets/aee1d29c-72e9-4668-86bf-d801e47f4db8" />

아직 허접하지만, 게임 화면이다. 어느정도 있을건 다 있는느낌이랄까(아님)

### 스테이지 데이터 구조

이젠 내부의 적들과 탄막 데미지 등등을 구현했으니까, 스테이지라는 것을 만들어 보기로 한다.

일단 스테이지의 데이터 구조를 짜야한다.

**StageData.cs(스테이지 데이터 구조)**
```
using UnityEngine;

[CreateAssetMenu(fileName = "StageData", menuName = "Game/StageData")]
public class StageData : ScriptableObject
{
    [Header("스테이지 정보")]
    public string stageName;
    public float stageDuration; // 보스 등장까지 걸리는 시간 (초)

    [Header("적 등장 목록")]
    public EnemySpawnEvent[] spawnEvents;

    [Header("보스")]
    public GameObject bossPrefab;
}

[System.Serializable]
public class EnemySpawnEvent
{
    public GameObject enemyPrefab;   // 어떤 적?
    public float spawnTime;          // 몇 초에 등장?
    public Vector2 spawnPosition;    // 어디서 등장?
    public bool isStationary;        // true = 자리잡고 탄막 / false = 지나가는 적
}
```

**StageManager.cs**
```
using UnityEngine;
using System.Collections;

public class StageManager : MonoBehaviour
{
    public static StageManager Instance;

    [Header("스테이지 데이터")]
    public StageData currentStage;

    private float stageTimer = 0f;
    private bool stageStarted = false;
    private bool bossSpawned = false;

    void Awake()
    {
        Instance = this;
    }

    void Start()
    {
        StartStage();
    }

    public void StartStage()
    {
        stageTimer = 0f;
        stageStarted = true;
        bossSpawned = false;

        // 모든 적 등장 이벤트 코루틴 시작
        foreach (var spawnEvent in currentStage.spawnEvents)
        {
            StartCoroutine(SpawnEnemyAtTime(spawnEvent));
        }
    }

    void Update()
    {
        if (!stageStarted) return;

        stageTimer += Time.deltaTime;

        // 시간 다 되면 보스 등장
        if (!bossSpawned && stageTimer >= currentStage.stageDuration)
        {
            bossSpawned = true;
            StartCoroutine(SpawnBoss());
        }
    }

    IEnumerator SpawnEnemyAtTime(EnemySpawnEvent spawnEvent)
    {
        yield return new WaitForSeconds(spawnEvent.spawnTime);

        if (spawnEvent.enemyPrefab == null) yield break;

        GameObject enemy = Instantiate(
            spawnEvent.enemyPrefab,
            spawnEvent.spawnPosition,
            Quaternion.identity
        );

        // 자리잡는 적이면 이동 멈추게
        EnemyBase eb = enemy.GetComponent<EnemyBase>();
        if (eb != null) eb.isStationary = spawnEvent.isStationary;
    }

    IEnumerator SpawnBoss()
    {
        // 잠깐 텀 주고 보스 등장
        yield return new WaitForSeconds(2f);

        if (currentStage.bossPrefab != null)
        {
            Instantiate(currentStage.bossPrefab, new Vector3(6f, 0f, 0f), Quaternion.identity);
            Debug.Log("보스 등장!");
        }
    }

    public void StageClear()
    {
        stageStarted = false;
        Debug.Log("스테이지 클리어!");
        // 나중에 씬 전환 연결
    }
}
```

**StageBase.cs 수정**
<img width="716" height="186" alt="image" src="https://github.com/user-attachments/assets/bd7c3751-6348-4658-a357-ce92a65738ef" />
```
protected override IEnumerator MoveRoutine()
{
    if (isStationary) yield break; // 고정 적이면 이동 안 함

    // 기존 이동 코드
    while (true)
    {
        transform.Translate(Vector2.left * moveSpeed * Time.deltaTime, Space.World);
        if (transform.position.x < -Camera.main.orthographicSize * Camera.main.aspect - 2f)
            Destroy(gameObject);
        yield return null;
    }
}
```

그 후, 유니티 세팅을 한다.
<img width="715" height="550" alt="image" src="https://github.com/user-attachments/assets/3d878420-eaec-4d0c-9f4e-2b8023959883" />

휴, 이제야 어느정도 숨이 트인다...

자잘한 오류가 있긴한데, 말해주면 다 고쳐주더라. 이게 바이브 코딩이지ㅋ

이제 뭐 또 여러가지 말하는데, 나는 적군을 더 다양하게 추가하고 싶었다.

그래서 여러가지 탄막의 종류를 만들어 달라했다.

하나의 적은 플레이어를 조준해서 발사하고, 다른 적은 나선형 패턴, 다른적은 위아래로 퍼지는패턴을 주더라.

아 그리고, 저번에 스폰매니저를 이용해서 적군이 랜덤으로 등장하게 했는데,

이 기능이 이제 필요없어져서, 물어봤더니, 지워도 상관없다더라. 그래서 없앴씀!

없앤 후에 진행하는데, 아니... 적군이 천천히 나타나는게 아니라, 갑자기 뿅하고 지정한 위치에 생기는게 아닌가.

하... 이건 아니야.

<img width="587" height="48" alt="image" src="https://github.com/user-attachments/assets/a0bafcae-956d-4316-8c55-3f9b75b27ba2" />

바로 겐세이 넣기

<img width="734" height="188" alt="image" src="https://github.com/user-attachments/assets/6002ad22-26af-4c0b-aecc-8c2736671e6b" />
<img width="603" height="614" alt="image" src="https://github.com/user-attachments/assets/450958f4-6e9c-4cbf-9d11-f86ec998a6f8" />

스폰매니저 수정까지
<img width="686" height="524" alt="image" src="https://github.com/user-attachments/assets/a60dcce2-63f1-406b-bcc4-f9dbde8679a7" />

그리고 enemyB까지 나혼자의 힘으로!!!!!!!!!!!!!!!!!!!!!!!!! 만들었다.

물론 cs코드는 들고왔지만..^^ 나머지 설정들ㅎ

이러고 국취제 이슈로 멘탈갈려서 도망쳤다. 그래도 나름 많이 했자나 한잔해

0422 끗

## 0423 시작

사실 어제 정리도 안하고 도망쳐서 오전 수업 시작한지 좀 됬는데 이제 적기 시작한다. 에효;

저번에 하다 만 적군들의 다양한 패턴들이다.

### 패턴

**EnemyA.cs (플레이어 조준 발사)**
```
using UnityEngine;
using System.Collections;

public class EnemyA : EnemyBase
{
    [Header("EnemyA 이동")]
    public float moveSpeed = 2f;

    protected override IEnumerator MoveRoutine()
    {
        if (isStationary) yield break;

        while (true)
        {
            transform.Translate(Vector2.left * moveSpeed * Time.deltaTime, Space.World);

            if (transform.position.x < -Camera.main.orthographicSize * Camera.main.aspect - 2f)
                Destroy(gameObject);

            yield return null;
        }
    }

    protected override IEnumerator ShootRoutine()
    {
        yield return new WaitForSeconds(1f);

        while (true)
        {
            // 플레이어 방향 계산
            GameObject player = GameObject.FindGameObjectWithTag("Player");
            if (player != null)
            {
                Vector2 dir = (player.transform.position - transform.position).normalized;
                FireBullet(dir);
            }

            yield return new WaitForSeconds(1.5f);
        }
    }
}
```
**EnemyB.cs (나선형 회전 발사)**
```
using UnityEngine;
using System.Collections;

public class EnemyB : EnemyBase
{
    [Header("EnemyB 이동")]
    public float moveSpeed = 1.5f;

    [Header("나선형 설정")]
    public float rotateSpeed = 60f;  // 회전 속도 (도/초)
    public int bulletCount = 3;      // 동시에 발사할 탄 수

    private float currentAngle = 0f;

    protected override IEnumerator MoveRoutine()
    {
        if (isStationary) yield break;

        while (true)
        {
            transform.Translate(Vector2.left * moveSpeed * Time.deltaTime, Space.World);

            if (transform.position.x < -Camera.main.orthographicSize * Camera.main.aspect - 2f)
                Destroy(gameObject);

            yield return null;
        }
    }

    protected override IEnumerator ShootRoutine()
    {
        yield return new WaitForSeconds(1f);

        while (true)
        {
            // 여러 방향으로 나선형 발사
            for (int i = 0; i < bulletCount; i++)
            {
                float angle = currentAngle + (360f / bulletCount) * i;
                Vector2 dir = new Vector2(
                    Mathf.Cos(angle * Mathf.Deg2Rad),
                    Mathf.Sin(angle * Mathf.Deg2Rad)
                );
                FireBullet(dir);
            }

            currentAngle += rotateSpeed * 0.1f;
            yield return new WaitForSeconds(0.1f);
        }
    }
}
```
**EnemyC.cs (위아래로 퍼지는 패턴)**
```
using UnityEngine;
using System.Collections;

public class EnemyC : EnemyBase
{
    [Header("EnemyC 이동")]
    public float moveSpeed = 2f;

    [Header("위아래 패턴 설정")]
    public int bulletCount = 5;      // 발사할 탄 수
    public float spreadAngle = 90f;  // 퍼지는 각도 범위

    protected override IEnumerator MoveRoutine()
    {
        if (isStationary) yield break;

        while (true)
        {
            transform.Translate(Vector2.left * moveSpeed * Time.deltaTime, Space.World);

            if (transform.position.x < -Camera.main.orthographicSize * Camera.main.aspect - 2f)
                Destroy(gameObject);

            yield return null;
        }
    }

    protected override IEnumerator ShootRoutine()
    {
        yield return new WaitForSeconds(1f);

        while (true)
        {
            // 위아래로 퍼지게 발사
            for (int i = 0; i < bulletCount; i++)
            {
                float angle = -spreadAngle / 2f + (spreadAngle / (bulletCount - 1)) * i;
                Vector2 dir = Quaternion.Euler(0, 0, angle) * Vector2.left;
                FireBullet(dir);
            }

            yield return new WaitForSeconds(1.5f);
        }
    }
}
```

일단 세개까지만 만들고 구현만 시켜두기로 했다.

## 0427 시작

7ㅐ피곤하다. 0424는 google AI studio로 과제 해결하느라 아예 손도 못댔다.

주말에 좀 했어야했는데, 약속이 있는걸 어떠케><

ㅈㅅ

다시 진행하겠다.
