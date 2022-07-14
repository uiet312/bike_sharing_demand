1차 : 베이스라인 baseline.csv
간단한 전처리 후 모델링 진행
- 피처 제거 : 'datetime','casual','registered'
- 모델 : linear
rmsle : 1.43233

2차 : 전처리 진행 baseline_v1.csv
- count(targer변수) 로그 변환
- 원핫인코딩['holiday', 'workingday', 'season', 'weather']
- 모델 linear
rmsle : 1.18442

3차 : 전처리 추가
- datetime을 month, year, day, hour 로 분할
- 모델 linear
rmsle : 
