# Spotify App 리뷰 감성분석 :musical_note:
<div><img src ="https://user-images.githubusercontent.com/85285367/235826775-224c4b7c-57b3-4e1d-b13e-49849cb86cbd.png"></div>


<div>
MobileBert를 이용하여 Google Play Store의 Spotify App 리뷰 긍부정을 예측해보는 프로젝트
    
<img src="https://img.shields.io/badge/PyTorch-E34F26?style=flat-square&logo=PyTorch&logoColor=white"/> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white"/>
</div>

## 1. 개요

### 1.1 문제정의
Google Play Store는 음악, 동영상, 책, 안드로이드 응용 프로그램, 게임을 포함한 온라인 스토어와 클라우드 미디어 플레이어를 아우르는 구글의 디지털 콘텐츠 서비스이다. 안드로이드에서 사용할 수 있는데 2023년 4월 기준 전 세계 모바일 운영체제(OS) 시장에서 안드로이드(Android)의 점유율은 약 68.6% 이다. <a href="https://gs.statcounter.com/os-market-share/mobile/worldwide/">[1]</a>  
<img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/92ab9528-3faf-47fd-8ea1-a2db2a80d62d" width="400"/>

평점과 리뷰는 중요하다. 앱과 제공하는 전반적인 서비스에 대한 사용자의 경험은 가치 있는 정량적, 정성적 피드백을 제공한다. 그렇기 때문에 사람들이 Google Play Store에서 어플을 다운로드할지 결정할 때 고려하는 요소 중 하나가 된다. <a href="https://android-developers.googleblog.com/2021/08/making-ratings-and-reviews-better-for.html">[2]</a>  
음악감상은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. 스트리밍 서비스를 지원하는 spotify는 현재 180여개 국가에서 서비스를 제공하고 있다. IT 시장조사업체 미디어리서치(MIDiA)에 따르면 2022년 상반기 기준 spotify는 전 세계 음악 스트리밍 서비스 시장의 30% 가량(구독자 1억8780만명)을 차지하고 있다. <a href="https://biz.chosun.com/it-science/ict/2023/03/21/P6ZEG3RF2VDU7K4R2MO3B6S5BY">[3]</a>  
<img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/fa093c4d-2755-49ba-a4f9-09690ba979f2" width="400"/>  
2023년 3월 31일 기준으로 5억 1,500만 명이 이용하고 있고 Spotify는 거의 모든 연령대 뿐만 아니라 선진국과 개발도상국 시장 모두에서 이용자 수에 대한 큰 성장을 보였다. 이러한 성장의 대부분은 무료 광고 지원 버전의 Spotify 서비스를 사용하는 사람들을 기반으로 한다. 프리미엄 구독은 전년 대비 15% 증가한 2억 1천만 명으로 유럽과 라틴 아메리카를 비롯한 모든 지역에서 우수한 실적을 보였다. <a href="https://newsroom.spotify.com/2023-04-25/spotify-reports-first-quarter-2023-earnings/">[4]</a>  
<img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/08216e11-5597-4fe6-8916-baef580d3df0" width="400">

spotify가 다른 스트리밍 앱들보다 경쟁력이 있는지 알기 위해 Kaggle에서 제공하는 spotify app 리뷰 데이터를 바탕으로 리뷰의 긍정 또는 부정을 예측하는 인공지능 모델을 개발하고자 한다.

### 1.2 spotify 리뷰의 영향력
사용자들이 어떤 기능이나 서비스를 좋아하는지, 어떤 부분에서 경쟁사와 차별화되는지 등을 파악할 수 있다. 이를 통해 Spotify는 경쟁사와의 차별화된 서비스를 제공하고 음악 스트리밍 시장에서의 경쟁력을 강화할 수 있다. 또한 사용자들의 리뷰를 통해 Spotify의 브랜드 이미지와 고객 인식이 형성될 수 있다. 긍정적인 리뷰는 Spotify의 이미지를 향상시키고 브랜드에 대한 고객들의 신뢰를 증대시킬 수 있다. 부정적인 리뷰는 Spotify가 개선해야 할 부분을 도출하고 이를 통해 사용자들에게 더 나은 서비스를 제공하기 위한 노력을 보여줄 수 있다.

### 1.3 데이터 출처
Kaggle [Spotify App(Google Play Store)](https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022 "Spotify App")

## 2. 데이터

### 2.1 원시 데이터
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

6만여 개의 리뷰가 있으며 1점부터 5점으로 구성되어 있다
, 도움된 수를 별점별과 평균값에 대한 그래프를 그려봤다
      
<div><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/86cb68fa-9547-432c-9a86-dc761a41e329" width="400"><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/f2cc7700-2a67-4c2c-8646-5bacd4c2b61c" width="400"></div>



리뷰 문장 20자 이상 길이의 분포도
<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/b4a13bda-e0e1-446a-b0c0-bd6749c1e791" width="400"></div>
100자 전후로 많은 리뷰가 몰려있다

### 2.2 데이터 가공

1, 2점은 부정 4, 5점은 긍정으로 분류했다

<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/9ed9b098-b40e-4856-83f2-74137d95c4c0" width="400"></div>

필요한 데이터와 긍부정 나눈것을 합쳐서 하나의 데이터로 만들었다
- 데이터 (positive:0, negative:1)

||Review|Label|
|---|---|---|
|0|Great music service, the audio is higy quality..|0|
|1|Please ignore previous negative rating..|0|
|2|This pop-up "Get the best Spotify eperience..|0|
|...|...|...|
|54281|This app would be good if not for it..|1|
|54282|The app is good hard to navigate and won't..|1|
|54283|Its good but sometimes it doesnt load the..|0|


긍부정 리뷰 문장 20자 이상 길이의 분포
<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/81c86908-758d-48a2-a976-c5185761c27f" width="400"></div>


### 가공한 데이터 학습
0,1에서 각각 1000건씩 추출하여 2000건을 학습했다  
<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/c1f86774-1951-4e15-98a0-82cbb8250630"></div>
모델의 긍부정 예측 정확도는 0.91이 나왔다  
<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/eadf19b7-e775-4f24-b878-24fdfbdbc92f" width="400"></div>
모델의 loss 그래프 학습할수록 loss가 떨어지고 있다  
<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/d2ca6bba-1e96-4734-9654-0c0189558c06" width="400"></div>
Accuracy 그래프 학습할수록 정확도가 올라가고 있다  
<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/ff0fd7db-4bb5-4f71-9812-7c0cbcc45813" width="400"></div>
전체 데이터의 긍부정 예측 정확도는 0.87이 나왔다





