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

## Traffic Capacity 모델

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

---

## UE 트래픽 모델

*References: TR 36.814, TR 38.913*

---

## 주파수 별 최대 커버리지

### 개요

무선 통신 네트워크에서 각 주파수 대역의 최대 커버리지는 기지국의 송신 전력, 수신기 감도, 환경에 따른 경로 손실 모델에 따라 달라짐. 본 시뮬레이터에서는 **800 MHz**은 **Okumura-Hata** 모델 **1.8GHz** 대역에는 **Cost 231-Hata** 모델, **3.5GHz** 대역에는 **UMi NLOS** 모델을 적용하여 최대 커버리지를 계산하였다.


### 필요 파라미터
- 송신 전력($$P_{tx}$$): 기지국에서 송신하는 신호의 전력(43 dBm)
- 수신 감도($$P_{rx_min}$$): UE가 안정적으로 신호를 수신하기 위한 최소 전력 (-100 dBm)
- 기지국 높이($$h_{BS}$$): 기지국 안테나의 높이 (20m)
- UE 높이($$h$$): UE의 높이 (1.5m)
- 안테나 이득: $$G_{BS} = 0 dBi$$, $$G_{UE} = 0 dBi$$

#### 경로 손실 한계($$L_{path, max}$$)

$$
L_{path, max} = P_{tx} + G_{BS} + G_{MS} - P_{rx, min} = 143 dB
$$

- 송신 전력($$P_{tx}$$): 기지국에서 송신하는 신호의 전력(43 dBm)
- 수신 감도($$P_{rx_min}$$): UE가 안정적으로 신호를 수신하기 위한 최소 전력 (-100 dBm)
- 안테나 이득: $$G_{BS} = 0 dBi$$, $$G_{UE} = 0 dBi$$ 

##### 800 MHz [Okumura-Hata]

$$
L = 69.55 + 26.16 log_{10}(f) - 13.82 log_{10}(h_b) - a(h_m) + (44.9 - 6.55 log_{10}(h_b))log_{10}(d)
$$

  - $$f$$ = 800 MHz
  - $$h_b$$ = 20m
  - $$h_m$$ = 1.5m
  - $$L$$ = 143 dB

도시 지역에서의 보정값 $$a(h_m)$$는 다음과 같음 

$$
a(h_m) = (1.1 log_{10}(f) - 0.7)h_m - (1.56 log_{10}(f) - 0.8)
$$



##### 1.8 GHz [COST 231-Hata]

$$
L = 46.3 + 33.9 log_{10}(f)-13.82log_{10}(h_b)-a(h_m)+(44.9-6.55log_{10}(h_b))log_{10}(d)+C
$$

- $$f$$ = 1800 MHz
- $$h_b$$ = 20m
- $$h_m$$ = 1.5m
- $$L$$ = 143 dB
- 도시 지역 보정 값 $$C$$ = 3 dB

##### 3.5 GHz [UMi]

$$
L_{NLOS} = 22.4 + 35.3 log_{10}(d) + 21.3 log_{10}(f) - 0.3 \times (h_m - 1.5)
$$

- $$d$$: 송수신 거리(m)
- $$f$$: 주파수 (GHz)
- $$h_m$$: UE의 높이(m)


|---|---|---|---|
|주파수 대역|모델|경로 손실 한계|최대 커버리지|
|800 MHz|Okumura-Hata|143 dB|2.67km|
|1.8 GHz|COST 231-Hata|143 dB|1.09km|
|3.5 GHz|UMi(NLOS)|143 dB| 745.4 m|

*References:*

*- TR 45.820(Okumura-Hata)* 

*- TR 36.942(COST 231-Hata)* 

*- TR 38.901(UMi)*

---

## BS Power Consumption 모델

### 기지국 전력 소모 모델

BS의 전력 소모는 기본 전력 $$P>0$$에서 시작하며, downlink 송신 전력 $$P_t$$에 따라 선형적으로 증가한다. 

#### 총 전력 소비 모델

$$
P = P_o + \vartriangle P \times P_t
$$

   - $$P_0$$: 기본 전력 소비 (712W)
   - $$\vartriangle P$$: 전력 증폭 효율 (14.5)
   - $$P_t$$: 전송 전력




#### 전송 전력 - $$P_t$$

$$
P_{t,k} = 
\begin{cases} 
\frac{\Gamma N_0 W}{-D \ln(1 - \epsilon)} \times \frac{2^{\frac{K b}{W}} - 1}{K} \times \left( \frac{r_k}{r_0} \right)^{\alpha}, & \text{if } r_k \geq r_0, \\[10pt]
\frac{\Gamma N_0 W}{-D \ln(1 - \epsilon)} \times \frac{2^{\frac{K b}{W}} - 1}{K}, & \text{otherwise}.
\end{cases}
$$

- $$r_k$$: $$k$$번째 UE와 MBS 간의 거리
- $$r_o$$: 기준 거리 (1m)
- $$\alpha$$: path-loss exponent(도시 환경이므로 2.5)
- $$K$$: 전체 UE 수
- $$b$$: 요구되는 데이터 전송률
- $$W$$: 시스템 대역폭

*References: [IEEE]Green 5G Heterogeneous Networks through  Dynamic Small-Cell Operation*

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

Stackelberg 게임은 cell들간의 계층적 관계를 효과적으로 모델링할 수 있기 때문에 선택하였음
{:.note}

- Off 하는 셀은 off-loading 전략을 먼저 결정하고, off-loading을 받는 셀은 이를 기반으로 수용량을 결정함
- Stackelberg game의 `Backward Induction`을 통해 안정적인 균형 해를 찾을 수 있음

### Deep Reinforcement Learning: PPO or IPPO
