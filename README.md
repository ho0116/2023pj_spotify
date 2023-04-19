# spotify 음악앱 리뷰 감성분석 :musical_note:
MobileBert를 이용하여 리뷰 긍부정을 예측해보는 프로젝트

## 1. 개요

### 1.1 문제정의
음악은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. spotify가 다른 스트리밍 앱들보다 경쟁력이 있는지 알기 위해 Kaggle에서 제공하는 spotify 앱 리뷰 데이터를 바탕으로 리뷰의 긍정 또는 부정을 예측하는 인공지능 모델을 개발하고자 한다.

### 1.2 spotify 리뷰의 영향력
사용자들이 어떤 기능이나 서비스를 좋아하는지, 어떤 부분에서 경쟁사와 차별화되는지 등을 파악할 수 있다. 이를 통해 Spotify는 경쟁사와의 차별화된 서비스를 제공하고 음악 스트리밍 시장에서의 경쟁력을 강화할 수 있다. 또한 사용자들의 리뷰를 통해 Spotify의 브랜드 이미지와 고객 인식이 형성될 수 있다. 긍정적인 리뷰는 Spotify의 이미지를 향상시키고 브랜드에 대한 고객들의 신뢰를 증대시킬 수 있다. 부정적인 리뷰는 Spotify가 개선해야 할 부분을 도출하고 이를 통해 사용자들에게 더 나은 서비스를 제공하기 위한 노력을 보여줄 수 있다.

### 1.3 데이터 출처
Kaggle에서 Spotify App Reviews(https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022) 데이터를 사용했다.

## 2. 데이터

### 2.1 구성
|데이터명|설명|
|---|---|
|Time_submitted|리뷰 제출 시간|
|Review|리뷰|
|Rating|평점|
|Total_thumbsup|도움된 수|
|Reply|리뷰 재응답|

6만여 개의 리뷰가 있으며 1점부터 5점으로 구성되어 있다.
<div><img src = "https://user-images.githubusercontent.com/85285367/232650843-7b7cc531-297b-48a8-9946-26046b172f31.png" width="350"></div>
