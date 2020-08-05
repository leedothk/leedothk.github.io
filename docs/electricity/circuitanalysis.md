---
layout: default
title: 회로이론
parent: Electricity
nav_order: 3
use_math: true
---

# 회로이론
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## 정현파 교류

---

### 파형별 실효값, 평균값

<div class="code-example" markdown="1">

| 파형           | 실효값                 | 평균값($\frac{면적}{주기}$) | 
|:--------------|:-----------------------|:---------------------------|
| 정현파         | $\frac{V_m}{\sqrt{2}}$ | $\frac{2V_m}{\pi}$        |
| 정현반파       | $\frac{V_m}{2}$        | $\frac{V_m}{\pi}$          |
| 삼각파(톱니파) | $\frac{V_m}{\sqrt{3}}$  | $\frac{V_m}{2}$           |
| 구형반파       | $\frac{V_m}{\sqrt{2}}$ | $\frac{V_m}{2}$            |
| 구형파         | $V_m$                  | $V_m$                     |

</div>

---

## 라플라스 변환

|               | f(t) | F(s) |
|:-----|:-----|
| 단위임펄스함수 | $\delta(t)$ | 1 |
| 단위계단함수   | $u(t), 1$      | $\frac{1}{s}$ | 
| 단위경사함수   | $t$         | $\frac{1}{s^2}$ |
| | $\sin \omega t$ | $\frac{\omega}{s^2 + \omega^2}$ |
| | $\cos \omega t$ | $\frac{s}{s^2 + \omega^2}$ |
| | $e^{-at}$ | $\frac{1}{s + a}$ |