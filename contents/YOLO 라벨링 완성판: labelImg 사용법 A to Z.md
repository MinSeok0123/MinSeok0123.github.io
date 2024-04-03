---
date: '2024-04-03'
title: 'YOLO 라벨링 완성판: labelImg 사용법 A to Z'
categories: ['Yolo', '이미지라벨링', '커스텀데이터셋', '컴퓨터비전']
summary: 'YOLO 이미지 라벨링이란 무엇인가?
YOLO는 실시간 객체 탐지를 위한 최신 알고리즘이다. YOLO는 You Only Look Once의 줄임말로, 이것은 우리가 한 번만 봐도 이미지를 분석할 수 있다는 효율성을 뜻한다. 그렇다면 이미지 라벨링은 무엇일까? 이는 YOLO 알고리즘의 핵심 과정 중 하나로, 특정 이미지에 대한 정보를 정확하게 태깅하는 작업을 의미한다.'
thumbnail: './image/labelImg.jpeg'
---

# 서론

## YOLO 이미지 라벨링이란 무엇인가?

YOLO는 실시간 객체 탐지를 위한 최신 알고리즘이다. YOLO는 You Only Look Once의 줄임말로, 이것은 우리가 한 번만 봐도 이미지를 분석할 수 있다는 효율성을 뜻한다. 그렇다면 이미지 라벨링은 무엇일까? 이는 YOLO 알고리즘의 핵심 과정 중 하나로, 특정 이미지에 대한 정보를 정확하게 태깅하는 작업을 의미한다.

## 왜 labelImg를 사용하는가?

YOLO를 이용한 이미지 학습에서 핵심은 '데이터셋'이다. 그런데 원하는 데이터셋이 없는 경우, 우리는 직접 데이터셋을 생성해야 한다. 이 과정에서 필요한 도구가 바로 labelImg이다.

labelImg는 이미지에 Bounding Box를 지정하여 라벨링하는 과정을 간편하게 만들어준다. 이를 통해 YOLO를 이용한 사용자 지정 이미지 학습 과정을 원활하게 진행할 수 있는 것이다.

---

# labelImg 설치 가이드

1. labelImg의 GitHub 페이지
   https://github.com/tzutalin/labelImg
   에 접속한다.

![](https://velog.velcdn.com/images/devminsuk/post/1ec54b64-ce3d-4227-9df0-7c2b70f9b03a/image.png)

2. 웹페이지 상단의 'Releases'를 클릭한다.

![](https://velog.velcdn.com/images/devminsuk/post/578b6f81-2688-4bb0-bee9-d7385ca8f6a9/image.png)

3. Windows 환경에서는 'Windows_v1.8.1.zip' 파일을 선택하여 다운로드한다.

![](https://velog.velcdn.com/images/devminsuk/post/af7433a3-03f5-416d-8459-c7bcfd87321e/image.png)

4. 다운로드한 파일을 압축 해제하고, 생성된 `windows_v1.8.1` 디렉토리를 C 혹은 D 드라이브 바로 아래에 위치시킨다.

![](https://velog.velcdn.com/images/devminsuk/post/c63598e7-a366-43c4-a2de-4c4b3593bfc1/image.png)

여기까지 완료했다면 `labelImg.exe` 파일을 실행시켜보자.

<table>
  <tr>
    <td align="center"><img src="https://velog.velcdn.com/images/devminsuk/post/3edac7a4-3b44-4a07-b67f-e7fa3314dec8/image.png" alt="Image 1"></td>
    <td align="center"><img src="https://velog.velcdn.com/images/devminsuk/post/ed669251-5622-490d-89aa-6a40be32286e/image.png" alt="Image 2"></td>
  </tr>
</table>

5. `labelImg.exe` 파일을 실행한다. 창이 두 개 뜨면 '추가 정보' 클릭 후 '실행'을 선택한다.

![](https://velog.velcdn.com/images/devminsuk/post/c6e2eaec-6f0a-4119-9d86-cff40fae39c9/image.png)

정상적으로 실행된다면 다음과 같은 화면을 볼 수 있을텐데, 프로그램을 실행하는 동안에 검은색의 콘솔창을 종료할 경우 프로그램도 함께 종료되기 때문에 주의해야 한다.

# 사용방법

라벨링을 진행하기 전에 먼저 해야 할 일이 있다. 라벨링하고자 하는 class를 정의하고, YOLOv5의 경우 xml이 아닌 txt 파일 형식이 필요하므로, labelImg의 기본값인 xml을 변경해야 한다.

## class 정의

![](https://velog.velcdn.com/images/devminsuk/post/d5144d12-8c35-4473-b1bb-5757299f0d27/image.png)

1. labelImg가 위치한 디렉토리 아래에 있는 'data' 디렉토리로 들어간다.

![](https://velog.velcdn.com/images/devminsuk/post/59665f5d-3039-406b-81fd-223d9a6d651b/image.png)

2. 'predefined_classes.txt' 파일을 열어서 class를 원하는 대로 변경한다.

![](https://velog.velcdn.com/images/devminsuk/post/d27c57b0-3390-42c0-b24b-887575c303f9/image.png)

3. txt 파일에 있는 순서대로 class 번호가 저장되므로, 해당 파일 수정 시 순서에 유의한다.

## 저장 방식 변경

![](https://velog.velcdn.com/images/devminsuk/post/9b60cad3-b74f-47a9-8800-60dedc3f9fac/image.png)

앞서 언급했던 것처럼 라벨링을 진행할 때 저장되는 파일의 형식을 변경해줘야 한다. labelImg 메뉴에서 `PascalVOC` 클릭하여 `YOLO` 변경한다.
labelImg를 실행할 때마다 이 설정을 변경해야 한다.

## 이미지 불러오기

![](https://velog.velcdn.com/images/devminsuk/post/1d646826-8b4c-4cdf-9cc1-38f7154bf2d4/image.png)

이제 `Open Dir`을 통해 이미지가 저장된 폴더를 선택해주자.

## 단축키

이제 라벨링 작업을 진행하면 되는데 라벨링 작업을 진행할 때 유용한 단축키들을 몇 가지 살펴보자.

![](https://velog.velcdn.com/images/devminsuk/post/6b23edc6-08a6-4c1f-b0b5-a85081be2aba/image.png)

### 단축키 사용

- W : 이미지 범위 선택
- A : 이전 이미지
- D : 다음 이미지
- Ctrl + S : 저장

## 라벨링

W를 누른 후 시작점부터 끝점까지 드래그하여 Bounding Box의 영역을 설정하자. 드래그를 마치면, 해당하는 class를 선택하는 창이 나온다. 상단의 검색 기능을 이용해 원하는 class를 빠르게 찾을 수 있다.
![](https://velog.velcdn.com/images/devminsuk/post/6cce1f0a-380f-4d02-bc72-d0a66e2125ae/image.png)

![](https://velog.velcdn.com/images/devminsuk/post/8af10a16-292f-4caf-9c0e-10c6497d44b9/image.png)

드래그를 종료하면 다음과 같이 class를 선택하는 창이 나오는데, 해당하는 class를 선택해주면 된다. 상단의 검색 기능을 포함하고 있으므로 영역을 지정 후 해당하는 class의 첫 글자를 입력하여 빠르게 class를 찾을 수 있다.

![](https://velog.velcdn.com/images/devminsuk/post/e5ad5e0b-0da0-4daa-9b5f-de962d0a560a/image.png)
라벨링된 파일을 살펴보면 다음과 같이 class 번호와 좌표가 저장된 것을 확인할 수 있다.

---

# 번외

## 라벨 저장 위치 설정 방법

![](https://velog.velcdn.com/images/devminsuk/post/a13a7a9c-f8b7-42f3-bbbe-8ab7fedb419c/image.png)

라벨링 작업을 시작하기 전에, 'Open Dir' 버튼을 클릭하여 파일 위치를 선택합니다. 만약 .txt파일을 다른 위치에 저장하고자 하는 경우, 'Change Save Dir'를 클릭하여 원하는 경로로 변경하면 됩니다.

이미지 파일과 동일한 경로에 .txt파일을 저장하고자 하는 경우, 'Change Save Dir'에서 이미지 경로와 동일하게 설정해야 합니다.

---

이제 **열심히 라벨링을 진행하면** 된다.

<img src="https://velog.velcdn.com/images/devminsuk/post/2fe79820-62f9-4420-8177-9193e2df34cc/image.png" width="200">
