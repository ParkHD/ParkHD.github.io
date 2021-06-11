---
title:  "[Unity_SurvivorGame]5. ItemSpawner"
excerpt: "아이템을 게임씬에 생성하는 Spawner스크립트"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-06-11
last_modified_at: 2021-06-11
---

# 1. ItemSpawner
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ItemSpawner : MonoBehaviour
{
    [SerializeField] ITEM_TYPE itemName;
    [SerializeField] Transform spawnPivot;
    private void Start()
    {
        ItemObject item = ItemManager.Instance.MakeItem(itemName);
        item.transform.position = spawnPivot.position;
    }
}
```
> ItemManager를 통해 아이템을 생성하고 생성위치(SpawnPivot)를 정해준다.
