---
layout: default
title: 전기기기
parent: Electricity
nav_order: 5
use_math: true
---

# 전기설비 기술기준 및 판단기준
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 직류기

### 직류발전기의 구조

(1) 직류발전기 3요소 : 전기자, 계자, 정류자

(2) 전기자 철심

* 규소강판+성층철심 : 철손 감소

* 규소강판 : 히스테리시스손 감소

* 성층철심 : 와류손(=와전류손=맴돌이 전류손) 감소

(3) 회전자

<div class="code-example" markdown="1">

회전자 속도 $v = 회전자원둘레 \times \frac{회전수}{60초} = \pi D \frac{N}{60} = 2\pi r \frac{N}{60} [m/s]$

</div>

(4) 브러쉬

탄소브러쉬 | 접촉저항이 큼, 정류가 잘됨, 직류기에 사용
금속흑연브러쉬 | 저전압 대전류용

### 직류기 권선법

|환상권
|고상권|개로권
||폐로권|단층권
|||이층권|중권(병렬권)|저전압,대전류<br>병렬회로수(a)=극수(p)=브러시수(b)
||||파권(직렬권)|고전압,저전류<br>병렬회로수(a)=2=브러시수(b)

* 주로 고상권 - 폐로권 - 이층권 - 파권 사용

### 직류기의 유기 기전력

<div class="code-example" markdown="1">

$자속 \phi \space 가 \space 있을 경우\space E = \frac{PZ \phi N}{60a} [V] , \space 자속 \phi 가 \space 없을 \space 경우\space E = V \pm I_aR_a$

</div>

(P:자극수, Z:전기자도체수, $\phi$:극당 자속수, N:분당회전수,a:병렬회로수)<br>
(V:단자전압, $I_a$:전기자전류, $R_a$:전기자저항, 발전기:+, 전동기:-)

<div class="code-example" markdown="1">

$E \propto \phi, E \propto N, \phi \propto \frac{1}{N}$

</div>