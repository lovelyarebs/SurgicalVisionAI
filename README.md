# SurgicalVisionAI

https://www.notion.so/f7fd6e3597704978a7f00f32900a906e


&nbsp;
## 연구 주제

본 연구는 **성형 전후 사진 데이터**를 학습하여, 주어진 얼굴 사진으로부터 성형 후 모습을 시뮬레이션하는 딥러닝 기반의 프레임워크를 제안합니다. 이를 통해 환자와 의사 간의 원활한 소통을 지원하고, 수술 결과에 대한 기대치를 보다 현실적으로 조율하며, 데이터 기반의 의사결정을 지원하고자 합니다.
&nbsp;
## 연구 목적

성형수술을 고려하는 많은 환자가 공통적으로 가지는 가장 큰 우려는 “내가 수술을 했을 때 결과가 과연 만족스러울지, 혹은 수술 결과가 좋지 않으면 어떻게 해야 하나?” 입니다. 이러한 환자들의 우려를 해소하고, 성형수술의 결과에 대한 신뢰를 높이기 위하여, 본 연구에서는 환자가 수술을 받았을 때 예상되는 결과를 시각적으로 예측할 수 있는 생성형 딥러닝 모델 개발을 목표로 연구를 진행하였습니다.본 연구는 성형외과 분야에 딥러닝 기술을 접목하여, 수술 전후의 결과를 시각화하고, 환자와 의료진 모두에게 더 나은 의사결정 도구를 제공하는 데 의의가 있다고 생각합니다. 

&nbsp;
## 연구 방법
저희는 성형 전후 이미지를 활용한 연구를 위해 기존 모델 구조를 데이터에 맞게 커스텀하였습니다.
정량적 평가와 함께 사람이 직접 생성 결과를 눈으로 확인하는 정성적 평가도 수행하였습니다. 결과는 시각화하여 모델의 생성 품질을 직관적으로 파악하고, 모델 개선 방향성을 분석하는 데 활용했습니다. 
기존의 모델들을 학습시켜 출력된 이미지와 평가지표를 분석한 뒤, 이를 바탕으로 모델을 변형하여 새로운 제안 모델을 개발하였습니다.

### 1. 데이터 준비 및 전처리
성형 전(before) 이미지를 입력, 성형 후(after) 이미지를 출력으로 구성된 데이터셋을 생성.
데이터를 학습(train)과 테스트(test)로 분리.
이미지 크기를 512x512로 리사이즈하고, 픽셀 값을 정규화([0, 1] 또는 [-1, 1]).
데이터 증강(회전, 플립, 밝기 조정 등) 기법 적용.

### 2. 모델 구성 및 학습

성형 전 이미지를 입력, 성형 후 이미지를 출력으로 하는 생성형 모델로 구조를 개편.
학습된 모델에 테스트 데이터의 성형 전 이미지를 입력하여 성형 후 이미지를 생성.


### 3. 사용한 평가지표

![image](https://github.com/user-attachments/assets/1a020a83-83f7-4e55-9306-2aea90e30432)
FID (Fréchet Inception Distance): 생성된 이미지와 실제 이미지의 유사성을 평가
![image](https://github.com/user-attachments/assets/8a8431c8-0a7c-4111-9f81-ca0a42a7e8ae)
SSIM (Structural Similarity Index): 이미지의 구조적 유사성을 평가.
![image](https://github.com/user-attachments/assets/4b1f64ed-d364-46d8-b4be-31da3c9c5e40)
PSNR (Peak Signal-to-Noise Ratio): 이미지의 신호 대 잡음 비율을 평가.
![image](https://github.com/user-attachments/assets/74db5916-1b7e-4d17-a3bc-c8733431dae1)
IS (Inception Score): 생성된 이미지의 다양성과 품질을 평가.
![image](https://github.com/user-attachments/assets/3f51626a-bafe-4949-9e0e-49e6e02d95c3)
LPIPS (Learned Perceptual Image Patch Similarity): 이미지 간의 지각적 유사성을 평가.



## 모델 선택
### 1. AutoEncoder (AE)
### 2. Variational AutoEncoder (VAE)
### 3. Conditional GAN
### 4. StarGAN
### 5. StarGANv2
### 6. Conditional Diffusion
### 7. Transformer Encoder, Decoder



