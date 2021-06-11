---
title:  "[Unity_Project1]0. 배경 및 지형물 생성(TileMap)"
excerpt: "카테고리별로 게시글 정리하기!"

categories:
  - Unity
tags:
  - [category]

toc: true
toc_sticky: true
date: 2021-05-22
last_modified_at: 2021-05-22
---
## 1. 하이어라키창에 TileMap생성
<img src="https://user-images.githubusercontent.com/76206050/119224664-77f56400-bb3a-11eb-85e1-1f35eb81d96b.png" width="100%" height="700">

* 2DObject -> TileMap -> Rectangular 만든다

## 2. Open Tile Palette
<img src="https://user-images.githubusercontent.com/76206050/119224783-11247a80-bb3b-11eb-97c5-e0ec81d44268.png" width="800" height="500">

* Scene화면 오른쪽 아래 팔레트 열기

## 3. Create New Palette

<img src="https://user-images.githubusercontent.com/76206050/119224824-53e65280-bb3b-11eb-8160-5988038a9da3.png" width="800" height="500">  
<br>
<img src="https://user-images.githubusercontent.com/76206050/119224890-9a3bb180-bb3b-11eb-8909-a718354dc4b6.png" width="800" height="500">

* tileset 파일내용들을 Palette에 드래그 해준다

<img src="https://user-images.githubusercontent.com/76206050/119224825-55b01600-bb3b-11eb-9bc6-d9e9d23bf24e.png" width="800" height="500">

* 최종적으로 이 화면이 나온다.

## 4. 꾸미기
<img src="https://user-images.githubusercontent.com/76206050/119224826-56e14300-bb3b-11eb-86ac-619bdd5168e1.png" width="800" height="500">

* 알아서 꾸미면 된다.

## 5. collider설정
### 5-1. Tilemap Collider 2D
* 지형지물이므로 플레이어가 통과하지 않도록 collider를 넣어준다

### 5-2. Composite Collider 2D
* tilemap Collider만 사용할경우 타일 중간중간 틈이 발생한다 따라서 오류가 발생할 수 있으므로
Composite Collider를 이용하여 타일들을 하나의 콜리더로 만들어 사용한다.
* 1. Composite Collider 2D를 Add해준다.
* 2. Tilemap Collider 2D에 Used By Composite를 체크해준다.

<img src="https://user-images.githubusercontent.com/76206050/119224828-5779d980-bb3b-11eb-8b5e-3b82b9ac81be.png" width="800" height="500">

## 6. 타일 collider설정(Sprite Editor)
<img src="https://user-images.githubusercontent.com/76206050/119224829-5779d980-bb3b-11eb-8e9d-d80b3d03330d.png" width="800" height="500">

* 하지만 이렇게 하면 수풀도 Collider처리로 안으로 들어가는것이 아닌 위에 올라타는 문제가 생긴다 따라서 수풀타일을 수정해줘야 한다.

<img src="https://user-images.githubusercontent.com/76206050/119224830-58127000-bb3b-11eb-8da1-e20681870e14.png" width="800" height="500">

* tileset파일로 가서 Sprite Editor로 들어간다

<img src="https://user-images.githubusercontent.com/76206050/119224831-58127000-bb3b-11eb-80c3-b96cf72f16a9.png" width="800" height="500">

* Custom Physics Shape를 누른다.

<img src="https://user-images.githubusercontent.com/76206050/119225249-a0329200-bb3d-11eb-9db3-8b78aa55d032.png" width="250" height="500">  -> 
<img src="https://user-images.githubusercontent.com/76206050/119225252-a163bf00-bb3d-11eb-9a7f-eaefde84f5a5.png" width="250" height="500">

* 원하는 타일을 누르고 사각형 모양을 드래그하여 내린다 그리고 Apply를 누르고 빠져나온다.

* ***그런다음에 원래있던 하이어라키창에 있는 수정한 타일을 삭제하고 팔레트에 수정한 타일을 다시 넣고 하이어라키창에 다시 넣어야한다. 안그러면 수정이 안된다!!***

## 7. 완성!!
<img src="https://user-images.githubusercontent.com/76206050/119224832-58ab0680-bb3b-11eb-9b3d-73c33dc6fda9.png" width="800" height="500">

* 바닥은 올라가지만 수풀에는 들어가는것을 확인 할 수 있다!!