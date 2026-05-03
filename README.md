#  CNN vs ResNet (CIFAR-10 Image Classification)

## 프로젝트 개요
본 프로젝트는 CIFAR-10 데이터셋을 기반으로  
기본 CNN과 ResNet 모델을 구현하고 성능을 비교하는 것을 목표로 한다.  

특히 CNN의 구조적 한계(깊어질수록 성능 저하)를 분석하고,  
ResNet이 이를 어떻게 해결하는지 실험적으로 검증하였다. 
---

## ResNet 핵심 개념

### Residual Learning
기존 CNN:
H(x)

ResNet:
H(x) = F(x) + x

- 입력 x를 그대로 더하는 skip connection 사용
- 복잡한 함수 대신 residual F(x) 학습
- gradient 흐름 개선 (gradient highway) :contentReference[oaicite:1]{index=1}

---

## ResNet 구조

###  Residual Block
- Conv → BN → ReLU → Conv → BN → + input

###  Skip Connection
- 입력을 출력에 직접 더함

###  Projection Shortcut
- 차원 불일치 해결을 위해 1x1 convolution 사용 :contentReference[oaicite:2]{index=2}

---

##  모델 개선 (본 프로젝트 적용)

### 1. 채널 확장
- 기존: 16 channel 고정
- 개선: 32 → 64 → 128

 더 다양한 feature 표현 가능 :contentReference[oaicite:3]{index=3}

---

### 2. Downsampling 적용
- stride=2 사용
- 공간 크기 감소 → 추상적 특징 학습

---

### 3. Projection Shortcut
- 채널 및 feature map 크기 mismatch 해결
- 1×1 convolution 사용 :contentReference[oaicite:4]{index=4}

---

### 4. Batch Normalization + ReLU
- Conv → BN → ReLU 구조 유지
- 학습 안정성 향상
- gradient 흐름 개선 :contentReference[oaicite:5]{index=5}

---

### 5. 데이터 증강 및 학습 튜닝
- RandomHorizontalFlip 적용
- Dropout (0.3에서 최고 성능)
- 학습률 0.01 → 0.001 조정 :contentReference[oaicite:6]{index=6}

---

## 실험 결과

| 모델 | 정확도 |
|------|--------|
| CNN (기본) | 약 60% |
| CNN (튜닝) | 약 84% |
| ResNet (개선 전) | 69.7% |
| ResNet (개선 후) | **84.64%** |

 ResNet 구조 개선 후 성능 크게 향상 :contentReference[oaicite:7]{index=7}

---

## 결론

- CNN은 깊어질수록 성능 저하 및 학습 불안정 발생
- ResNet은 skip connection을 통해 gradient 문제 해결
- 깊은 네트워크에서도 안정적인 학습 가능
- 구조적 개선을 통해 CNN보다 높은 성능 달성 :contentReference[oaicite:8]{index=8}

---

##  핵심 요약

ResNet = "깊은 네트워크에서도 학습이 가능하게 만든 구조" (residual 중요)

---

##  참고
- He et al., Deep Residual Learning for Image Recognition (2016)
