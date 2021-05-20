---
title:  "[Unity_Project1]1. 플레이어 이동 및 점프"
excerpt: "카테고리별로 게시글 정리하기!"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-05-20
last_modified_at: 2021-05-20
---
## 1. 플레이어 이동
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
    [SerializeField] float playerSpeed;   // 속력
    private SpriteRenderer playerRenderer;
    private Rigidbody2D playerRigid;

    void Start()
    {
        playerRigid = GetComponent<Rigidbody2D>();
        playerRenderer = GetComponent<SpriteRenderer>();
    }
    void Update()
    {
        Move();
    }
    void Move()
    {
        // 좌우 버튼이 눌렸을 경우
        if (Input.GetButton("Horizontal") == false)
            return;

        // left : -1, right : 1
        float h = Input.GetAxisRaw("Horizontal");
        playerRigid.AddForce(Vector2.right * h, ForceMode2D.Impulse);

        // 계속 힘을 주면 속력이 계속 증가함으로 속력의 최대값을 설정하여 가속이 안 붙게함
        if (playerRigid.velocity.x < -playerSpeed)
            playerRigid.velocity = new Vector2(-playerSpeed, playerRigid.velocity.y);
        else if (playerRigid.velocity.x > playerSpeed)
            playerRigid.velocity = new Vector2(playerSpeed, playerRigid.velocity.y);

        // 방향이 왼쪽 오른쪽에 따라 플레이어의 모습을 바꾸기 위함
        // flipX > true:왼쪽, flase:오른쪽.
        playerRenderer.flipX = (h == -1);
    }
}
```
### 1-1. [SerializeField]
* ***[SerializeField]*** : 클래스 외부에서 참조가 안되지만     ***유니티엔진***  안에서는 참조가능
* private : 클래스 내부에서만 참조가능
* public : 클래스 내부 외부 다 참조가능

### 1-2. SpriteRenderer Component
 * Object의 외형을 담당하는 컴포넌트
> * #### flipX : bool값으로 X값 반전시킬 수 있다

### 1-3. Rigidbody2D Component
* Object의 물리처리를 담당하는 컴포넌트
> * #### AddForce() : Object에 힘 가하기
> * #### velocity : Object에 가해지는 힘의 크기  

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMove : MonoBehaviour
{
    [SerializeField] float playerSpeed;
    [SerializeField] float playerJump;
    private SpriteRenderer playerRenderer;
    private Rigidbody2D playerRigid;
    private Animator playerAni;

    private int MAX_JUMP_COUNT = 2;
    private int jumpCount;

    void Start()
    {
        playerRigid = GetComponent<Rigidbody2D>();
        playerRenderer = GetComponent<SpriteRenderer>();
        playerAni = GetComponent<Animator>();
        jumpCount = MAX_JUMP_COUNT;
    }
    void FixedUpdate()
    {
        CheckGround();
    }

    void Update()
    {
        Move();
        if (Input.GetButtonUp("Horizontal"))
        {
            playerRigid.velocity = new Vector2(0, playerRigid.velocity.y);
            playerAni.SetBool("isRun", false);
        }
        Jump();
    }

    void Move()
    {
        if (Input.GetButton("Horizontal") == false)
            return;

        playerAni.SetBool("isRun", true);

        float h = Input.GetAxisRaw("Horizontal");
        playerRigid.AddForce(Vector2.right * h, ForceMode2D.Impulse);

        if (playerRigid.velocity.x < -playerSpeed)
            playerRigid.velocity = new Vector2(-playerSpeed, playerRigid.velocity.y);
        else if (playerRigid.velocity.x > playerSpeed)
            playerRigid.velocity = new Vector2(playerSpeed, playerRigid.velocity.y);

        // flipX > true:왼쪽, flase:오른쪽.
        playerRenderer.flipX = (h == -1);
    }
    void Jump()
    {
        if (jumpCount <= 0)
            return;
        if(Input.GetButtonUp("Jump"))
        {
            playerRigid.velocity = new Vector2(playerRigid.velocity.x, 0);
            playerRigid.AddForce(Vector2.up * playerJump, ForceMode2D.Impulse);
            jumpCount--;
        }
    }
    void CheckGround()
    {
        playerAni.SetFloat("isJump", playerRigid.velocity.y);

        if (playerRigid.velocity.y > 0)
        {
            playerAni.SetBool("isGround", false);
            return;
        }

        float rayDistance = 0.4f;
        RaycastHit2D hit = Physics2D.Raycast(transform.position, Vector2.down, rayDistance, 1 << LayerMask.NameToLayer("Ground"));
        Debug.DrawRay(transform.position, Vector2.down * rayDistance, Color.red);
        if(hit)
        {
            jumpCount = MAX_JUMP_COUNT;
            playerAni.SetBool("isGround", true);
        }
        else
        {
            playerAni.SetBool("isGround", false);
        }
    }
}

```
