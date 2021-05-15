---
title:  "[Jekyll] 블로그 포스팅하는 방법"
excerpt: "md 파일에 마크다운 문법으로 작성하여 Github 원격 저장소에 업로드 해보자. 에디터는 Visual Studio code 사용! 로컬 서버에서 확인도 해보자. "

categories:
  - Blog
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2021-05-13
last_modified_at: 2021-05-13
---
# 여기로이동
[동일포스터 내 문단이동](#2연습)
# 0. 비고
# 1. The minimal-mistakes-jekyll theme could not be found. (Jekyll::Errors::MissingDependencyException)  

    Geimfile에 gem "minimal-mistakes-jekyll"추가

    cmd창에 bundle install

    완료
  
## 2.연습
* ㅇㅇ<br><br>
* ___ss___
- **ss**
+ **abc *def* ghi**
> A
>> B
>>> C
>>>> D
>>>>> E

[유튜브로 이동](https://youtube.com "마우스 올렸니?")<br>
<https://youtube.com><br>
[동일포스터 내 문단이동](#여기로이동)
> #제목

[동일포스터 내 문단이동](#2연습)

```c++
int x;
cout << x;
```