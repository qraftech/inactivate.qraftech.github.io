---
layout: post
title:  "Introduction to Qraft Deep Learning Asset Management Framework"
author: Qraft
image: assets/images/2019-03-06/00.png
categories: [ Qraft, Tech ]
---

### 1) Multi-Channel Feature Extraction Deep Neural Network for Financial Data (Q-DNN)

Tabular 데이터로 들어온 복합 금융데이터를 raw data로 넣어주게 되면 일반적으로 학습이 거의 되지 않습니다. 이는 금융데이터의 노이즈 특성 때문입니다.

이에 정보를 핵심정보로 압축해 학습에 이용해야 하며, 금융 데이터의 특성을 고려해 핵심정보를 특징으로 추출하기 위한 네트워크 구조를 설계했습니다. 



### 2) Reinforcement Learning with Adversarial Multi Actors for Financial Data (Q-DRL)

Qraft는 지도학습이 어려운 문제를 해결하기 위해 Proximal Policy Optimization, Soft Actor Critic 기반의 금융데이터용 강화학습 알고리즘을 개발했습니다.

예를 들어 최적 주문집행과 같은 문제는 정답 레이블을 제공하기가 어렵습니다. 따라서 강화학습 알고리즘을 통해 문제를 해결합니다.

최적 주문집행 문제에서 결정해야할 것은 주문시점에 따른 총 주문량, 주문의 시장가 및 지정가 배분, 호가창 배분 등이 있습니다. 이 결정요인들은 모두 이산적이지 않고 연속적인 값들이며 단일 Actor로 학습하기 어려운 문제입니다.

따라서 Qraft는 복수의 Actor가 역할을 맡아 의사결정을 내리지만, 서로 간의 견제를 통해 학습이 원활하게 이루어지도록 설계했습니다.
 
 

### 3) Qraft Asynchronous Multi-Network Training Engine (QAMTE)

그러나 여전히 initial value impact가 작지 않기 때문에 overfitting 가능성이 존재합니다.

이에 Qraft는 Multi threading, Multi-GPU 병렬 연산을 활용해 개별적으로 초기화된 여러 네트워크를 동시 학습시킵니다. 학습 과정에서 검증 데이터 상 과최적화가 보이는 모델을 제거하고, 성과가 좋은 모델을 살리는 방식과 같이 적자생존 방식을 통해 학습을 진행시키며, 최종적으로 모델들에 대한 앙상블을 통해 오버피팅 최소화합니다.

이를 통해 좀더 Robust한 인공지능 학습이 가능합니다.



### 4) Uncertainty Quantification

금융데이터는 노이즈가 심하고 feature 수에 비해 상대적으로 time-series 데이터 길이가 짧습니다. 학습 데이터로 모든 case에 대한 데이터가 있는 것이 아닙니다.

학습된 데이터와 비슷한 state라면 신뢰도가 높지만 그렇지 않은 경우 uncertainty가 높다고 할 수 있습니다. 예를 들어 근래와 같은 초저금리 상황은 딥러닝 모델이 학습할 수 없었던 상황입니다. 이런 상황에서의 모델 출력 결과는 uncertainty가 높을 수 밖에 없습니다. 데이터 부족으로 낯선 상황에서는 확신을 가지고 투자를 하는 것보다 조금 더 보수적으로 투자하는 것이 우월전략입니다.

Uncertainty 모형은 조금 더 보수적으로 안정적인 투자를 할 수 있도록 도와줍니다.

Qraft는 MC Dropout, MC Batch Normalization 외에도 Deep Regression + GPR 등의 방법론을 활용합니다.

 

### 5) Multi Genetic Algorithm for hyper-parameter tuning

Genetic algorithm은 19C 후반에 개발된 알고리즘입니다. 오래된 알고리즘이지만, 신경망 학습과 더불어 파라미터 최적화 자체에는 매우 효과적입니다.

GA를 Qraft Asynchronous Multi-Network Training Engine과 함께 응용하면, overfitting에서 벗어날 가능성이 더 높습니다.

 

### 6) Qraft Reward function targeted Deep Neural Network Framework for Financial Data

노이즈가 심한 금융 데이터의 특성상 금융 포트폴리오의 비지도학습이 어려습니다. 이런 경우에 지도학습이 좀 더 유리한데, 지도학습을 하기 위해서는 최적의 포트폴리오를 정답 label로 제공해야하는 문제점이 존재합니다.

Qraft는 보상함수를 최대화하는 최적의 포트폴리오를 실시간으로 연산하고, 이를 통해 딥러닝 레이블로 활용해 금융 영역에서 범용적으로 이용할 수 있는 Framework를 개발했습니다.

보상함수는 상황에 맞춰 변경할 수 있으며 클라이언트가 보수적인 성향일 경우 보수적인 보상함수를 설정해 커스터마이즈가 바로 가능한 형태입니다. 

예를 들어 클라이언트가 보수적인 성향일 경우 변동성을 최대한 제한하고, 장기간의 기대수익률을 최대화하도록 설계할 수 있습니다.

이 Framework는 Multi-Channel Feature Extraction Deep Neural Network for Financial Data, Qraft Asynchronous Multi-Network Training Engine과 함께 적용할 경우 매우 효과적인 것으로 나타나고 있습니다. 
