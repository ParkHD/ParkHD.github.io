---
title:  "[Unity_SurvivorGame]2. Object(상대)와 상호작용"
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

# 1. Iinteraction 인터페이스
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public interface Iinteraction
{
    ITEM_TYPE GetName();
    void OnInteract();
}
```

# 2. PlayerInteract 스크립트
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerInteract : MonoBehaviour
{
    [SerializeField] Transform rayPivot;
    [SerializeField] float interactRange;
    [SerializeField] LayerMask targetLayer;

    public static string TargetName
    {
        get;
        private set;
    }
    // Update is called once per frame
    void Update()
    {
        Search();
    }
    void Search()
    {
        Ray ray = new Ray(rayPivot.position, rayPivot.forward);
        RaycastHit hit;

        Debug.DrawRay(rayPivot.position, rayPivot.forward * interactRange, Color.red);
        if (Physics.Raycast(ray, out hit, interactRange, targetLayer))
        {
            Iinteraction target = hit.transform.GetComponent<Iinteraction>();
            if (target != null)
            {
                TargetName = target.GetName().ToString();
                if(Input.GetKeyDown(KeyCode.F))
                {
                    target.OnInteract();
                }
            }
        }
        else
        {
            TargetName = null;
        }
    }
}
```
## 2-1. Ray(Vector3 origin, Vector3 direction)
* origin위치에서 direction방향으로 ray를 쏜다.

## 2-2. RaycastHit
* ray의 저장소

## 2-3. Physics.Raycast(Ray ray, out RaycastHit hitinfo, float maxDistance, int layerMask)
* ray를 maxDistance만큼 쏴서 Layer가 layerMask인것을 hit에 저장한다.


