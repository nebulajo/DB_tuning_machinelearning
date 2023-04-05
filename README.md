# Redis 파라미터 분류 및 단계적 베이지안 최적화를 통한 파라미터 튜닝 연구

[paper](https://drive.google.com/file/d/1JCWwKfQMQBS4rc9tmG3MLMdDCuZ1dORR/view)

1. FA로 internal_metrics 클러스터링 진행(internal_metrics)
2. corr로 클러스터 별로 상관 계수 확인 (internal_metrics, result_config)
3. model에서 모델 생성 후 클러스터 별로 예측 진행(external_metrcis, result_config)

DBMS 파라미터 튜닝이란 데이터베이스에서 제공하는 다양한 파라미터의 값을 조율하여, 최적의 성능을 도출하는 과정이다. 데이터베이스 종류에 따라 파라미터 개수가 수십 개에서 수백 개로 다양하며, 각 기능이 모두 다르기 때문에 최적의 조합을 찾는 것은 쉽지 않다. 선행 연구에서는 BO 기법을 사용하여 적절한 파라미터 값을 추출했지만, 파라미터 개수에 비례하여 차원이 커지는 문제가 발생한다. 본 논문에서는 통계적으로 파라미터를 분류하여 탐색 공간을 줄인 다음 단계적으로 BO 를 수행하는 PBO 방식을 제안한다. 파라미터 값을 랜덤하게 할당하여 벤치마킹한 결과값을 군집화한 후, 각 군집별로 파라미터와의 연관성을 분석해 높은 상관관계를 가진 파라미터를 매칭시켜 분류한다. 제안하는 방법론을 검증하기 위하여 8 가지 회귀 모델과의 비교 실험을 통해 제안한 방법 론의 우수성을 검증하였다.


<img width="669" alt="스크린샷 2023-04-01 오후 2 32 29" src="https://user-images.githubusercontent.com/126544082/229267534-becb632d-90f0-44f0-b6c8-9e41ccb4e8f5.png">

## Experiment

<img width="649" alt="스크린샷 2023-04-01 오후 2 34 45" src="https://user-images.githubusercontent.com/126544082/229267631-1d118a3b-bc62-42af-9b7e-ea97e57dbd30.png">

<img width="354" alt="스크린샷 2023-04-01 오후 2 34 56" src="https://user-images.githubusercontent.com/126544082/229267632-0ac7ab29-e6d0-4d43-b039-843098c4d4c4.png">

<img width="338" alt="스크린샷 2023-04-01 오후 2 35 00" src="https://user-images.githubusercontent.com/126544082/229267633-3531133f-73d4-41de-a0cb-c0119617a377.png">

본 연구에서는 BO 를 통해 파라미터 튜닝 작업 시, 파라미터를 분류하여 탐색 공간을 줄이는 연구를 수행하였다. 파라미터 전체를 탐색 공간으로 BO 를 진행하는 선행연구와는 달리 통계적 기법을 사용하여 파라미터를 분류한 후 BO 를 단계적으로 진행하는 PBO 방식을 제안하였다. 연구 결과 PBO 방식이 분류하지 않고 BO 를 진행한 경우보다 성능이 모두 높았으며, default 설정값과 비교했을 때도 단위 시간당 처리량이 대부분 높은 것을 확인하였다. 그리고 회귀모델 중에서는 LGBM 과 DT 에서 가장 높은 성능이 나타나는 것을 확인하였다.
