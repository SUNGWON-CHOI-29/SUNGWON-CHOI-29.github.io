---
layout: post
title: Medium - The Best machine learning research so far(2019)
description: >
  <a href="https://medium.com/@ODSC/the-best-machine-learning-research-of-2019-so-far-954120947794">원문 링크 - ODSC(Open Data Science)</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 머신러닝 연구 동향 파악

![500x400](https://cdn-images-1.medium.com/max/1600/0*HXLd67zuwj3VB7XT.png)

## Transfer learning for vision-based tactile sensing

인간의 감각기관을 흉내내는 컴퓨터 능력의 발전은 고르지 않은 발전양상을 보여왔다.

오감 중에 특히나 촉각은 그 중 가장 연구가 더딘 분야였다.

최근에 촉각에 대한 시각기반 전이학습에 관한 논문이 발표되었다.

탄성물질이 힘을 받을 때 물체가 변형되는 것을 포착해 부드러운 표면의 힘 분포를 학습함으로써

촉각 모델을 훈련시키는데 시스템의 시각이 보조역할을 해주는 것이다.


## Self-Supervised Learning of Face Representations for Video Face Clustering

최근 몇년간 얼굴 인식 기술은 꾸준히 발전해 왔고 연구원들은 이 기술의 한계와 적용 방법을 많이 고민해왔다.

비디오 연구를 위해 고안된 시스템의 경우 단순히 주인공을 식별하는 것에서 얼굴 지식을 사용해 스토리를 분석

하는 것으로 연구 방향이 옮겨갔다.

토론토 대학에서는 최근 발표한 비디오 얼굴 클러스터링을 위한 얼굴 표현 자기주도 학습 논문에서

연구팀은 어떤 캐릭터가 어디에 등장하는지 예측하는 능력에 대해서 강조한다.

이 연구를 위해 주어진 데이터셋을 사용하는 비지도학습 모델과 제한된 양의 매우 정교한 얼굴 인식 모델을 사용하였다.

비디오 얼굴 분석에 비용과 시간이 감소하는 결과를 통해 앞으로 영상 분석에 더욱 큰 발전이 예상된다.


## Competitive Training of Mixtures of Independent Deep Generative Models

VAEs와 GANs는 비지도학습 모델 중 가장 두드러진 모델이지만 각각 큰 장애를 가지고 있다.

VAEs의 경우 고화질의 샘플을 수급하는 것이 어렵다는 것이고

GANs의 경우 학습의 총 횟수가 제한된다.

최근 연구에서는 훈련 분포의 독립적인 부분에 초점을 맞춰 복수의 모델을 병렬적으로 수행하는 것에 대한

결과를 발표했다. 모델의 직관적인 사용, 복수의 모델을 동시에 사용하는 것이 보다 강력한

모델 훈련 환경을 만들고 보다 많은 데이터를 사용할 수 있게 만든다고 말했다.


## Can You Trust This Prediction? Auditing Pointwise Reliability After Learning

머신러닝이 일상 업무 운영속으로 더욱 깊이 통합됨에 따라 예측모델의 신뢰성과 정확성을 측정하려는 욕구가

늘고 있다. 정확도를 측정하는 많은 방법들은 학습모델에서 오류를 제거하는 것이지만 활성모델의 정확도를

측정하는 방법은 거의 없다.

이것을 위해 존스홉킨스에서 RUE(Resampling Uncertainty Estimator) 알고리즘을 발표했다.

이것은 학습모델이 다른 데이터를 학습했을 경우 예측이 얼마나 달라졌는지 감사하는 것으로써

머신러닝이 학습 전과 후 모두에서 정확성을 분석할 수 있도록 하는 것이다.

## Summary

* 머신러닝은 금융과 HR분야의 업무 자동화를 이끌었고 계속해서 발전이 이루어 지고 있다.
* 광고 및 의학분야에 걸쳐 머신러닝은 더욱 폭 넓게 활용될 것이다.
