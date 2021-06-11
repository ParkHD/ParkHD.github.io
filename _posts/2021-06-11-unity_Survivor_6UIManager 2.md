---
title:  "[Unity_SurvivorGame]6. UIManager"
excerpt: "전체적인 UI관리"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-06-11
last_modified_at: 2021-06-11
---

# 1. UIManager
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class UIManager : Singleton<UIManager>
{
    [SerializeField] GameObject invenUI;

    public void ShowInven()
    {
        bool isInvenOpen = invenUI.activeSelf;
        Cursor.lockState = isInvenOpen ? CursorLockMode.Locked : CursorLockMode.None;
        invenUI.SetActive(!isInvenOpen);
    }
}

```
> 인벤이 켜져있으면 끄고 꺼져있으면 키게 만들었다  
또한 인벤토리가 켜져있을 때는 cursor가 움직이도록 반대로 꺼지면 다시 cursor를 lock시켰다.

## 1-1. GameObject.activeSelf
* object가 활성화 되었는지 안되었는지 (bool)
