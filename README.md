# Spotify App 리뷰 감성분석 :musical_note:
<div><img src ="https://user-images.githubusercontent.com/85285367/235826775-224c4b7c-57b3-4e1d-b13e-49849cb86cbd.png"></div>


<div>
MobileBert를 이용하여 Google Play Store의 Spotify App 리뷰 긍부정을 예측해보는 프로젝트
    
<img src="https://img.shields.io/badge/PyTorch-E34F26?style=flat-square&logo=PyTorch&logoColor=white"/> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white"/>
</div>

## 1. 개요

### 1.1 문제정의
Google Play Store는 음악, 동영상, 책, 안드로이드 응용 프로그램, 게임을 포함한 온라인 스토어와 클라우드 미디어 플레이어를 아우르는 구글의 디지털 콘텐츠 서비스이다. 안드로이드에서 사용할 수 있는데 2023년 4월 기준 전 세계 모바일 운영체제(OS) 시장에서 안드로이드(Android)의 점유율은 약 68.79% 이다.[1]  
음악감상은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. 스트리밍 서비스를 지원하는 spotify는 현재 180여개 국가에서 서비스를 제공하고 있다. IT 시장조사업체 미디어리서치(MIDiA)에 따르면 2022년 상반기 기준 spotify는 전 세계 음악 스트리밍 서비스 시장의 30% 가량(구독자 1억8780만명)을 차지하고 있다.[2] spotify가 다른 스트리밍 앱들보다 경쟁력이 있는지 알기 위해 Kaggle에서 제공하는 spotify app 리뷰 데이터를 바탕으로 리뷰의 긍정 또는 부정을 예측하는 인공지능 모델을 개발하고자 한다.

### 1.2 spotify 리뷰의 영향력
사용자들이 어떤 기능이나 서비스를 좋아하는지, 어떤 부분에서 경쟁사와 차별화되는지 등을 파악할 수 있다. 이를 통해 Spotify는 경쟁사와의 차별화된 서비스를 제공하고 음악 스트리밍 시장에서의 경쟁력을 강화할 수 있다. 또한 사용자들의 리뷰를 통해 Spotify의 브랜드 이미지와 고객 인식이 형성될 수 있다. 긍정적인 리뷰는 Spotify의 이미지를 향상시키고 브랜드에 대한 고객들의 신뢰를 증대시킬 수 있다. 부정적인 리뷰는 Spotify가 개선해야 할 부분을 도출하고 이를 통해 사용자들에게 더 나은 서비스를 제공하기 위한 노력을 보여줄 수 있다.

### 1.3 데이터 출처
Kaggle [Spotify App(Google Play Store)](https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022 "Spotify App")

## 2. 데이터

### 2.1 구성
- 데이터명

|Time_submitted|Review|Rating|Total_thumbsup|Reply|
|---|---|---|---|---|
|리뷰 제출 시간|리뷰|평점|도움된 수|댓글|

- 데이터

||Time_submitted|Review|Rating|Total_thumbsup|Reply|
|---|---|---|---|---|---|
|0|2022-07-09 15:00:00|Great music service, the audio is higy quality..|5|2|NaN|
|1|2022-07-09 14:21:22|Please ignore previous negative rating..|5|1|NaN|
|2|2022-07-09 13:27:32|This pop-up "Get the best Spotify eperience..|4|0|NaN|
|...|...|...|...|...|...|
|61591|2022-01-01 01:02:29|This app would be good if not for it..|2|10|NaN|
|61592|2022-01-01 00:49:23|The app is good hard to navigate and won't..|2|1|NaN|
|61593|2022-01-01 00:19:09|Its good but sometimes it doesnt load the..|4|0|NaN|

6만여 개의 리뷰가 있으며 1점부터 5점으로 구성되어 있다.
      
<div><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/75df662c-fa0e-4223-97d7-5fb90d922745" width="350"></div>


1, 2점은 부정, 4, 5점은 긍정으로 분류했다.

<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/71197cdc-8eaf-47fe-b114-35d4333ec7c1" width="350"></div>


리뷰 문장 20자 이상 길이
<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/b02823cb-472b-4c33-a5fc-f010c6eb814d" width="350"></div>






### ---출처---
[1] <a href="https://gs.statcounter.com/os-market-share/mobile/worldwide/">안드로이드</a>  
[2] <a href="https://biz.chosun.com/it-science/ict/2023/03/21/P6ZEG3RF2VDU7K4R2MO3B6S5BY">미디어리서치(MIDiA)</a>
