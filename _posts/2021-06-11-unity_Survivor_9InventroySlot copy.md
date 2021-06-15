---
title:  "[Unity_SurvivorGame]9. 인벤토리 만들기(InventorySlot)"
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

# 1. InventorySlot
``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using System;

public class InventorySlot : MonoBehaviour
{
    Item item;

    [SerializeField] Image selectedImage;
    [SerializeField] Image itemImage;
    [SerializeField] Text itemCount;

    public event Action<Item> ShowInfo;
    public event Action ClearInfo;
    public event Action<Item> DragBegin;
    public event Action Dragging;
    public event Action DragEnd;

    public static int targetIndex;
    public static int originIndex;

    private void OnEnable()
    {
        if (selectedImage == null)
            return;
        selectedImage.enabled = false;
    }
    public void OnCursorEnter()
    {
        targetIndex = transform.GetSiblingIndex();
        selectedImage.enabled = true;
        ShowInfo(item);
    }
    public void OnCursorExit()
    {
        selectedImage.enabled = false;
        ClearInfo();
    }
    public void OnDragBegin()
    {
        originIndex = transform.GetSiblingIndex();
        DragBegin(item);
    }
    public void OnDragging()
    {
        Dragging();
    }
    public void OnDragEnd()
    {
        DragEnd();
        PlayerState.Instance.Inven.MoveItem(targetIndex, originIndex);
    }

    public void SetUp(Item item)
    {
        this.item = item;
        if (item == null)
        {
            Clear();
            return;
        }
        itemImage.enabled = true;

        itemImage.sprite = item.ItemImage;
        itemCount.text = item.Count > 1 ? item.Count.ToString() : "";
    }
    public void Clear()
    {
        itemImage.enabled = false;
        itemCount.text = "";
    }
}
```
> **EventTrigger**컴포넌트를 사용하였다.

> delegate를 사용함으로써 OnCursorEnter()가 호출될때 InventoryUI.ShowInfo도 호출된다.
## 1-1 Image.enabled
* Image를 활성화 설정

## 2-2 Text.text
* TextUi에 text를 수정한다.