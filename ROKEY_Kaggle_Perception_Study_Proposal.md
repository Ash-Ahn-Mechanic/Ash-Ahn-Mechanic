# ROKEY 스터디 제안서  
## 주제: Kaggle 기반 자율주행 인지(Perception) 파이프라인 프로젝트

---

## 1. 스터디 주제 개요

**주제**  
Kaggle에 공개된 자율주행·도로 환경 데이터셋을 활용하여,  
**자율주행 인지(Perception) 파이프라인**을 단계적으로 구현한다.

본 스터디는 대규모 하드웨어나 실제 차량 없이도,  
ROKEY 취지에 맞는 **AI·로봇 소프트웨어 사고력과 프로젝트 경험**을 쌓는 것을 목표로 한다.

---

## 2. Why this Study? (ROKEY 적합성)

- Kaggle 데이터는 **표준화된 입력과 명확한 평가 지표** 제공
- 실제 산업·연구에서 사용하는 **Perception 문제 유형** 경험 가능
- 시뮬레이션·비전 중심 → 하드웨어 의존 최소화
- 결과가 **정량 지표(Accuracy, mAP 등)** 로 남아 성장 확인 가능

본 스터디는 Kaggle의 *문제 정의 → 데이터 → 평가* 구조를 따라가며,  
ROKEY가 지향하는 **실무형 AI/로봇 개발 역량**과 직접적으로 연결된다.

참고: https://www.kaggle.com

---

## 3. 진행 방식

### 협업 환경
- **GitHub (Team Repository)**  
  - 데이터 전처리 코드, 모델 코드, 실험 기록 관리
- **Slack**  
  - 실험 결과 공유 및 자유 토론
- **정기 미팅 (주 1회)**  
  - 주차별 목표 공유
  - 실험 결과 비교 및 개선 방향 논의

---

## 4. 스터디 산출물

- Kaggle 데이터셋 기반 **인지 모델 또는 알고리즘**
- 데이터 분석·전처리·학습 과정 문서
- 실험 결과 정리 리포트 (Markdown)

모든 산출물은 **재현 가능성**을 기준으로 관리한다.

---

## 5. 단계별 미니 프로젝트 예시

### 5.1 도로 환경 이미지 이해 (Image Understanding)

**후보 Kaggle 데이터셋**
- *Road Damage Detection Dataset*  
  https://www.kaggle.com/c/road-damage-detection-2020

**내용**  
도로 이미지에서 균열, 포트홀 등의 객체를 인식하여  
자율주행 시스템이 위험 구간을 판단할 수 있도록 한다.

**학습 포인트**
- 이미지 데이터 구조 이해
- 객체 탐지 문제 정의
- 성능 지표(mAP) 해석

---

### 5.2 차선 인식 및 주행 가능 영역 분할 (Segmentation)

**후보 Kaggle 데이터셋**
- *TuSimple Lane Detection* (Kaggle mirror 기반)  
  https://www.kaggle.com/datasets

**내용**  
도로 영상에서 차선을 분할하여 주행 가능 영역을 추정한다.

**학습 포인트**
- Semantic Segmentation 개념
- 인지 결과를 주행 판단에 연결하는 사고

---

### 5.3 자율주행 상황 분류 (Scene Classification)

**후보 Kaggle 데이터셋**
- *Traffic Sign Recognition*  
  https://www.kaggle.com/c/gtsrb-german-traffic-sign

**내용**  
교통 표지판 이미지를 분류하여 차량의 행동 판단에 활용한다.

**학습 포인트**
- 분류 문제 설계
- 오인식이 미치는 영향 분석

---

### 5.4 통합 인지 파이프라인 미니 프로젝트

**내용**  
차선 인식 + 객체 인식 결과를 종합하여  
"주행 가능 / 주의 / 위험" 상태를 판단하는 간단한 로직을 구현한다.

**출력 예**
- 상태(State): Safe / Caution / Danger
- 근거 정보: 인식된 객체, 신뢰도

---

## 6. 참고 자료

- Kaggle 공식 플랫폼  
  https://www.kaggle.com

- Kaggle Learn (입문·실습 코스)  
  https://www.kaggle.com/learn

- 자율주행 인지 관련 공개 데이터 개요  
  https://www.kaggle.com/datasets

---

## 7. 기대 효과

- Kaggle 기반 실험 경험 → **정량적 성과 제시 가능**
- 자율주행 인지 문제에 대한 **구조적 이해**
- 캡스톤·공모전·ROKEY 이후 프로젝트로 확장 가능
- AI/로봇 분야 진로 설명에 활용 가능한 **대표 프로젝트 확보**
