---
title:  "[Unity_SurvivorGame]7. Inventory클래스"
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

# 1. Inventory
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;
public class Inventory
{
    Item[] itemArray;

    public event Action<Item[]> UpdateInven;
    public Inventory()
    {
        itemArray = new Item[15];
    }
    public void ShowInven()
    {
        UIManager.Instance.ShowInven();
        UpdateInven?.Invoke(itemArray); 
    }
    public void GetItem(Item item)
    {
        for(int i = 0;i<itemArray.Length;i++)
        {
            if(itemArray[i] == null)
            {
                itemArray[i] = item;
                UpdateInven?.Invoke(itemArray);
                break;
            }
        }
    }
    public void MoveItem(int originIndex, int targetIndex)
    {
        Item temp = itemArray[originIndex];
        itemArray[originIndex] = itemArray[targetIndex];
        itemArray[targetIndex] = temp;

        UpdateInven(itemArray);
    }
}
```
## 1-1. delegate
* 함수를 집어넣어서 사용한다
* 다른class에 있는 private함수도 넣어서 사용 할 수 있다.