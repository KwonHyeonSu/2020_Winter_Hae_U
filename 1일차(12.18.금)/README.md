# 2020_Winter_Hae_U

빈 공간에 Capsule과 Plane을 만듭니다.

> rename : Capsule -> Player
> rname : Plane -> Ground

 Camera를 조정하여 플레이어를 위에서 비스듬히 내려다 볼 수 있게 세팅을 완료합니다.

>   **단축키**
> Q : 화면 이동 or 마우스 휠 클릭
> W : Object 이동
> (빨간선 : x축, 초록선 : y축, 파란선 : z축)
> <img src = "../Img/3.PNG" width = "300">
> E : Object 회전
> <img src = "../Img/4.PNG" width = "300">
> R : 오브젝트 크기 조절
> <img src = "../Img/5.PNG" width = "300">
> T : 오브젝트 평면 크기 조절
> <img src = "../Img/6.PNG" width = "300">
<br>


PlayerMoveController.cs 스크립트를 만들고 Player에게 적용시킵니다.

<img src = "../Img/1.PNG" width = "800">

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMoveController : MonoBehaviour
{
    public float h;
    public float v;

    public float playerSpeed = 5.0f;

    public Vector3 dir;

    private void Update()
    {
        h = Input.GetAxis("Horizontal");
        v = Input.GetAxis("Vertical");

        dir = h * Vector3.back + v * Vector3.right;

        this.transform.Translate(dir * playerSpeed * Time.deltaTime);
    }

}

```

플레이어를 따라가게하는 CameraController.cs 스크립트 또한 만들고, Main camera에 적용시킵니다.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraController : MonoBehaviour
{
    public float cameraSpeed = 1.0f;
    public GameObject player;

    public Vector3 dir;
    public Vector3 offset;

    private void Start()
    {
        offset = player.transform.position - this.transform.position;
    }
    private void Update()
    {
        dir = player.transform.position - this.transform.position - offset;

        this.transform.Translate(dir * cameraSpeed * Time.deltaTime, Space.World);
    }
}
```

카메라가 플레이어를 잘 따라가는지 확인해봅니다.

-> cameraSpeed를 Inspector상에서 조정함으로서 게임 중에 적절한 카메라 속도를 찾을 수 있습니다.

<img src = "../Img/2.PNG">