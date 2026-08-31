# CAN Classification

Driving CAN 데이터를 이용한 시계열 분류 프로젝트입니다. 슬라이딩 윈도우 방식으로 CAN 신호를 나누고, 1D CNN 기반 인코더와 MLP 분류기를 사용해 주행 클래스를 예측합니다.

- Time Series Classification
  - Self-Supervised Learning
  - Semi-Supervised Learning
  - Foundation Encoder / Prompt Active Learning

## 주요 내용

- `data/driving.csv`: CAN 주행 데이터
- `data_loader.py`: supervised / semi-supervised 데이터 분할 및 슬라이딩 윈도우 생성
- `model.py`: 1D CNN 인코더와 MLP 기반 시계열 분류 모델
- `run_supervised.py`: 지도학습 실행 스크립트
- `run_semisupervised.py`: pseudo label 기반 준지도학습 실행 스크립트
- `representation.py`: 학습된 표현을 t-SNE 또는 UMAP으로 시각화
- `prompt_active_learning.py`: frozen foundation encoder, prompt tuning, active learning 예제

## 설치

```bash
pip install torch numpy pandas scikit-learn matplotlib umap-learn
```

## 실행 전 준비

결과 저장을 위해 아래 폴더를 생성합니다.

```bash
mkdir -p checkpoints logs visualization
```

## 실행

지도학습:

```bash
python run_supervised.py
```

준지도학습:

```bash
python run_semisupervised.py
```

표현 시각화:

```bash
python representation.py --method tsne
python representation.py --method umap
```

Prompt Active Learning 예제:

```bash
python prompt_active_learning.py
```

## 참고

- 기본 입력 데이터 경로는 `./data/driving.csv`입니다.
- 기본 분류 클래스 수는 10개로 설정되어 있습니다.
- `run_supervised.py` 실행 후 best model이 `checkpoints/best_model.pth`에 저장됩니다.


## 사사
본 연구는 과학기술정보통신부 및 정보통신기획평가원의 자율주행기술개발혁신사업의 지원을 받아 수행된 연구임 (RS-2023-00232046, 비정상 주행 데이터 전송을 통한 클라우드 기반 원인 분석 기술 개발).

This work was partly supported by Institute of Information & communications Technology Planning & Evaluation (IITP) grant funded by the Korea government(MSIT) (No.2023-00232046, Development of cloud-based cause analysis technology by transmission of abnormal driving data)
