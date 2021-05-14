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

# 1. The minimal-mistakes-jekyll theme could not be found. (Jekyll::Errors::MissingDependencyException)  

Geimfile에 
{{gem "minimal-mistakes-jekyll"}}추가

cmd창에 bundle install

완료