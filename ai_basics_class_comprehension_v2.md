# AI 학습 전 체크리스트: 클래스 & 컴프리헨션 정리

파이썬으로 머신러닝/딥러닝을 제대로 하려면, “코드를 짜는 속도”보다 **구조화(클래스)**와 **데이터 다루기(컴프리헨션)**가 먼저 잡혀야 합니다. 아래는 시험/실무/프로젝트에서 자주 쓰는 핵심만 모은 요약입니다.

## 목차
- [1) 클래스: 왜 필요한가](#class)
- [2) 클래스 핵심 문법/패턴](#class-core)
- [3) AI에서 클래스가 쓰이는 위치(현실 예시)](#class-ai)
- [4) 컴프리헨션: 한 줄 요약 & 타입별 예시](#comp)
- [5) 컴프리헨션 팁/함정](#comp-tips)
- [6) AI에서 컴프리헨션을 사용하는 이유](#comp-why)

---

## 1) 클래스: 왜 필요한가 <a id="class"></a>

AI 프로젝트는 보통 “데이터 → 전처리 → 모델 → 학습 → 평가 → 저장/로드” 흐름입니다. 이걸 함수만으로 쌓으면 **상태(state)**가 흩어져서 유지보수가 어렵고, 재사용도 힘듭니다. 클래스는 아래를 해결합니다.

- **상태를 묶기**: 모델 파라미터, 하이퍼파라미터, 학습 로그 등을 한 객체에 저장  
- **기능을 묶기**: `fit()`, `predict()`, `save()` 같은 인터페이스 통일  
- **확장하기**: 상속/구성으로 실험을 빠르게 늘림 (예: 여러 모델을 같은 평가 코드로 돌림)

> ✅ **팁**  
> “클래스 = 복잡하게 만들기”가 아니라, **실험을 복사/붙여넣기 없이 반복하기 위한 장치**라고 보면 됩니다.

---

## 2) 클래스 핵심 문법/패턴 <a id="class-core"></a>

### 2-1. 기본 구조: __init__ (초기화) + 메서드

```python
class SimpleScaler:
    def __init__(self, mean: float, std: float):
        self.mean = mean
        self.std = std

    def transform(self, x: float) -> float:
        return (x - self.mean) / (self.std + 1e-12)
```

> ⚠️ **주의**  
> 메서드 첫 인자 `self`를 빼먹거나, 인스턴스 변수에 `self.`를 안 붙여서 “로컬 변수”로 끝나는 경우가 많습니다.

### 2-2. __repr__ / __str__ : 디버깅 생산성

```python
class Config:
    def __init__(self, lr=1e-3, batch_size=32):
        self.lr = lr
        self.batch_size = batch_size

    def __repr__(self):
        return f"Config(lr={self.lr}, batch_size={self.batch_size})"
```

### 2-3. @dataclass : 설정/데이터 담는 클래스에 강력

```python
from dataclasses import dataclass

@dataclass
class TrainConfig:
    lr: float = 1e-3
    batch_size: int = 32
    epochs: int = 10
```

### 2-4. 상속 vs 구성(Composition)

- **상속(is-a)**: 구조가 딱 맞을 때만  
- **구성(has-a)**: 부품을 끼워서 조합(실무에서 더 안전한 경우 많음)

```python
class BaseModel:
    def predict(self, x):
        raise NotImplementedError

class LinearModel(BaseModel):
    def __init__(self, w, b):
        self.w, self.b = w, b

    def predict(self, x):
        return self.w * x + self.b
```

```python
class Pipeline:
    def __init__(self, scaler, model):
        self.scaler = scaler
        self.model = model

    def predict(self, x):
        x2 = self.scaler.transform(x)
        return self.model.predict(x2)
```

### 2-5. __call__ : 객체를 함수처럼 호출

```python
class Threshold:
    def __init__(self, t=0.5):
        self.t = t

    def __call__(self, p: float) -> int:
        return 1 if p >= self.t else 0

th = Threshold(0.7)
print(th(0.65))  # 0
print(th(0.72))  # 1
```

---

## 3) AI에서 클래스가 쓰이는 위치(현실 예시) <a id="class-ai"></a>

### 3-1. 데이터셋/로더 개념(프레임워크 공통)

```python
class TinyDataset:
    def __init__(self, xs, ys):
        self.xs = xs
        self.ys = ys

    def __len__(self):
        return len(self.xs)

    def __getitem__(self, idx):
        return self.xs[idx], self.ys[idx]
```

### 3-2. 모델 클래스: 파라미터/추론/저장을 묶기

```python
import json

class SimpleLinear:
    def __init__(self, w=0.0, b=0.0):
        self.w = w
        self.b = b

    def predict(self, x):
        return self.w * x + self.b

    def save(self, path="model.json"):
        with open(path, "w", encoding="utf-8") as f:
            json.dump({"w": self.w, "b": self.b}, f, ensure_ascii=False, indent=2)

    @classmethod
    def load(cls, path="model.json"):
        with open(path, "r", encoding="utf-8") as f:
            d = json.load(f)
        return cls(**d)
```

### 3-3. 훈련 루프도 클래스로 두면 실험이 빨라짐

```python
class Trainer:
    def __init__(self, model, lr=1e-2):
        self.model = model
        self.lr = lr

    def fit_one_step(self, x, y):
        pred = self.model.predict(x)
        grad_w = 2 * (pred - y) * x
        grad_b = 2 * (pred - y)
        self.model.w -= self.lr * grad_w
        self.model.b -= self.lr * grad_b
```

---

## 4) 컴프리헨션: 한 줄 요약 & 타입별 예시 <a id="comp"></a>

**한 줄 요약**: “반복 + 조건 + 변환”을 짧게 쓰는 문법. 데이터 전처리에서 정말 자주 씁니다.

### 4-1. List Comprehension

```python
squares = [x*x for x in range(1, 6)]
evens = [x for x in range(10) if x % 2 == 0]

raw = ["  Hello", "", "  AI  ", "python "]
clean = [s.strip().lower() for s in raw if s.strip() != ""]
```

### 4-2. Dict Comprehension

```python
names = ["cat", "dog", "penguin"]
length_map = {n: len(n) for n in names}

labels = ["normal", "fault", "normal", "warning"]
label_to_id = {lab: i for i, lab in enumerate(sorted(set(labels)))}
```

### 4-3. Set Comprehension

```python
nums = [1, 1, 2, 3, 3, 3, 4]
unique_squares = {n*n for n in nums}
```

### 4-4. Generator Expression (메모리 절약)

```python
gen = (x*x for x in range(1_000_000))
total = sum(x*x for x in range(1000))
```

---

## 5) 컴프리헨션 팁/함정 <a id="comp-tips"></a>

> ⚠️ **규칙 하나만 기억**  
> 한 줄로 “명확하게” 끝나면 컴프리헨션, 아니면 for문이 이깁니다. (가독성이 곧 디버깅 속도)

### 5-1. 중첩 컴프리헨션(2중 for) - Flatten

```python
mat = [[1,2,3],[4,5,6]]
flat = [v for row in mat for v in row]
```

### 5-2. if-else는 위치 주의

```python
x = [1,2,3,4,5]
y = ["big" if n >= 3 else "small" for n in x]
```

### 5-3. 전처리에서 자주 쓰는 패턴

```python
# None 제거
vals = [1.0, None, 2.5, None, 3.1]
vals2 = [v for v in vals if v is not None]

# (x,y) 쌍 만들기
xs = [10, 20, 30]
ys = [0, 1, 0]
pairs = [(x, y) for x, y in zip(xs, ys)]
```

> ✅ **팁**  
> 컴프리헨션을 쓰기 전 “이걸 누가 내일 봐도 이해할까?”만 체크하면 실수가 줄어듭니다.

---

## 6) AI에서 컴프리헨션을 사용하는 이유 <a id="comp-why"></a>

### 6-1. 전처리(정제/필터링/변환)가 대부분 “반복 + 조건 + 변환” 패턴

```python
clean = [s.strip().lower() for s in raw_texts if s and s.strip()]
```

### 6-2. 라벨 인코딩/매핑 딕셔너리를 빠르게 만든다

```python
label_to_id = {lab: i for i, lab in enumerate(sorted(set(labels)))}
id_to_label = {i: lab for lab, i in label_to_id.items()}
```

### 6-3. (x, y) 형태로 묶거나 feature를 구성하기 쉽다

```python
pairs = [(x, y) for x, y in zip(xs, ys)]
```

### 6-4. Generator 표현식으로 큰 데이터에서 메모리를 아낀다

```python
total = sum(v for v in big_stream)
```

### 6-5. 데이터 증강/샘플링/서브셋 생성이 빠르다

```python
subset = [ex for ex in dataset if ex["label"] != "unknown"][:10000]
```

### 6-6. 파이프라인(입력→변환→출력) 사고방식에 잘 맞는다

```python
features = [[float(v) for v in row.split(",")] for row in lines if row.strip()]
```

> ⚠️ **AI에서 특히 조심할 점 (현업에서 많이 터짐)**  
> - **너무 길어지면 즉시 for문으로**: 전처리가 2단계 넘어가면 가독성 때문에 사고 납니다.  
> - **중첩 컴프리헨션은 순서 실수 잦음**: flatten 같은 확실한 패턴 아니면 for문 추천.  
> - **큰 데이터에서 list/dict를 한 번에 만들면 메모리 폭탄**: generator/iterator 또는 chunk 처리.

---

작성일: 2026-01-11 (Asia/Seoul)  
용도: AI/ML 학습 전 기초 문법 정리 (클래스/컴프리헨션)
