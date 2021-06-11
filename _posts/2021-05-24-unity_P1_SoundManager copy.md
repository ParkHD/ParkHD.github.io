---
title:  "[Unity_Project1]2. 사운드(배경음악, 효과음) 재생"
excerpt: "카테고리별로 게시글 정리하기!"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-05-24
last_modified_at: 2021-05-24
---

# 1. SoundManager(전체적인 사운드 관리)

``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SoundManager : MonoBehaviour
{
    private static SoundManager instance;
    public static SoundManager Instance
    {
        get
        {
            return instance;
        }
    }
    AudioSource audio;

    [SerializeField] AudioClip[] bgmArray;
    [SerializeField] AudioClip[] sfxArray;
    [SerializeField] GameObject soundObject;
    private string bgmName;
    private void Awake()
    {
        instance = this;
        audio = GetComponent<AudioSource>();
        bgmName = "musicbox";
    }
    private void Start()
    {
        PlayBGM(bgmName);
    }
    public void PlayBGM(string clip)
    {
        for(int i = 0;i<bgmArray.Length;i++)
        {
            if(bgmArray[i].name == clip)
            {
                audio.clip = bgmArray[i];
                audio.Play();
                break;
            }
        }
    }
    public void PlaySFX(string clip)
    {
        for(int i = 0;i< sfxArray.Length;i++)
        {
            if(sfxArray[i].name == clip)
            {
                Instantiate(soundObject).GetComponent<SfxManager>().PlaySfx(sfxArray[i]);
            }
        }
    }
}
```

## 1-1. AudioSource
> * ### .clip : 오디오 클립
> * ### .Play() : 오디오 재생

## 1-2. Instantiate(Object)
* Object를 생성

# 2. sfxManager(효과음 관리)

``` c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SfxManager : MonoBehaviour
{
    AudioSource audio;
    // 효과음이 재생되기전에 Destroy방지.
    bool isSet; 
    private void Awake()
    {
        audio = GetComponent<AudioSource>();
    }
    private void Update()
    {
        if(isSet && !audio.isPlaying)
        {
            Destroy(gameObject);
        }
    }
    public void PlaySfx(AudioClip clip)
    {
        isSet = true;
        audio.clip = clip;
        audio.Play();
    }
}
```
## 2-1. AudioSource
> * ### .isPlaying() : 현재 노래가 재생되고 있는지

## 2-2. Destroy(object)
* object 제거