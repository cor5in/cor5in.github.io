---
layout: project
title: 'System Level Simulator'
caption: System Level Simulator for Green Network
description: >
  Simulator for cell on/off & data offloading in 5G environment
date: '12-11-2024'
image: 
  path: /assets/img/projects/sls.jpg
  srcset: 
    1920w: /assets/img/projects/sls.jpg
    960w:  /assets/img/projects/sls@0,5x.jpg
    480w:  /assets/img/projects/sls@0,25x.jpg
links:
  - title: Link
    url: https://github.com/cor5in/AIMM-simulator
sitemap: false
---

# SLS for 5G

## Procedure
1. 기지국의 트래픽이 일정 수준 이하로 떨어지면 `Cell Off`
2. Off 된 기지국의 서비스를 만족하기 위해 다른 기지국들이 UE들을 커버해야 함

> Cell Traffic 예측 $$\rightarrow$$ 데이터 오프로딩


Offloading 이후 모든 기지국의 총 전력량이 최소가 되게 결정해야 함

- 목표: 소모 전력량 최소
- 제약조건: User QoS 만족
{:.note}

## Path Loss 모델

- **800MHz와 1.8GHz**: `COST 231-HATA`
- **3.5GHz**: `UMi(Urban Micro)` 

|---|---|---|
|주파수|800MHz|1.8GHz| 3.5GHz |
|SCS(Subcarrier Spacing)|15kHz|15kHz|30kHz|
|RB의 수|50개|100개|136개|

*References: TS 38.104*

## UE Mobility 모델
- eMBB(enhanced Mobile Broadband)
  - 보행자
  - 자동차

*References: TR 38.901, TR 38.802*

## UE 트래픽 모델

*References: TR 36.814, TR 38.913*

## Cell Power Consumption 모델


---

## 트래픽 예측 모델

### Statistical
- Prophet
- ARIMA

### Machine Learning
- Random Forest
- SVR

### Deep Learning
- LSTM
- GRU

---

## 데이터 오프로딩 알고리즘

### Game Theory: Stackelberg Game

Stackelberg 게임은 셀들간의 계층적 관계를 효과적으로 모델링할 수 있기 때문에 선택하였음
{.note}

- Off 하는 셀은 off-loading 전략을 먼저 결정하고, off-loading을 받는 셀은 이를 기반으로 수용량을 결정함
- Stackelberg game의 `Backward Induction`을 통해 안정적인 균형 해를 찾을 수 있음

### Deep Reinforcement Learning: PPO or IPPO
