---
title:  "블로그 카테고리(collections)"
excerpt: "카테고리별로 게시글 정리하기!"

categories:
  - Blog
tags:
  - [categories]

toc: true
toc_sticky: true
date: 2021-05-16
last_modified_at: 2021-05-16
---
## 1. 카테고리 폴더를 만들자
* 카테고리 분류하여 글들을 넣을 _posts-blogs 폴더를 만든다  

## 2. _pages 폴더에 페이지(카테고리) 추가하기 
* _pages폴더가 없다면 폴더를 만들어준다.<br>

* _pages폴더안에 collection-blog.md를 만들어준다  
(md파일 이름은 아무거나 상관없다.)  
* md파일 내용은 아래처럼 맞춰준다.
```
---
title: Custom & Div Blog 
layout: collection
permalink: /blogdiv/
collection: posts-blogs
entries_layout: grid
classes: wide
---
```


## 3. _config.yml 에 추가하기
``` 
collections:
  posts-blogs:
    permalink: /:collection/:path/
    output: true

# Defaults
defaults:
  # _posts-blogs
  - scope:
      path: ""
      type: posts-blogs
    values:
      layout: single
      author_profile: true
      share: true
      sidebar:
        nav: "main"
```
## 4. 확인하기 
[1번에서 만든 폴더](#1.-카테고리-폴더를-만들자) 에다가 아무 글을 넣고 
(자기주소).github.io/blogdiv/에 들어가봐서 있는지 확인 ㄱㄱ  
확인할수 있다.

