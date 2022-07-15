### Description
* datetime - hourly date + timestamp  
* season -  1 = 봄, 2 = 여름, 3 = 가을, 4 = 겨울  
* holiday - 1 = 토, 일요일의 주말을 제외한 국경일 등의 휴일, 0 = 휴일이 아닌 날
* workingday - 1 = 토, 일요일의 주말 및 휴일이 아닌 주중, 0 = 주말 및 휴일
* weather 
    - 1: 맑음, 약간 구름 낀 흐림  
    - 2: 안개, 안개 + 흐림  
    - 3: 가벼운 눈, 가벼운 비 + 천둥  
    - 4: 심한 눈/비, 천둥/번개 
* temp - 온도(섭씨)  
* atemp - 체감온도(섭씨)  
* humidity - 상대 습도  
* windspeed - 풍속  
* casual - 사전에 등록되지 않은 사용자가 대여한 횟수  
* registered - 사전에 등록된 사용자가 대여한 횟수  
* count - 대여 횟수  

### Evaluation
Submissions are evaluated one the Root Mean Squared Logarithmic Error (RMSLE).


1차 : 베이스라인 
간단한 전처리 후 모델링 진행
- 피처 제거 : 'datetime','casual','registered'
- 모델 : linear
rmsle : 1.43233

2차 : 전처리 진행 
- count(targer변수) 로그 변환
- 원핫인코딩['holiday', 'workingday', 'season', 'weather']
- 모델 linear
rmsle : 1.18442

3차 : 전처리 추가
- datetime을 month, year, day, hour 로 분할
- 모델 linear
rmsle : 1.03186

4차-1  : 다중공산성(실패)
- temp, atemp의 상관관계가 매우 높아서 다중공산성 문제가 발생할것으로 예측됨 
- count(타겟)을 기준으로 상관관계가 낮은 atemp를 제거
rmsle : 1.03246

4차-2  : 다중공산성(실패) 
- atemp를 제거하지 말고 temp 제거
rmsle : 1.03299

5차 : 수치형 데이터인 windspeed(풍속) 데이터 처리(실패)
- windspeed값이 0인 데이터를 y변수로 머신러닝 모델을 돌려서 예측해서 0인 값을 채워준다
rmsle: 1.65214

6차 : 데이터 오류 수정
- 데이터 수기보완 : holiday, workingday 피처에 데이터 오류가 발견되어 이를 수정
rmsle: 1.03212

7차 : linear -> rf
- 랜덤포레스트 모델로 변경해서 모델링 진행
rmsle : 0.45008

8차 : 랜덤 서치를 활용하여 간단한 모델 튜닝 진행
- RandomizedSearchCV을 활용하여 rf모델 파라미터 튜닝
- 대회 평가지표에서는 rmsle을 활용하지만 튜닝 과정에서는 rmse지표를 활용함
- 평가 지표가 다르기 때문에 튜닝을 진행해도 모델 성능 개선에는 도움이 안되는것으로 판단됨
rmsle : 0.45037




