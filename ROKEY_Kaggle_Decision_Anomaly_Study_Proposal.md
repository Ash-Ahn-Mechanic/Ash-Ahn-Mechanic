# ROKEY 스터디 제안서  
## 주제: Kaggle 기반 **의사결정·이상 탐지 AI 시스템** 프로젝트 (Online Only)

---

## 1. 스터디 주제 개요

**주제**  
Kaggle에 공개된 **시계열·로그·센서형 데이터**를 활용하여,  
로봇·산업 시스템에서 실제로 중요한 **의사결정(Decision-Making) 및 이상 탐지(Anomaly Detection)** AI 파이프라인을 구축한다.

본 스터디는 **카메라·SLAM·하드웨어를 전혀 사용하지 않고**,  
온라인 환경(노트북 + Kaggle)만으로 프로젝트를 진행한다.

---

## 2. Why this Study? (ROKEY 적합성)

- ❌ 비전/SLAM/하드웨어 의존 없음  
- ✅ **로봇·산업 시스템의 두뇌 역할**에 해당하는 판단 로직 경험  
- Kaggle 데이터 → 명확한 입력/출력/평가 지표  
- 실제 로봇 시스템에서 중요한 질문을 다룸  
  - *지금 상태가 정상인가?*  
  - *언제 문제가 발생할 것인가?*  
  - *지금 어떤 행동을 선택해야 하는가?*

이 스터디는 ROKEY가 지향하는  
**"단순 모델 구현이 아닌, 시스템 관점의 AI 사고"**와 강하게 연결된다.

참고: https://www.kaggle.com

---

## 3. 진행 방식

### 협업 환경
- **GitHub (Team Repository)**  
  - 데이터 분석 코드, 모델, 실험 기록 관리
- **Slack**  
  - 실험 결과 공유, 의사결정 로직 토론
- **정기 미팅 (주 1회)**  
  - 문제 정의 점검  
  - 모델 선택 근거 설명  
  - 결과 비교 및 개선 방향 논의

모든 작업은 **온라인에서 재현 가능**해야 한다.

---

## 4. 스터디 산출물

- Kaggle 데이터 기반 **AI 판단 시스템**
- 이상 탐지 또는 예측 모델
- 결과 해석 중심 리포트 (Markdown)

> 단순 정확도 경쟁이 아니라,  
> **왜 이 판단을 했는지 설명 가능한 시스템**이 목표

---

## 5. 단계별 미니 프로젝트 예시

### 5.1 산업 센서 이상 탐지 (Anomaly Detection)

**후보 Kaggle 데이터셋**
- *NASA Turbofan Engine Degradation*  
  https://www.kaggle.com/datasets/behrad3d/nasa-cmaps

**내용**  
엔진 센서 시계열 데이터를 이용해  
"정상 → 열화 → 고장 임박" 상태를 조기에 탐지한다.

**학습 포인트**
- 시계열 데이터 이해
- 정상/이상 기준 정의
- False Alarm vs Missed Detection 트레이드오프

---

### 5.2 로봇 시스템 상태 분류 (System Health Monitoring)

**후보 Kaggle 데이터셋**
- *Predictive Maintenance Dataset*  
  https://www.kaggle.com/datasets/shivamb/machine-predictive-maintenance-classification

**내용**  
시스템 로그 및 센서 정보를 기반으로  
장비 상태를 "정상 / 주의 / 위험"으로 분류한다.

**학습 포인트**
- Feature Engineering
- 불균형 데이터 처리
- 판단 결과의 실무적 의미 해석

---

### 5.3 의사결정 로직 설계 (Rule + ML Hybrid)

**내용**  
모델 출력 확률과 규칙 기반 로직을 결합하여  
"정지 / 유지 / 점검 요청" 같은 행동 결정을 생성한다.

**출력 예**
```
System State: Caution
Confidence : 0.72
Decision  : Request Inspection
Reason    : Vibration ↑, Temperature Trend ↑
```

**학습 포인트**
- AI 결과를 행동으로 바꾸는 과정
- 설명 가능한 판단 구조

---

### 5.4 통합 판단 시스템 미니 프로젝트

**내용**  
- 입력: 센서/로그 데이터  
- 처리: 이상 탐지 + 상태 분류  
- 출력: 시스템 행동 결정

**특징**
- 전 과정 온라인 실행 가능
- 로봇·산업·제조 도메인 공통 적용 가능

---

## 6. 참고 자료

- Kaggle 공식 플랫폼  
  https://www.kaggle.com

- Kaggle Learn (시계열·머신러닝)  
  https://www.kaggle.com/learn

- Predictive Maintenance 개념 정리  
  https://www.kaggle.com/datasets

---

## 7. 기대 효과

- 비전/SLAM과 **완전히 다른 축의 ROKEY 프로젝트**
- "AI가 언제, 왜 결정을 내려야 하는가"에 대한 사고력 강화
- 온라인 환경만으로 **캡스톤급 결과물** 확보
- 로봇·AI 직무에서 차별화 가능한 프로젝트 주제

---

## 8. 이 스터디를 한 줄로 요약하면

> **"카메라 없이, 온라인으로, 로봇의 두뇌를 만든다"**
