---
title:  "[Unity_SurvivorGame]1. 플레이어 이동 및 시야회전"
excerpt: "CharacterController, "

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-06-11
last_modified_at: 2021-06-11
---

# 1. ItemObject

``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [SerializeField] float moveSpeed;
    [SerializeField] float turnSpeed;
    [SerializeField] new Camera camera;
    [SerializeField] float LookUpMax;
    [SerializeField] float LookUpMin; // 시야가 얼마나 위로 가는지

    CharacterController controller;

    private void Awake()
    {
        controller = GetComponent<CharacterController>();
    }
    private void Start()
    {
        Cursor.lockState = CursorLockMode.Locked;
    }
    private void Update()
    {
        Move();
        Look();
    }
    void Move()
    {
        if(Input.anyKey)
        {
            controller.Move(transform.forward * Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime);
            controller.Move(transform.right * Input.GetAxis("Horizontal") * moveSpeed * Time.deltaTime);
        }
    }

    float RotationX;
    void Look()
    {
        transform.Rotate(Vector3.up * Input.GetAxis("Mouse X") * turnSpeed);

        float lookUp = Input.GetAxis("Mouse Y") * turnSpeed;
        RotationX += lookUp;
        RotationX = Mathf.Clamp(RotationX, LookUpMin, LookUpMax);
        camera.transform.localRotation = Quaternion.Euler(Vector3.left * RotationX);
    }
}
```

## 1-1. CharacterController
* unity 자체 컴포넌트
> * ### .Move(Vector3 vec) : vec방향으로 Object를 이동시킨다.

## 1-2. Cursor.lockState
* 커서를 자유롭게 둘건지 잠글건지 설정
> * CursorLockMode.Locked : 커서를 잠근다.
> * CursorLockMode.None : 커서를 자유롭게 푼다.

## 1-3. transform.Rotate(Vector3 vec)
* vec값만큼 회전한다.

## 1-4. transfoem.Rotation(Quaternion q)
* Quaternion값을 회전값으로 받는다
* Quaternion로 회전한다.
> * .localRotation : 일반 Rotation은 속해있는 상위 Object에 영향을 받지만 local은 자체 회전값으로 상위 Object의 영향을 받지 않는다.

## 1-5. Quaternion
* vector3는 사람용 언어이고 Quaternion은 기계용 언어이다.
> * .Euler(Vector3 vec) : vector를 Quaternion으로 바꿔준다 

## 1-6 Mathf.Clamp(float x, float min, float max)
* x의 최댓값 및 최솟값 설정.