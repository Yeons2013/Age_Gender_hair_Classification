# 안면 데이터를 이용한 분류 모델 구축

Second Mini Project(Computer Vision)
<br>
<br>
목록 | 설명
------------|--------------------
[AgeModel.ipynb](https://github.com/Yeons2013/Age_Gender_hair_Classification/blob/master/AgeModel.ipynb) | 연령대 분류 모델
[GenderModel.ipynb](https://github.com/Yeons2013/Age_Gender_hair_Classification/blob/master/GenderModel.ipynb) | 성별 분류 모델
[HairModel(Augmentation).ipynb](https://github.com/Yeons2013/Age_Gender_hair_Classification/blob/master/HairModel(Augmentation).ipynb) | 헤어 분류 모델(증강O)
[HairStyleModel.ipynb](https://github.com/Yeons2013/Age_Gender_hair_Classification/blob/master/HairStyleModel.ipynb) | 헤어 분류 모델(증강X)

---

## 프로젝트 주제


+ 유동인구가 많은 곳에 위치해 있지만 폐점률이 높은 상가의 폐점률을 개선한다는 목표
+ 안면데이터를 활용해 해당 위치의 유동인구 정보를 활용하는 AI 모델을 만들어 특정 층을 겨냥한 상가가 들어설 수 있도록 함.
  
<br>

---

<br>

## 프로젝트 팀 구성 및 역할
<br>

팀 원 | 담당업무|
----  |------|
강동호 | 기획, 전처리, 모델링, 시각화
이정아 | 기획, 전처리, 모델링, 시각화
박혜정 | 기획, 전처리, 모델링, 팀 노션 관리
정가영 | 기획, 전처리, 모델링, 시각화
최현호 | 전처리, 모델링, 디자인, 발표 
황성연 | 기획, 전처리, 모델링, 시각화

<br>
<br>


---


## 사용 데이터
+ AI Hub의 페르소나 기반의 가상인물 몽타주 데이터<br>
[➡️<AI Hub 접속>](https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=618)
+ 여러 정보 중 나이, 성별, 헤어스타일 유형 정보를 사용하여, 각각 분류해줄 수 있는 모델 3개 생성.

<img src="https://cdn.discordapp.com/attachments/1002189622912221250/1085777131696574514/9.JPG" width="700">

<br>

---

<br>

## 데이터 분포
### 1. Age
<img src="https://media.discordapp.net/attachments/1002189622912221250/1085781299563872276/15.JPG" width="700">

<br>

### 2. Gender
<img src="https://media.discordapp.net/attachments/1002189622912221250/1085781927082070066/20.JPG" width="700">

<br>

### 3. HairStyle
<img src="https://media.discordapp.net/attachments/1002189622912221250/1085781927363084338/25.JPG" width="700">







<br>

---

<br>

## 데이터 전처리
### 1. Resize & Padding
+ Resize를 통해 이미지를 학습할 수 있는 자원의 크기로 축소.
+ 전이학습을 원할하게 하기 위해 가로 세로 길이를 맞춤.
+ 가로와 세로의 비율이 무너지지 않도록 Padding을 통해 맞춰줌.

<img src="https://media.discordapp.net/attachments/1002189622912221250/1085778734847623228/11.JPG" width="700">


<br>


<br>

### 2. Zero-centering
+ 입력값에 zero-mean 값을 빼서 normalization을 수행함.
+ 이를 통해 모든 차원의 값들이 동등한 기여를 할 수 있도록 조절해줌.

<img src="https://media.discordapp.net/attachments/1002189622912221250/1085780099380559952/12.JPG" width="700">


<br>

<br>



### 3. Data-Augmentation
+ 데이터 편향이 심하고, 나이와 성별에 비해 낮은 정확도를 보이는 헤어스타일 데이터를 증강하여 편향문제를 개선하고 성능 향상을 기대함.
+ 원본을 크게 훼손하지 않는 회전, 위치 변경 등의 기법만을 사용

<img src="https://media.discordapp.net/attachments/1002189622912221250/1085782149120139375/13.JPG" width="700">

<img src="https://media.discordapp.net/attachments/1002189622912221250/1085787638063190089/47.jpg?width=1060&height=671" width="700">


<br>

---

<br>


## 모델 학습

### 1. Age Model
+ 분류할 클래스의 숫자 : 3 (청년, 중년, 장년)
+ 4가지 모델 사용
  + 사용 모델 1 : Custom MLP
  + 사용 모델 2 : Custom CNN
  + 사용 모델 3 : [전이학습] AlexNet
  + 사용 모델 4 : [전이학습] ResNet50
+ CnvLayer, FcLayer의 개수, DropOut, 각 층의 Node 수, Optimizer, LearnigRate 등 모델 핸들링 
+ __최적의 Model로 Resnet50 선정__


<br>

### 2. Gender Model
+ 분류할 클래스의 숫자 : 2 (남성, 여성)
+ 4가지 모델 사용
  + 사용 모델 1 : Custom MLP
  + 사용 모델 2 : Custom CNN
  + 사용 모델 3 : [전이학습] AlexNet
  + 사용 모델 4 : [전이학습] ResNet50
+ CnvLayer, FcLayer의 개수, DropOut, 각 층의 Node 수, Optimizer, LearnigRate 등 모델 핸들링 
+ __최적의 Model로 ResNet50 선정__


<br>

### 3. HairStyle Model
+ 분류할 클래스의 숫자 : 2 (남성, 여성)
+ 4가지 모델 사용
  + 사용 모델 1 : Custom MLP
  + 사용 모델 2 : Custom CNN
  + 사용 모델 3 : [전이학습] AlexNet
  + 사용 모델 4 : [전이학습] ResNet50
+ CnvLayer, FcLayer의 개수, DropOut, 각 층의 Node 수, Optimizer, LearnigRate 등 모델 핸들링 
+ __최적의 Model로 ResNet50 선정__
  

<br>

---

<br>

## 결과 해석
### 1. Age Model
+ 90% ~ 94%의 Accuracy
+ 많지 않은 Class, Class별 데이터 갯수의 불균등이 크지 않아 비교적 높은 성능을 보임
+ 데이터의 복잡도와 ResNet50의 복잡도 4가지 모델 중 가장 잘 맞아 떨어짐.

<br>

### 2. Gender Model
+ 99.9%라는 높은 Accuracy
+ 이진 분류이기에 문제 자체가 쉬우며, 투입한 몽타주 데이터의 특징 남녀 특징 역시 뚜렷하여 데이터의 복잡도가 낮음
+ 데이터의 복잡도가 낮기에 어떠한 모델이든 높은 정활도를 보인 것으로 판단

<br>

### 3. HairStyle Model
+ 앞의 두 모델과 비교하면 지나치게 낮은 성능
+ 클래스의 개수도 5개로 앞의 모델에 비해 많으며, 라벨 간 편향이 심하기 때문에 좋지 않은 성능을 보인 것으로 판단
+ 성능 향상을 위해서는 데이터를 추가로 투입하거나, 좀 더 다양한 Augmentation을 통해 라벨간 균형을 맞춰주는 필요할 것으로 보임.


<br>

---

<br>

## 활용가치

### 모델을 이용해 파악한 성별과, 연령대 정보를 활용해 부동산 컨설팅
+ 예를 들어 중년 남성층의 유동인구가 많다면, 해당 상가에 DAKS, BlASCK YAK 등 중년 남성을 타겟으로 할 수 있는 상가가 들어 설 수 있도록 컨설팅

+ 성별 및 연령을 분류해줄 수 있는 간단한 웹 사이트 생성을 통해 모델 홍보 및 광고 수익 기대
  
<img src="https://media.discordapp.net/attachments/1002189622912221250/1085798829661622343/44.JPG" width="700">
<img src="https://media.discordapp.net/attachments/1002189622912221250/1085798829934248076/45.JPG" width="700">
