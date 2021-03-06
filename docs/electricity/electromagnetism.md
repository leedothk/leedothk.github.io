---
layout: default
title: 전기자기학
parent: Electricity
nav_order: 3
use_math: true
---

# 전기자기학
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## 상수

---

### 전자

<br>

전자의 질량 : $9.1093826 \times 10^{-31}$ [kg]<br><br>
전자 1개의 전하량 : $1.6021773349 \times 10^{-19} [C]$<br><br>
1쿨롱에 해당하는 전자 갯수 :$\frac{1}{1.6021773349 \times 10^{-19}} = {6.24150962915265 × 10^{18}} [개]$

---

### 전계 자계

<br>

진공의 유전률 : $\epsilon_0 = 8.8541878176 \times 10^{−12} [F/m]$ (매질이 저장할 수 있는 전하량)<br><br>
진공의 투자율 : $\mu_0 = 4\pi \times 10^{-7} [H/m]$ (매질이 자화되는 정도)<br><br>
빛의 속도 : $C = 3 \times 10^8 [m/s]$<br><br>
유전률, 투자율, 광속의 관계 : $\epsilon_0 = \frac{1}{C^2\times\mu_0}$<br><br>
쿨롱 상수 : $k = \frac{1}{4\pi\epsilon_0} = 8.99 \times 10^9 [N \cdot m^2 / C^2]$<br><br>
전기력선의 갯수(가우스 법칙 $\in$ 맥스웰 방정식) : $N = \frac{Q}{\epsilon_0} = \frac{1}{8.8541878176 \times 10^{−12}} = 1.13 \times 10^{11} [개]$

---

### 에너지

<br>

$1 [kg] = 9.8 [N]$<br><br>
$1 [N \cdot m] = 1 [J] = 1 [W \cdot s] = 0.239 [cal]$<br><br>
$1 [kWh] = 860 [kcal]$

---

## 정전계

### 전위, 정전용량, 저항, 인덕턴스

<div class="code-example" markdown="1">
* 기본공식

$C = \frac{Q}{V}[F]$ | $R = \frac{\rho\epsilon}{C}[\Omega]$ <br> $RC = \rho\epsilon[\Omega]$ | $L = \frac{\mu\epsilon}{C}[H]$ <br> $LC = \mu\epsilon[H]$

* 구도체

$V = \frac{Q}{4\pi\epsilon_0 a}[V]$ | $C = 4\pi\epsilon_0a[F]$ | $R = \frac{\rho}{4\pi a}$ | $L = \frac{\mu}{4\pi a}$

* 동심원통도체

$V = \frac{\lambda}{2\pi\epsilon_0}\ln\frac{b}{a}[V]$ | $C = \frac{2\pi\epsilon_0l}{\ln\frac{b}{a}}[F \cdot m]$ <br><br> $C^\prime = \frac{2\pi\epsilon_0}{\ln\frac{b}{a}}[F]$ | $R = \frac{\rho}{2\pi l}\ln\frac{b}{a}[\Omega \cdot m]$ <br><br> $R^\prime = \frac{\rho}{2\pi}\ln\frac{b}{a}[\Omega]$ | $L = \frac{\mu}{2\pi l}\ln\frac{b}{a}[H \cdot m]$ <br><br> $L^\prime = \frac{\mu}{2\pi}\ln\frac{b}{a}[H]$ 

* 평행도선

$V = \frac{\lambda}{\pi\epsilon_0}\ln\frac{d}{a}[V]$ | $C = \frac{\pi\epsilon_0l}{\ln\frac{d}{a}}[F \cdot m]$ <br><br> $C^\prime = \frac{\pi\epsilon_0}{\ln\frac{d}{a}}[F]$ | $R = \frac{\rho}{\pi l}\ln\frac{d}{a}[\Omega \cdot m]$ <br><br> $R^\prime = \frac{\rho}{\pi}\ln\frac{d}{a}[\Omega]$ | $L = \frac{\mu}{\pi l}\ln\frac{d}{a}[H \cdot m]$ <br><br> $L^\prime = \frac{\mu}{\pi}\ln\frac{d}{a}[H]$

</div>

## 전자장

### 맥스웰 방정식

<div class="code-example" markdown="1">

| 이름                     | 미분형                                                | 적분형 | 
|:-------------------------|:-----------------------------------------------------|:-------|
| 가우스 전속 (+전하와 -전하는 홀로 존재할 수 있음)|$\nabla \cdot D = \rho_v$ | $\oint D \cdot dS = \int_v \rho_v dv = Q$|
| 가우스 자속 (N극과 S극은 홀로 존재할 수 없음) | $\nabla \cdot B = 0$ |$\oint B \cdot dS = 0$|
| 패러데이 법칙 (자기장이 변하면 전류가 생성됨)  | $\nabla \times E = - \frac{\partial B}{\partial t} = - \mu \frac{\partial H}{\partial t}$ | $\oint E \cdot dl = \int_s (- \frac{d B}{dt})dS$|
| 앙페르 주회적분 (전도전류 또는 변위전류는 자계발생) | $\nabla \times H = i_c + i_D = kE + \epsilon \frac{\partial E}{\partial t}$ | $\oint_l H \cdot dl = \int_s i \cdot dS = \int_s (i_c + \frac{\partial D}{\partial t})dS$|

</div>

---

