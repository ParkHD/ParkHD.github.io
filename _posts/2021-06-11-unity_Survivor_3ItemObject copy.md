---
title:  "[Unity_SurvivorGame]3. 아이템 오브젝트 및 Ammo 오브젝트"
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
using UnityEngine.UI;

public enum ITEM_TYPE
{
    None = -1,
    Ammo5_56mm,
    Ammo7_76mm,
}
[System.Serializable]
public class Item
{
    [SerializeField] ITEM_TYPE name;
    [SerializeField] Sprite image;
    [SerializeField] int count;
    [SerializeField] string info;
    public ITEM_TYPE Name => name;
    public int Count => count;
    public Sprite ItemImage => image;
    public string Info => info;
    public Item(Item item)
    {
        name = item.name;
        count = item.count;
        image = item.image;
        info = item.info;
    }
}
public class ItemObject : MonoBehaviour
{
    [SerializeField] Item item;
    public void OnInteract()
    {
        Debug.Log(item.Name.ToString() + "획득");
        PlayerState.Instance.GetItem(item);
        Destroy(gameObject);
    }
    public ITEM_TYPE GetName()
    {
        return item.Name;
    }
}

```

## 1-1. [System.Serializable]
* class는 [SerializeField]만 하면 적용이 안된다. 
* class위에 [System.Serializable] 추가해준다.


# 2. AmmoObject
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Ammo : Item
{
    public Ammo(Ammo ammo)
        : base(ammo)
    {

    }
}

public class AmmoObject : ItemObject, Iinteraction
{
    
}
```