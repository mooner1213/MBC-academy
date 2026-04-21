# 혼자 게임 만들어보기

아무것도 모르니까 ai를 이용해서 만들어본다.

2d 횡스크롤 슈팅게임을 만들어 보겠다.

일단 어떤걸 만들고 싶은지를 최대한 설명했다. 아참, AI는 Claude ai를 쓰고있다.
<img width="761" height="454" alt="image" src="https://github.com/user-attachments/assets/324a666b-4f1f-472d-b53a-acc0e6c6c6d1" />

일단 플레이어를 만들어야 해서, 대충 2d object를 트라이앵글로 만들어서 플레이어를 대체했다.

그리고 우측으로 돌렸다. 2d 횡스크롤이기때문..

일단 추후에 피격이나 타격을 만들어야하므로 rigidbody 2d 컴포넌트를 추가했다.
<img width="445" height="346" alt="image" src="https://github.com/user-attachments/assets/73ae95a2-25b6-4912-9c53-93c842244053" />

Freeze rotation Z 를 체크했다. 물어보니까, 피격받았을때 회전 할 가능성을 없앤다고 하더라.
<img width="237" height="56" alt="image" src="https://github.com/user-attachments/assets/300831ea-e2c9-4264-af29-e1f41fee7750" />

그 후에, 이것도 추가하라던데
<img width="442" height="253" alt="image" src="https://github.com/user-attachments/assets/f3a1978f-b52d-44cf-b65d-143f6e8bacb3" />

일단 isTrigger를 체크하기 위함이 아닐까? 라고 생각한다.

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
뭐가 많은데, 나중에 추가하기 귀찮아서 기능을 최대한 생각나는대로 넣었다.

이동, 체력, 탄막, 피격, 피격시 무적, 무적시 깜박거림, hp표시 등등... 아마 이것도 모자라겠지

그런데 뭔가 이상했다. 플레이 하니까 방향키로 안움직이는거임;;

그래서 물어봤다.
<img width="739" height="714" alt="image" src="https://github.com/user-attachments/assets/bf684520-d671-4713-b360-751e8ab7b47f" />

**1,2,3,4 전부 아니었다.** 혹시몰라서 하나하나 다 찍어보냈는데, 다른게 없었거든... 당연히 플레이버튼은 눌렀는데 이자식이
<img width="719" height="352" alt="image" src="https://github.com/user-attachments/assets/8b85ce79-cf94-47a3-b304-1d07c3962441" />

**나를 무시하잖슴.**

그래서 플레이를 하고 뭔가 문제가 없나, 찾아보는데,,

플레이 화면 아래쪽에 빨간글씨로 뭔가 떠있는거임!!
<img width="1373" height="40" alt="image" src="https://github.com/user-attachments/assets/ff0a460c-ae61-474f-b333-53f9b5f8473d" />

잘은 안보이겠지만, 뭔가가 잘못되었다는건 알겠음..

그래서 물어보니까,
<img width="715" height="464" alt="image" src="https://github.com/user-attachments/assets/d7d2d9ac-e4ef-4b09-89f4-45e8a7edcdd7" />
라고한다. 1번을 따라서 해보니 바로 해결되었으나,,,

또 다른 **문제**가 생겼다.

아니 플레이어가 우측을 바라보고 있는데, 위 방향키를 누르니 우측으로 돌진하는 것이 아닌가!!!!!!!!!!!!!!!!!

그래서 이것도 물어봐서 해결했다.
<img width="724" height="484" alt="image" src="https://github.com/user-attachments/assets/cac45da6-b029-469d-9aca-82b5059ee3ea" />

역시 ai야 금방 해결해주는구나?

이제는 총알 부분을 한번 만들어 보겠다.
