---
title:  "[Unity_SurvivorGame]8. PlayerState"
excerpt: ""

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-06-11
last_modified_at: 2021-06-11
---

# 1. PlayerState
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;

public class PlayerState : Singleton<PlayerState>
{
    Inventory inven;
    public Inventory Inven => inven;

    private void Awake()
    {
        base.Awake();
        inven = new Inventory();
    }
    private void Update()
    {
        if (Input.GetKeyDown(KeyCode.I))
        {
            ShowInven();
        }
    }
    private void ShowInven()
    {
        inven.ShowInven();
    }
    public void GetItem(Item item)
    {
        inven.GetItem(item);
    }

}
```
