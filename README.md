# Spotify App 리뷰 감성분석 :musical_note:
<div><img src ="https://user-images.githubusercontent.com/85285367/235826775-224c4b7c-57b3-4e1d-b13e-49849cb86cbd.png"></div>


MobileBert를 이용하여 Google Play Store의 Spotify App 리뷰 긍부정을 예측해보는 프로젝트  

## 1. 개요

### 1.1 문제정의
음악감상은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. Google Play Store를 통해 다양한 음악 스트리밍 앱을 다운로드할 수 있으며, 사용자들은 이러한 앱을 통해 원하는 음악을 언제 어디서나 즐길 수 있다.
  
<div align="center"><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/92ab9528-3faf-47fd-8ea1-a2db2a80d62d" width="500"></div>
Google Play Store는 음악, 동영상, 책, 안드로이드 응용 프로그램, 게임을 포함한 온라인 스토어와 클라우드 미디어 플레이어를 아우르는 구글의 디지털 콘텐츠 서비스이다.  
안드로이드에서 사용할 수 있는데 2023년 4월 기준 전 세계 모바일 운영체제(OS) 시장에서 안드로이드(Android)의 점유율은 약 68.6%으로 많은 사람들이 Google Play Store를 이용한다. <a href="https://gs.statcounter.com/os-market-share/mobile/worldwide/">[1]</a>  


각 앱마다 평점과 리뷰가 있고, 사용자들이 해당 앱과 제공하는 전반적인 서비스에 대한 사용자의 경험은 가치 있는 정량적, 정성적 피드백을 제공하므로 평점과 리뷰는 중요하다. 
평점은 일반적으로 1부터 5까지의 5점 척도로 표현되며 1점은 매우 나쁨, 2점은 나쁨, 3점은 보통, 4점은 좋음, 5점은 매우 좋음을 의미한다.
높은 평점을 받은 앱은 보통 사용자들이 해당 앱의 기능과 서비스에 만족하는 경향이 있다.
리뷰는 Google 계정이 있는 사용자가 앱을 다운로드하여 사용한 경험을 바탕으로 제공한다. 다른 사용자들의 리뷰를 통해 앱의 장점과 단점, 사용자 인터페이스의 편의성 등을 파악할 수 있다. 
긍정적인 리뷰는 앱의 우수한 품질과 기능을 강조하며, 부정적인 리뷰는 앱의 개선점과 문제점을 지적한다.
이러한 평점과 리뷰를 통해 Google Play Store에서 음악 스트리밍 앱을 선택할 때 사용자들은 다른 사용자들의 평점과 리뷰를 참고하여 자신에게 가장 적합한 음악 스트리밍 앱을 선택할 수 있다. <a href="https://android-developers.googleblog.com/2021/08/making-ratings-and-reviews-better-for.html">[2]</a>

<div align="center"><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/3790d289-575f-40d9-922f-d983d0275db1" width="500"></div>
Spotify는 전 세계적으로 널리 이용되고 있는 음악 스트리밍 플랫폼이다. IT 시장조사업체인 미디어리서치(MIDiA)가 2022년 2분기를 기준 글로벌 시장 점유율을 집계한 결과에 따르면, Spotify가 가장 높은 시장 점유율을 보여줬다. Spotify는 전체 시장의 30.5%를 차지하며 1위를 기록했다. Apple Music은 13.7%의 점유율로 2위를 차지하고, Tencent Music은 13.4%의 점유율로 3위를 차지했다. 이를 비교해보면 Spotify는 2위인 Apple Music보다도 약 2배 가량 더 많은 시장 점유율을 보여주고 있다. 이러한 결과로, 음악 스트리밍 앱 시장에서 Spotify가 현저한 우위를 차지하고 있다는 사실을 알 수 있다. <a href="https://it.chosun.com/site/data/html_dir/2023/06/19/2023061902063.html">[3]</a>
<div align="center"><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/08216e11-5597-4fe6-8916-baef580d3df0" width="500"></div>
SPotify는 2023년 1분기 기준 5억 1,500만 명이 이용하고 있고 Spotify는 거의 모든 연령대 뿐만 아니라 많은 나라에서 이용자 수에 대한 큰 성장을 보였다.
이러한 성장의 대부분은 무료 광고 지원 버전의 Spotify 서비스를 사용하는 사람들을 기반으로 한다.
프리미엄 구독은 전년 대비 15% 증가한 2억 1천만 명으로 유럽과 라틴 아메리카를 비롯한 모든 지역에서 우수한 실적을 보였다. <a href="https://newsroom.spotify.com/2023-04-25/spotify-reports-first-quarter-2023-earnings/">[4]</a>  


### 1.2 spotify 리뷰의 영향력
사용자들이 어떤 기능이나 서비스를 좋아하는지, 어떤 부분에서 경쟁사와 차별화되는지 등을 파악할 수 있다. 이를 통해 Spotify는 경쟁사와의 차별화된 서비스를 제공하고 음악 스트리밍 시장에서의 경쟁력을 강화할 수 있다. 또한 사용자들의 리뷰를 통해 Spotify의 브랜드 이미지와 고객 인식이 형성될 수 있다. 긍정적인 리뷰는 Spotify의 이미지를 향상시키고 브랜드에 대한 고객들의 신뢰를 증대시킬 수 있다. 부정적인 리뷰는 Spotify가 개선해야 할 부분을 도출하고 이를 통해 사용자들에게 더 나은 서비스를 제공하기 위한 노력을 보여줄 수 있다.

spotify가 다른 스트리밍 앱들보다 경쟁력이 있는지 알기 위해 Kaggle에서 제공하는 spotify app 리뷰 데이터를 바탕으로 리뷰의 긍정 또는 부정을 예측하는 인공지능 모델을 개발하고자 한다.

### 1.3 데이터 출처
Kaggle [Spotify App(Google Play Store)](https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022 "Spotify App")

## 2. 데이터

### 2.1 원본 데이터
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

6만여 개의 리뷰가 있으며 1점부터 5점으로 구성되어 있다, 도움된 수를 평점별과 평균값에 대한 그래프를 그려봤다  
      
<div><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/86cb68fa-9547-432c-9a86-dc761a41e329" width="400"><img src = "https://github.com/ho0116/2023pj_spotify/assets/85285367/b784c1d8-85f7-4efc-933e-912ef76900af" width="400"></div>

1점에는 17653개, 2점은 7118, 3점은 6886, 4점은 7842개, 5점은 22095개의 데이터로 구성되어있다   
도움된 수 그래프는 1점은 9개, 2점은 10개, 3점은 13개, 4점은 11개, 5점은 3개로 구성되어있다  
Spotify가 글로벌 1위를 차지하고 있기 때문에 리뷰의 도움된 수도 높을 것으로 예상했는데 의외로 5점의 도움된 수가 적게 나왔다
  
- 리뷰 문장 10자 이상 길이의 분포도
<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/142995b8-ea69-4dee-9c30-24c21a00d9ba" width="400"></div>
100자 전후로 많은 리뷰가 몰려있다

### 2.2 분석 데이터

원본 데이터에서 리뷰와 평점을 추출하여 사용했다  
평점에서 3점을 제외하고, 1점과 2점은 부정(1)으로, 4점과 5점은 긍정(0)으로 분류했다  
이렇게 분류한 긍정과 부정을 하나의 데이터로 만들었다

- 데이터

||Review|Label|
|---|---|---|
|0|Great music service, the audio is higy quality..|0|
|1|Please ignore previous negative rating..|0|
|2|This pop-up "Get the best Spotify eperience..|0|
|...|...|...|
|54279|This app would be good if not for it..|1|
|54280|The app is good hard to navigate and won't..|1|
|54281|Its good but sometimes it doesnt load the..|0|

54282개의 데이터가 있으며 긍정과 부정에 대한 그래프를 그려봤다

<div><img src ="https://github.com/ho0116/2023pj_spotify/assets/85285367/de5de9c3-dd31-4f3a-ac80-6dbb8a70cf56" width="400"></div>

긍정은 29688개가 있고, 부정은 24594개의 데이터로 구성되어있다

### 2.3 학습 데이터

분석 데이터의 라벨인 긍정(0), 부정(1)에서 임의로 각각 1000건씩 추출하여 2000건을 학습했다
- 데이터

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
#### MobileBERT를 사용한 결과
<div><img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/26b2d811-b7ff-4b9a-afb8-58f635637911" width="400"> <img src="https://github.com/ho0116/2023pj_spotify/assets/85285367/11edb235-fb10-4996-b411-61086f9ca273" width="400"></div>

|step|0|1|2|3|
|:---:|:---:|:---:|:---:|:---:|
|loss|1.59|0.32|0.27|0.19|
|accuracy|0.9|0.92|0.93|0.93|

모델의 긍부정 예측 정확도는 **0.93**이 나왔다  
모델의 loss 그래프는 학습할수록 loss가 떨어지고 있다  
Accuracy 그래프는 학습할수록 정확도가 오르거나 유지되고 있다  
54282개의 분석 데이터의 긍부정 예측 정확도는 **0.89**가 나왔다

### 결론
사용된 모델은 학습 데이터와 분석 데이터에서 모두 높은 정확도를 보여 리뷰의 긍부정을 믿을 만한 정확도로 예측할 수 있다. Spotify의 관리자나 의사결정자는 이 모델을 활용하여 사용자 리뷰를 분석하고, 긍정적인 측면을 강화하거나 부정적인 측면을 개선하는 등 서비스 품질 향상에 도움을 줄 수 있을 것 같다.

## 배운점
이번 감성분석 프로젝트를 통해 중립인 3점을 포함한 부정, 중립, 긍정 세 가지로 분석해보고 싶다는 아쉬움이 들었다. 전처리 작업에 많은 시간을 투자하여 글쓰기에 충분한 시간을 할애하지 못한 것이 아쉬웠다. 또한, 정제된 데이터만을 사용하다가 정제되지 않은 데이터를 처리하면서 전처리 능력의 중요성을 깨달았다. 앞으로의 프로젝트에서는 데이터 전처리에 충분한 시간을 할애하면서도 글쓰기에도 충분한 시간을 확보해야 한다고 느꼈다.
