---
layout: default
title: 전력공학
parent: Electricity
nav_order: 3
use_math: true
---

# 전력공학
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## 사람이름 관련 문제

<div class="code-example" markdown="1">

### 켈빈(Kelvin)법칙 : 경제적인 전선 굵기 산정

<br>

### 피크(Peek) 식 : 코로나 손실과 코로나 임계전압

$P_c = \frac{241}{\delta}(f+25)\sqrt{\frac{d}{2D}}(E-E_0)\times10^{-5} [kW/km/line]$

$E_0 = 24.3m_0m_1\delta d\log{(\frac{D}{r})} [kV]$

$(\delta:공기밀도, f:주파수, d:전선의 지름, D:전선간 거리, E:대지전압, E_0:임계전압)$

<br>

### 스틸(Still) 식 : 경제적인 송전 전압 산정

$V = 5.5\sqrt{0.6l+\frac{P}{100}} [kV]$

</div>

---

## 암기팁

입진미 출지적 | 입력 콘덴서는 진상출력이며 미분기로 작동<br>출력 콘덴서는 지상출력이며 적분기로 작동
중과진C 경부지L | 중부하$(L\uparrow)$ : 동기조상기 과여자 진상전류 -> C 특성 -> 역율 개선<br>경(무)부하$(L\downarrow)$ : 동기조상기 부족여자 지상전류 -> L 특성 -> 역률 개선

---

## 이도

$이도\space D = \frac{WS^2}{8T} [m] \space (W:전선중량 , S:경간 , T:수평장력)$<br>

$인장\space하중 = 수평장력(T) \times 안전률$<br>

$전선의\space실제길이\space L = S + \frac{8D^2}{3S} [m]$<br>

$지지점에서의\space전선장력\space T_0 = T + WD [kg]$<br>

$전선의\space평균높이\space H_0 = H - \frac{2}{3} \times D [m]$

---

## 전압강하-전압강하율, 전력손실-전력손실율

전압강하 | $V_d = V_s - V_R = \sqrt{3}I_R(Rcos \theta + Xsin \theta) = \frac{P}{V_R}(R+Xtan \theta) [V]$ | $V_d \propto \frac{1}{V}, P \propto V$
전압강하율 | $\epsilon = \frac{V_s - V_R}{V_R} = \frac{\sqrt{3}I_R(Rcos \theta + Xsin \theta)}{V_R} = \frac{P}{V_R^2}(R+Xtan \theta) [\%]$ | $\epsilon \propto \frac{1}{V^2}, P \propto V^2$
전력손실 | $P_l = 3I^2R = 3(\frac{P}{\sqrt{3}Vcos\theta})^2R = \frac{P^2R}{V^2cos^2\theta} = \frac{P^2\rho l}{V^2cos^2\theta A} [W]$ | $P_l \propto \frac{1}{V^2}, P \propto V$
전력손실률 | $k = \frac{P_l}{P} = 3(\frac{P}{\sqrt{3}Vcos\theta})^2R\frac{1}{P} = \frac{PR}{V^2cos^2\theta} = \frac{P\rho l}{V^2cos^2\theta A} [\%] $ | $k \propto \frac{1}{V^2}, P \propto V^2$

전력손실이 일정할 때(기본) $P \propto V$ , 전력손실률이 일정할 때 $P \propto V^2$<br>
전압과 전력손실 변경시 새로운 전력 $P^\prime = \frac{k^\prime}{k} \frac{V^\prime}{V} P$<br>
전압과 전력손실률 변경시 새로운 전력 $P^\prime = \frac{k^\prime}{k} (\frac{V^\prime}{V})^2 P$

---

## 리액터와 콘덴서

```
리액터
직렬 리액터 : 제5고조파 제거
병렬 리액터 : 분로 리액터.  페란티 억제(과진상, 수전단전압 > 송전단전압), 지상전류 위상개선(조상설비)
소호 리액터 : 접지용, 지락전류 소멸, 아크 소멸
한류 리액터 : 단락전류 제한
```
```
콘덴서(축전기)
직렬 콘덴서 : Static Condenser, 전압강하 방지, 계통 안정도 향상
병렬 콘덴서 : 전력용 콘덴서, 진상전류로 역률을 개선(전력손실 경감)
```