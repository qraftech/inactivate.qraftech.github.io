---
layout: post
title:  "Asynchronous Multi Network Learning"
author: Qraft
image: assets/images/2019-03-06/00_awa.png
categories: [ Qraft, Tech ]
---

### Introduction
금융 데이터는 기본적으로 Feature 종류에 비해 Feature Sequence 길이 짧은 편입니다. 이로 인해 오버피팅이 매우 쉽게 일어납니다. 일반적으로 딥러닝에서 오버피팅이 일어나는 것을 방지하기 위해 Dropout, L1/L2 Norm과 같은 Regularization 방법을 채택하지만, 금융데이터에서는 이를 적용하는 것이 꼭 적절하다고 말할 수 없습니다. 

### 왜 기존의 Regularization을 적용하기 어려운가?

![regression_example](https://raw.githubusercontent.com/qraftech/qraftech.github.io/master/assets/images/2019-03-06/regression%20example.png)


일반적으로 데이터 분포가 균질하지만 노이즈가 껴있는 경우에는 기존의 Regularization 방법론은 오버피팅 방지에 도움이 됩니다. 하지만 금융 데이터의 경우 데이터 분포가 균질하지 않으며, 전혀 관찰되지 않은 데이터 구간도 존재합니다. 이런 이유로 기존의 Regularization 방법론이 무조건적으로 도움되지 않기도 합니다.

예를 들어서 위 그림으로 좀 더 자세히 들여다보겠습니다. 회색 원 데이터는 train data에서 볼 수 없는 데이터이며 (가령 초저금리 구간 데이터), 검정색 원은 train data에서 관찰할 수 있는 데이터입니다. 

Regularization을 적용하지 않은 경우 Weight initialization에 따라 주황색, 파란색, 초록색 경우로 결과가 나올 수 있습니다. 이 세 개의 경우는 모두 비슷한 cost인 상황입니다. 


![gradient_descent_by_weight_initialization](https://raw.githubusercontent.com/qraftech/qraftech.github.io/master/assets/images/2019-03-06/gradient%20descent%20by%20weight%20initialization.png)


하지만 Dropout이나 L2 Norm을 적용할 경우 Regression은 파란색 선과 같이 나타나게 됩니다. 관찰되지 않은 데이터까지 고려하면 초록색이 가장 올바른 Regression이었지만, Regularization은 이런 결과가 나오지 못하도록 방지합니다.

따라서 데이터의 분포가 균질하지 않을 경우 일반적인 Regularization이 좋은 방법이 되지 않음을 알 수 있습니다. (물론 Noise에 대해 강건해지기 위해 약간의 Dropout은 도움되고는 합니다)


### 그래서 Asynchronous Multi Network Learning
오버피팅이 어느 정도 일어난다는 것을 인정하고 최대한 오버피팅을 간접적으로 피하기 위해 Multi Core, Multi GPU의 장점을 살려 Asynchronous Multi Network Learning을 생각해볼 수 있습니다.

네트워크가 도달해야하는 training 밖 데이터에서 오버피팅이 최소화되는 지점을 먼저 정하고 (위 그림에서 빨간색 별), 여러 네트워크를 각가 weight initialization을 시켜 그 지점에 도달하는 네트워크가 나오기까지 기다리는 방법입니다.

하지만 이런 방법은 Look-ahead bias, 즉 미래참조오류와 같은 문제점이 발생할 수 있기 때문에, validation data에서만 오버피팅의 방지를 검증해야합니다.

이 내용을 정리해 알고리즘 형태로 정리하면 아래와 같습니다.

![asynchronous worker algorithm](https://raw.githubusercontent.com/qraftech/qraftech.github.io/master/assets/images/2019-03-06/asynchronous%20worker%20algorithm.png)



이런 식으로 여러 네트워크를 병렬적으로 학습시켜 위 그래프에서 초록색과 같은 그래프에 도달시키는 것인 목표입니다. 하지만 validation data로만 오버피팅 여부를 감지할 수 있다는 측면에서 오버피팅을 완전히 피할 수 있는 것은 아니지만 실험적으로 이 알고리즘은 오버피팅을 피하는데 큰 역할을 하고 있습니다.

![asynchronous worker algorithm](https://raw.githubusercontent.com/qraftech/qraftech.github.io/master/assets/images/2019-03-06/cost.png)


금융에서 딥러닝을 적용하기 어렵지만, 데이터에 대해 이해하고 이에 맞는 기술을 개발하면 더 나은 금융 딥러닝 모형을 설계할 수 있습니다.
