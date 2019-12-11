---
layout: post
title:  "Factor Investing Introduction"
author: Qraft
image: assets/images/2019-03-06/3d-factor-model.png
categories: [ Qraft, Investment ]
---



### 팩터 투자(Factor investing)란?

**장기적으로 시장 대비 초과수익을 창출할 수 있는 요인(Factor)에 대한 투자라고 할 수 있습니다.**

팩터 투자란 자산의 수익률에 영향을 미치는 다양한 요인(factor)를 기반으로 투자하는 것을 말합니다. 배경을 거슬러 올라가보면 1963년  자산가격이론인 CAPM에서 시작합니다. CAPM의 경우, 자산의 초과수익을 시장 수익률 한가지 Factor로 설명하는 이론입니다.

![capm](/assets/images/2019-03-06/capm.png)

<span class="image_caption"> *Capital Asset Pricing Model Equation* </span>


위 수식에서 보는 것처럼 자산수익은 시장(Market) 요소 하나에 의해서 설명하는 이론입니다. 하지만 경험적으로 CAPM을 이용했을때, 정확한 기대수익률을 가져다 주지 못합니다. 당연하게도 금융자산의 수익률을 결정하는데 시장 요소 뿐만 아니라 다양한 요인들이 작용할 수 있겠죠. 이러한 이유로 Multi factor model을 생각하게 되고, 그래서 등장한 것이 1993년 발표된 Fama-French 3 Factor Model(이하 FF3F)입니다.


![ff3f](/assets/images/2019-03-06/ff3f.png)


FF3F는  자산의 초과수익을 결정하는데 시장요인 외에도 다른 팩터가 존재함을 밝히고 이를 반영한 모델입니다. 위에서 SMB는 small market capitalisation minus big의 약자로써 Size Factor입니다. 이는 주식이 소형주일 수록 수익률이 높다라는 것을 의미하고, 이러한 효과를 Size effect라고 합니다. 반면 HML의 경우, high book to price ratio minus를 의미하여 이는 Value Factor를 나타냅니다. 이는 장부가치와 시장가치의 비율로써 가치주가 장기적으로 높은 수익률을 내는 효과를 반영한 요인입니다.

다시말해, FF3F에서는 CAPM과 달리 Size와 Value를 추가적인 리스크 프리미엄으로 고려한다고 할 수 있습니다.


### 다양한 Factor들의 등장

FF3F 모델 이후 다양한 논문에서 자산수익률을 결정하는 Factor들이 제시되고 있습니다. Size와 Value를 제외한 대표적인 Factor는 아래와 같습니다.

- 퀄리티 : 재무 구조와 수익성이 뛰어난 종목이 향후 수익률이 뛰어남

- 저변동성 : 변동성이 낮은 종목들이 장기적으로 수익률이 뛰어남

- 모멘텀 : 최근 상승세를 기록한 종목이 더 오르는 경향이 존재함

- 고배당 : 배당을 많이 주는 종목이 투자 수익률이 우선함

이외에도 실질금리, 인플레이션 등의 Macro 경제 요인들이 존재하며, 주식이 아닌 자산군에는 또 다른 Factor들이 존재합니다.

수많은 팩터들이 등장하면서 “팩터 과잉” 상태라고 말할 수 있기에, 실제로 팩터를 기반으로 투자를 할 때 다양한 시장과 기준으로 팩터 프리미엄이 검증이 필요합니다.
