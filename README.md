# SWCON_CapstoneDesign (2022-1)
소프트웨어융합캡스톤디자인
# Project title
: 웨어러블 센서 기반 스트레스 감지 모델 개발

* Student list
JiYeon Lee

## Overview
* Needs, problems

스트레스에 장기간 노출되면 고혈압 및 관상동맥 질환을 비롯한 여러 질병을 유발하는 것으로 알려져 있다. 따라서 사람들이 스트레스가 많은 상황을 인지하고 대처하기 위해 필요한 조치를 취할 수 있도록 하는 것이 중요하다. 스트레스 감지 모델을 통해 사전에 관리하고 예방하여 스트레스를 받을 것으로 예상되는 사람들의 삶에 긍정적인 효과를 기대할 수 있다.

* Goals, objectives (evaluation)

- 웨어러블 센서 데이터를 분석해 스트레스를 감지하는 모델을 개발한다. 
- 참고 논문보다 성능이 개선된 스트레스 감지 모델을 만든다.

## Results

dataset : WESAD: Multimodal Dataset for Wearable Stress and Affect Detection (available : https://uni-siegen.sciebo.de/s/HGdUkoNlW1Ub0Gx)
preprocess code : pkl_to_csv.ipynb / preprocess_binary_class.ipynb
model code : final_model_binary(i)_smoteenn.ipynb

Resampling을 적용하지 않았을 때에도 13명의 subject에 대해 성능이 개선된 스트레스 감지 모델을 만들었고, resampling을 통해 성능을 더욱 향상시켜 14명 모든 subject에 대해 성능을 개선시켰다.

WESAD data는 wrist센서와 chest센서에서 수집된 데이터였고, 데이터를 제공한 원 저자에 의하면 chest 착용 기구만을 사용하여 얻은 데이터가 chest와 wrist를 함께 사용하는 것보다 더 나은 결과를 제공한다고 하여 chest 센서에서 수집된 데이터만을 이용해 모델이 적용하였다. subject 1과 subject 12는 sensor malfunction으로 raw data로부터 제거되어 제공되어졌고, subject 8은 모두 non-stress인 경우만 존재해 제외하고 subject 14명에 대해 subject 별 스트레스 감지 모델을 만들었다. 원저자에 의하면 ACC 센서 데이터는 생리학적 데이터(EDA, TEMP 등)를 사용한 결과에 비해 분류 점수가 낮다고 했기 때문에 제외했다. Imbalanced data를 처리하기 위해 resampling 기법 SMOTE, RUS, SMOTE-ENN을 subject 1명에 대해 우선 적용해본 후 가장 성능이 좋은 SMOTE-ENN 방식을 14명의 subject 각각의 모델을 만드는 데에 사용했으며, 머신러닝 기법으로는 random forest를 이용해 모델링했다. Accuracy을 이용해 성능 평가를 진행했다.

## Conclusion
모델을 생성할 때 class 개수를 4개가 아닌 2개로 만들어줌으로써 좀 더 명확한 분류를 할 수 있도록 만들었으며, wrist 데이터가 아닌 chest 데이터를 사용했다. 또한 imbalanced data를 보완해줄 수 있는 resampling 기법인 SMOTE-ENN을 추가적으로 적용했다는 점에서 기존 연구와 차별점이 있다. Colab에서 최대로 사용할 수 있는 RAM을 초과해 모든 subject에 대한 하나의 모델을 만드는 것은 해보지 못했지만, RAM을 더 사용할 수 있는 환경이라면 하나의 모델을 만들어보고 성능을 향상시키는 연구도 할 수 있을 것이다. 또한 wrist 데이터만을 이용해보거나 resampling 기법을 바꿔서 성능을 향상시키는 방법을 찾는 후속 연구도 진행할 수 있을 것이다.

## References
[1] Fitri Indra Indikawati1 & Sri Winiarti1(2020). Stress Detection from Multimodal Wearable Sensor Data. IOP Conf. Series: Materials Science and Engineering, 771, 012028
[2] Prerna Garg, Jayasankar Santhosh, Andreas Dengel, and Shoya Ishimaru. 2021. Stress Detection by Machine Learning and Wearable Sensors. In 26th International Conference on Intelligent User Interfaces (IUI ’21 Companion), April 14–17, 2021, College Station, TX, USA. ACM, New York, NY, USA, 5 pages.
