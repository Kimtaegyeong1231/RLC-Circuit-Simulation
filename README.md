# ⚡ RLC Circuit Transient Response Visualizer
> **MATLAB 기반 RLC 직렬회로 과도 응답 시각화 및 분석 프로젝트**

---

## 📌 1. 개요 (Overview)
본 프로젝트는 전기공학 전공을 준비하며 회로이론의 핵심 개념인 **RLC 직렬회로의 과도 응답(Transient Response)** 특성을 이해하고 MATLAB 실습 역량을 키우기 위해 진행한 미니 프로젝트였음. MATLAB Onramp에서 익힌 행렬 연산과 시각화 기능을 활용해 $R, L, C$ 소자 값 변동에 따른 커패시터 양단 전압 변화를 프로그램으로 구현했음.

---

## 📐 2. 주요 이론 및 수식 (Theoretical Background)

RLC 직렬회로에서 커패시터 양단 전압 $v_C(t)$는 아래의 2차 미분방정식을 따름.

$$\frac{d^2 v_C(t)}{dt^2} + \frac{R}{L}\frac{dv_C(t)}{dt} + \frac{1}{LC}v_C(t) = \frac{V_0}{LC}$$

프로그램에서는 시스템의 응답 특성을 결정하는 두 핵심 파라미터를 산출하여 회로 상태를 판별함.
* **감쇠 계수 ($\alpha$)**: $\alpha = \frac{R}{2L}$
* **고유 진동수 ($\omega_0$)**: $\omega_0 = \frac{1}{\sqrt{LC}}$

### 🔍 조건에 따른 3가지 감쇠 상태
| 상태 (State) | 조건 (Condition) | 물리적 특성 (Characteristics) |
| :--- | :--- | :--- |
| **과감쇠 (Overdamped)** | $\alpha > \omega_0$ | 저항이 크며, 진동 없이 목표 전압까지 천천히 수렴함 |
| **임계감쇠 (Critically Damped)** | $\alpha = \omega_0$ | 진동 없이 가장 빠른 속도로 목표 전압에 도달함 |
| **부족감쇠 (Underdamped)** | $\alpha < \omega_0$ | 저항이 작아 목표 전압 주변에서 진동(Overshoot)하며 수렴함 |

---

## 💻 3. 핵심 코드 구조 (Code Structure)

```matlab
%% 1. 회로 파라미터 및 초기화
clear; clc; close all;
L = 0.1; C = 100e-6; R = 2 * sqrt(L/C); V0 = 10;
alpha = R / (2 * L); omega0 = 1 / sqrt(L * C);
t = linspace(0, 0.05, 1000);

%% 2. 감쇠 조건 판단 및 수식 계산
if alpha > omega0
    state_str = '과감쇠 (Overdamped)';
    % 과감쇠 해 계산...
elseif abs(alpha - omega0) < 1e-4
    state_str = '임계감쇠 (Critically Damped)';
    Vc = V0 - V0*(1 + alpha*t).*exp(-alpha*t);
else
    state_str = '부족감쇠 (Underdamped)';
    % 부족감쇠 해 계산...
end

%% 3. 그래프 시각화
figure(1);
plot(t * 1000, Vc, 'b-', 'LineWidth', 2); grid on; hold on;
yline(V0, 'r--', '목표 전압 (10V)', 'LineWidth', 1.5);
xlabel('시간 (ms)'); ylabel('커패시터 전압 (V)');
title(['RLC 직렬회로 과도 응답 : ', state_str]);
