# Spotify App 리뷰 감성분석 :musical_note:

<div>
MobileBert를 이용하여 Google Play Store의 Spotify App 리뷰 긍부정을 예측해보는 프로젝트
    
<img src="https://img.shields.io/badge/PyTorch-E34F26?style=flat-square&logo=PyTorch&logoColor=white"/> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white"/>
</div>

## 1. 개요

### 1.1 문제정의
음악감상은 스트리밍 서비스의 발전으로 대중의 접근성이 더 좋아졌다. 스트리밍 서비스를 지원하는 spotify는 현재 180여개 국가에서 서비스를 제공하고 있다. IT 시장조사업체 미디어리서치(MIDiA)에 따르면 2022년 상반기 기준 spotify는 전 세계 음악 스트리밍 서비스 시장의 30% 가량(구독자 1억8780만명)을 차지하고 있다. spotify가 다른 스트리밍 앱들보다 경쟁력이 있는지 알기 위해 Kaggle에서 제공하는 spotify app 리뷰 데이터를 바탕으로 리뷰의 긍정 또는 부정을 예측하는 인공지능 모델을 개발하고자 한다.

### 1.2 spotify 리뷰의 영향력
사용자들이 어떤 기능이나 서비스를 좋아하는지, 어떤 부분에서 경쟁사와 차별화되는지 등을 파악할 수 있다. 이를 통해 Spotify는 경쟁사와의 차별화된 서비스를 제공하고 음악 스트리밍 시장에서의 경쟁력을 강화할 수 있다. 또한 사용자들의 리뷰를 통해 Spotify의 브랜드 이미지와 고객 인식이 형성될 수 있다. 긍정적인 리뷰는 Spotify의 이미지를 향상시키고 브랜드에 대한 고객들의 신뢰를 증대시킬 수 있다. 부정적인 리뷰는 Spotify가 개선해야 할 부분을 도출하고 이를 통해 사용자들에게 더 나은 서비스를 제공하기 위한 노력을 보여줄 수 있다.

### 1.3 데이터 출처
Kaggle [Spotify App(Google Play Store)](https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022 "Spotify App")

## 2. 데이터

### 2.1 구성
- 데이터명

|Time_submitted|Review|Rating|Total_thumbsup|Reply|
|---|---|---|---|---|
|리뷰 제출 시간|리뷰|평점|도움된 수|리뷰 재응답|

- 데이터

![image](https://user-images.githubusercontent.com/85285367/232947749-a0c1dce2-da8e-4a4b-a26c-2901e316eb07.png)


6만여 개의 리뷰가 있으며 1점부터 5점으로 구성되어 있다.

    import matplotlib.pyplot as plt
    import seaborn as sns
    data = pd.read_csv('spotifyrv.csv')
    sns.countplot(data=data, x="Rating")
      
<div><img src = "https://user-images.githubusercontent.com/85285367/232946755-84bc9efe-56f0-4a1a-8015-c5914f21658e.png" width="350"></div>

1, 2점은 부정, 3점은 중립, 4, 5점은 긍정으로 분류했다.

    data["Rating"].replace(1, value="negative",inplace=True)
    data["Rating"].replace(2, value="negative",inplace=True)
    data["Rating"].replace(3, value="neutral",inplace=True)
    data["Rating"].replace(4, value="positive",inplace=True)
    data["Rating"].replace(5, value="positive",inplace=True)
    sns.histplot(data['Rating'])
    plt.title('Ratings')
    plt.xlabel('')
    plt.show()


<div><img src ="https://user-images.githubusercontent.com/85285367/232965879-a6247b8a-6927-4006-8818-e3d222b641b9.png"></div>






### ---출처---
<a href="https://biz.chosun.com/it-science/ict/2023/03/21/P6ZEG3RF2VDU7K4R2MO3B6S5BY">시장점유율</a>
