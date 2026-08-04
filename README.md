# ⚡ RLC Circuit Simulation (RLC 회로 시뮬레이션)

MATLAB을 활용하여 RLC 회로의 응답 특성을 시뮬레이션하고, 감쇠 조건(과감쇠, 임계감쇠, 부족감쇠)에 따른 전압 변화를 가시화하는 프로젝트입니다.

---

## 📌 프로젝트 소개
RLC 직렬 회로에서 저항($R$), 인덕턴스($L$), 커패시턴스($C$) 값에 따라 달라지는 회로의 과도 응답(Transient Response)을 해석합니다.

* **과감쇠 (Overdamped):** $\alpha > \omega_0$
* **임계감쇠 (Critically Damped):** $\alpha = \omega_0$
* **부족감쇠 (Underdamped):** $\alpha < \omega_0$

설정한 회로 파라미터에 맞춰 시간($t$)에 따른 커패시터 전압($V_c$) 변화 그래프를 자동으로 출력합니다.

---

## 🛠️ 사용한 언어 및 도구
* **Language:** MATLAB
* **Environment:** MATLAB R202x 이상 (또는 GNU Octave)
* **Version Control:** Git, GitHub

---

## 📁 파일 구성
* `main_rlc_simulation.m`: RLC 회로 해석 및 그래프 출력 메인 스크립트
* `Criticallydamped_result.png`: 임계감쇠 결과 그래프 이미지
* `overdamped_result.png`: 과감쇠 결과 그래프 이미지
* `underdamped_result.png`: 부족감쇠 결과 그래프 이미지
---

## 🚀 설치 및 실행 방법

### 1. 저장소 클론 (Clone)
Terminal 또는 Git Bash에서 아래 명령어를 실행하여 프로젝트를 내려받습니다.
```bash
git clone [https://github.com/kimtaegyeong1231/RLC-Circuit-Simulation.git](https://github.com/kimtaegyeong1231/RLC-Circuit-Simulation.git)
cd RLC-Circuit-Simulation
