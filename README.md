﻿# [2021 금융 데이터 경진대회] LDA기반 감성분석과 AHP를 통한 코로나 피해 소상공인의 디지털 전환 전략


## 👩‍👦‍👦 팀구성
- Team name: **김권홍팀**
- **김권호(Kwonho Kim)**: Dept. of Applied Statistics in CAU      
- **권예진(Yejin Kwon)**: Dept. of Applied Statistics in CAU   
- **홍지중(Jijoong Hong)**:  Dept. of Industrial Security in CAU   



## 💡 전체 분석 프로세스
![프로세스 사진.png](https://github.com/Becky-Kwon/Kim-Kwon-Hong/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%20%EC%82%AC%EC%A7%84.png?raw=true)

## 👀 코드 설명
(위의 분석 프로세스에 맞추어 코드 파일이 어떻게 구성되는지 단계 별로 정리해보았습니다. 분석 프로세스에 따른 코드는 단계별로 묶어 제출하여 확인가능합니다.)

|분석 프로세스|작성 코드|
|------|--------|
|데이터 수집|요기요 데이터 수집.ipynb|
|데이터 전처리|요기요 데이터 수집.ipynb<br>오프라인_데이터_분석/신한카드_데이터_EDA.ipynb<br>요기요_주문금액_계산.ipynb<br>요기요_주문금액_전처리.ipynb<br> 1.LDA+Inference.ipynb|
|데이터 분석(EDA)|"오프라인_데이터_분석"&"온라인_데이터_분석"속 전체 코드<br>|
|데이터 분석(모델링)|1.LDA+Inference.ipynb<br>2.classifications_pytorch_kobert_yogiyo.ipynb<br>3.infer_sentimental.ipynb<br>4.grouping.ipynb<br>5.AHP_progress.ipynb<br>|


###  1️⃣ 데이터 수집 단계
제공데이터로는 KB 국민카드, 신한카드, 신한은행 제공 데이터를 사용하였고, 추가적으로 [요기요 사이트](https://www.yogiyo.co.kr/mobile/#/)에서 직접 수집하여 데이터셋을 구성.  

**<요기요 데이터 수집 과정>**
- 리뷰 데이터 수집을 위한 사전단계로서 가게별 URL 수집
- 가게별 URL 기반 리뷰 데이터 수집
- 추가 분석을 위한 가게 평점, 메뉴 등 전반적인 가게 정보 수집  
 *(관련 코드 : "요기요 데이터 수집.ipynb" 참조 )*

###  2️⃣ 데이터 전처리 단계
 - **분석 대상 지역 선정** 
 : KB국민카드 데이터의 분석 범위를 기준으로 하여 강남구와 마포구 소재의 음식점을 분석대상으로 선정해 요기요 데이터 크롤링을 진행  
 *(관련 코드 : "요기요 데이터 수집.ipynb" 참조 )*
 
- **가게 별 라벨 통합**
: 요기요 리뷰 데이터를  기준으로  분석을  진행하기에, 신한카드  데이터  또한  업종  분류  라벨을  요기요  분류에  맞추어 EDA 진행  
 *(관련 코드 :  "오프라인_데이터_분석/신한카드_데이터_EDA.ipynb" 참조 )*
 
- **결측치 제거**  
*(관련 코드 :  "오프라인_데이터_분석/신한카드_데이터_EDA.ipynb" & "요기요 데이터 수집.ipynb" 참조 )*  

- **리뷰 당 주문금액 계산**  
: 리뷰  데이터의  주문  내역과  가게  별  메뉴  및  가게  데이터를  활용하여  리뷰를  남긴  사람이  지불한  금액을  계산  
 *(관련 코드 :  "요기요_주문금액_계산.ipynb" & "요기요_주문금액_전처리.ipynb"참조 )*

- **한국어 텍스트 전처리**  
: 요기요  리뷰  데이터를  사용해  업종  별로  서비스  평가기준을  찾고자  토픽  모델링을  수행하는데, 이때  리뷰를  토큰화한  후  불용어를  제거  
*(관련 코드 :  "1.LDA+Inference.ipynb" 참조 )*


###  3️⃣ 데이터 분석 단계
데이터 분석 단계는 가공한 데이터를 시각화 하는 EDA(탐색적 데이터 분석)단계와 리뷰 텍스트에 적용하여 모델을 구축하는 모델링 단계로 나누어진다.    

**1) EDA(탐색적 데이터 분석) 단계**  
 온라인 음식점과 오프라인 음식점 매출 분석 및 솔루션 대상 업종 선택  
*(관련 코드 :  "오프라인_데이터_분석 "  & 온라인_데이터_분석 " 속 코드 참조 )*

**2) 데이터 모델링 단계**
- `LDA 모델링` :  리뷰 데이터를 토픽 모델링 하여 소비자들의 서비스 평가 기준을 파악  
*(관련 코드 :   "1.LDA+Inference.ipynb" 참조 )*  

- `감성분석` :  각 리뷰를 토픽에 맞추어라벨링 한 후, 토픽 별로 감성 분석을 진행하여 추후 분석에 긍정 점수의 분산 값을 평가기준의 중요도 척도로 사용   
*(관련 코드 :  "2.classifications_pytorch_kobert_yogiyo.ipynb" & "3.infer_sentimental.ipynb" 참조 )*    

- `AHP 기법 적용` : 리뷰 별로 평가 기준(리뷰 속 토픽)별로 긍정 점수 분산 값을 계산하고 이에 AHP 기법을 적용해 평가기준 간에 상대적인 중요도를 분석  
*(관련 코드 :  "4.grouping.ipynb" & "5.AHP_progress.ipynb" 참조 )*   

      

## ✨ 분석 결과
붉은 색 계열일수록 경쟁이 치열한 업종이고, 파란색 계열일수록 진입하기 좋은 업종이다. 회색은 진입률도 낮고 매출도 감소하는 수익을 보기 어려운 업종이다.
![분석결과.png](https://github.com/Becky-Kwon/Kim-Kwon-Hong/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EB%B6%84%EC%84%9D%EA%B2%B0%EA%B3%BC.png?raw=true)




