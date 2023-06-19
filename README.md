# Spotify App 리뷰 감성분석 :musical_note:
<div><img src ="https://user-images.githubusercontent.com/85285367/235826775-224c4b7c-57b3-4e1d-b13e-49849cb86cbd.png"></div>


MobileBert를 이용하여 Google Play Store의 Spotify App 리뷰 긍부정을 예측해보는 프로젝트

## 1. 개요

### 1.1 문제정의
음악감상은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. Google Play Store를 통해 다양한 음악 스트리밍 앱을 다운로드할 수 있으며, 사용자들은 이러한 앱을 통해 원하는 음악을 언제 어디서나 즐길 수 있다.
  
<div align="center"><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/92ab9528-3faf-47fd-8ea1-a2db2a80d62d" width="500"></div>
Google Play Store는 음악, 동영상, 책, 안드로이드 응용 프로그램, 게임을 포함한 온라인 스토어와 클라우드 미디어 플레이어를 아우르는 구글의 디지털 콘텐츠 서비스이다.  
안드로이드에서 사용할 수 있는데 2023년 4월 기준 전 세계 모바일 운영체제(OS) 시장에서 안드로이드(Android)의 점유율은 약 68.6% 이다. <a href="https://gs.statcounter.com/os-market-share/mobile/worldwide/">[1]</a>  


평점과 리뷰는 앱과 제공하는 전반적인 서비스에 대한 사용자의 경험은 가치 있는 정량적, 정성적 피드백을 제공하므로 중요하다. 
평점은 일반적으로 1부터 5까지의 5점 척도로 표현되며 1점은 매우 나쁨, 2점은 나쁨, 3점은 보통, 4점은 좋음, 5점은 매우 좋음을 의미한다.
높은 평점을 받은 앱은 보통 사용자들이 만족하는 기능과 서비스를 제공하는 경향이 있다.
리뷰는 Google 계정이 있는 사용자가 앱을 다운로드하여 사용한 경험을 바탕으로 제공한다. 다른 사용자들의 리뷰를 통해 앱의 장점과 단점, 사용자 인터페이스의 편의성, 음악 추천 알고리즘의 정확성 등을 파악할 수 있다.
이를 통해 Google Play Store에서 음악 스트리밍 앱을 선택할 때 사용자들의 평가와 리뷰를 참고하여 자신에게 가장 적합한 음악 스트리밍 앱을 선택할 수 있다. <a href="https://android-developers.googleblog.com/2021/08/making-ratings-and-reviews-better-for.html">[2]</a>
<div align="center"><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/08216e11-5597-4fe6-8916-baef580d3df0" width="500"></div>
Spotify는 현재 184개 국가에서 서비스를 제공하고 있어 전 세계적으로 널리 이용되고 있는 음악 스트리밍 플랫폼이다. <a href="https://newsroom.spotify.com/2022-02-14/%EC%8A%A4%ED%8F%AC%ED%8B%B0%ED%8C%8C%EC%9D%B4-%EA%B5%AD%EB%82%B4-%EB%A1%A0%EC%B9%AD-1%EC%A3%BC%EB%85%84-%EA%B8%B0%EB%85%90-%EA%B8%80%EB%A1%9C%EB%B2%8C-%EC%84%B1%EA%B3%BC-%EB%B0%8F-%EB%8D%B0%EC%9D%B4/">[3]</a>
2023년 1분기 기준 5억 1,500만 명이 이용하고 있고 Spotify는 거의 모든 연령대 뿐만 아니라 많은 나라에서 이용자 수에 대한 큰 성장을 보였다.
이러한 성장의 대부분은 무료 광고 지원 버전의 Spotify 서비스를 사용하는 사람들을 기반으로 한다.
프리미엄 구독은 전년 대비 15% 증가한 2억 1천만 명으로 유럽과 라틴 아메리카를 비롯한 모든 지역에서 우수한 실적을 보였다. <a href="https://newsroom.spotify.com/2023-04-25/spotify-reports-first-quarter-2023-earnings/">[4]</a>  


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
      
<div><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/86cb68fa-9547-432c-9a86-dc761a41e329" width="400"><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/b784c1d8-85f7-4efc-933e-912ef76900af" width="400"></div>
도움된 수를 평점별과 평균값에 대한 그래프를 그려봤다  

  
- 리뷰 문장 10자 이상 길이의 분포도
<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/142995b8-ea69-4dee-9c30-24c21a00d9ba" width="400"></div>
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
|54279|This app would be good if not for it..|1|
|54280|The app is good hard to navigate and won't..|1|
|54281|Its good but sometimes it doesnt load the..|0|

### 2.3 학습 데이터
긍,부정에서 임의로 각각 1000건씩 추출하여 2000건을 학습했다
||Review|Label|
|---|---|---|
|0|Great music service, the audio is higy quality..|0|
|1|Please ignore previous negative rating..|0|
|2|This pop-up "Get the best Spotify eperience..|0|
|...|...|...|
|1997|Cannot update my premium. It always try to..|1|
|1998|worst possible app. constant bugs and issues,..|1|
|1999|Impossible to use liked songs will only play..|1|

## 결과  
#### 개발환경  
<img src="https://img.shields.io/badge/pycharm 2022.3.3-000000?style=flat-square&logo=pycharm&logoColor=white"/> <img src="https://img.shields.io/badge/Python 3.9.0-3776AB?style=flat-square&logo=Python&logoColor=white"/>  
#### 패키지  
<img src="https://img.shields.io/badge/pandas 1.4.4-150458?style=flat-square&logo=pandas&logoColor=white"/> <img src="https://img.shields.io/badge/torch 1.12.1-EE4C2C?style=flat-square&logo=pytorch&logoColor=white"/> <img src="https://img.shields.io/badge/tensorflow 2.9.1-FF6F00?style=flat-square&logo=tensorflow&logoColor=white"/> <img src="https://img.shields.io/badge/numpy 1.24.2-013243?style=flat-square&logo=numpy&logoColor=white"/> <img src="https://img.shields.io/badge/transformers 4.21.2-81c147?style=flat-square&logo=transformers&logoColor=white"/> <img src="https://img.shields.io/badge/scikit-learn 1.2.2-F7931E?style=flat-square&logo=scikit-learn&logoColor=white"/> <img src="https://img.shields.io/badge/matplotlib 3.7.1-3776AB?style=flat-square&logo=matplot&logoColor=white"/>

<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/26b2d811-b7ff-4b9a-afb8-58f635637911" width="500"> <img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/11edb235-fb10-4996-b411-61086f9ca273" width="500"></div>

|step|loss|accuracy|
|---|---|---|
|0|1.59|0.9|
|1|0.32|0.92|
|2|0.27|0.93|
|3|0.19|0.93|

모델의 긍부정 예측 정확도는 0.93이 나왔다  
모델의 loss 그래프는 학습할수록 loss가 떨어지고 있다 Accuracy 그래프는 학습할수록 정확도가 올라가고 있다  
54282개의 데이터의 긍부정 예측 정확도는 0.89가 나왔다

## 배운점
