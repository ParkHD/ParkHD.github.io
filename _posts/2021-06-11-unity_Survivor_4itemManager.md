---
title:  "[Unity_SurvivorGame]4. ItemManager"
excerpt: "아이템 생성 관리하는 Script"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-06-11
last_modified_at: 2021-06-11
---

# 1. ItemManager
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ItemManager : Singleton<ItemManager>
{
    [SerializeField] ItemObject[] itemArray;

    public ItemObject MakeItem(ITEM_TYPE itemName)
    {
        for(int i = 0;i<itemArray.Length;i++)
        {
            if(itemArray[i].GetName() == itemName)
            {
                return Instantiate(itemArray[i]);
            }
        }
        return null;
    }
}

```
