%% 1. 회로 파라미터 설정 및 초기화
clear; clc; close all;

% 소자값 및 입력 전압 (R 값을 바꿔가며 테스트 가능)
L  = 0.1;       % 인덕턴스 (H)
C  = 100e-6;    % 커패시턴스 (F)
V0 = 10;        % 입력 전압 (V)

% 임계 저항값 R_critical = 2 * sqrt(L/C) ~= 63.25 ohm
R  = 63.25;     % 저항값 (ohm)

% 주요 파라미터 계산
alpha  = R / (2 * L);           % 감쇠 계수
omega0 = 1 / sqrt(L * C);       % 고유 진동수
t      = linspace(0, 0.05, 1000);% 시간 축 (0 ~ 50ms)

%% 2. 감쇠 조건 판별 및 수식 계산
if alpha > omega0
    % 과감쇠 (Overdamped)
    state_str = '과감쇠 (Overdamped)';
    s1 = -alpha + sqrt(alpha^2 - omega0^2);
    s2 = -alpha - sqrt(alpha^2 - omega0^2);
    Vc = V0 + V0/(s1 - s2) * (s2*exp(s1*t) - s1*exp(s2*t));

elseif abs(alpha - omega0) < 1e-4
    % 임계감쇠 (Critically Damped)
    state_str = '임계감쇠 (Critically Damped)';
    Vc = V0 - V0 * (1 + alpha * t) .* exp(-alpha * t);

else
    % 부족감쇠 (Underdamped)
    state_str = '부족감쇠 (Underdamped)';
    wd = sqrt(omega0^2 - alpha^2); % 감쇠 고유 진동수
    Vc = V0 - V0 * exp(-alpha * t) .* (cos(wd * t) + (alpha / wd) * sin(wd * t));
end

%% 3. 그래프 출력
figure('Name', 'RLC Circuit Response', 'NumberTitle', 'off');

plot(t * 1000, Vc, 'b-', 'LineWidth', 2); grid on; hold on;
yline(V0, 'r--', '목표 전압 (V_0)', 'LineWidth', 1.5, 'LabelHorizontalAlignment', 'left');

xlabel('시간 (ms)');
ylabel('커패시터 전압 (V)');
title(['RLC 직렬회로 과도 응답 : ', state_str]);
ylim([0, V0 * 1.5]);
