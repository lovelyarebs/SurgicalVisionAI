# SurgicalVisionAI

https://www.notion.so/f7fd6e3597704978a7f00f32900a906e


&nbsp;
## 연구 주제

본 연구는 성형 전후 사진 데이터를 학습하여, 주어진 얼굴 사진으로부터 **성형 후 모습을 시뮬레이션하는 딥러닝 기반의 프레임워크**를 제안합니다. 이를 통해 환자와 의사 간의 원활한 소통을 지원하고, 수술 결과에 대한 기대치를 보다 현실적으로 조율하며, 데이터 기반의 의사결정을 지원하고자 합니다.


&nbsp;
## 연구 목적

- 성형수술을 고려하는 많은 환자가 공통적으로 가지는 가장 큰 우려는 “내가 수술을 했을 때 결과가 과연 만족스러울지, 혹은 수술 결과가 좋지 않으면 어떻게 해야 하나?” 입니다. 이러한 환자들의 우려를 해소하고 성형수술의 결과에 대한 신뢰를 높이기 위하여, 본 연구에서는 환자가 수술을 받았을 때 예상되는 결과를 시각적으로 예측할 수 있는 생성형 딥러닝 모델 개발을 목표로 연구를 진행하였습니다. 
- 본 연구는 성형외과 분야에 딥러닝 기술을 접목하여, **수술 전후의 결과를 시각화**하고 **환자와 의료진 모두에게 더 나은 의사결정 도구를 제공**하는 데 의의가 있습니다.


&nbsp;
## 연구 방법
- 저희는 성형 전후 이미지를 활용한 연구를 위해 기존 모델을 데이터에 맞게 커스텀하여 사용하였습니다.
생성 결과는 정량적 평가와 정성적 평가를 통해 검증하였습니다. 정량적 평가는 평가지표를 활용하여 수행하였고, 정성적 평가는 생성된 이미지를 사람이 직접 확인하는 방식으로 진행하였습니다.

- 기존 모델을 학습한 결과와 분석을 바탕으로, 모델 구조를 변형하여 보다 적합한 새로운 제안 모델을 개발하였습니다.


### 1. 데이터 준비 및 전처리
- **성형 전(before) 이미지를 입력, 성형 후(after) 이미지를 출력으로 구성된 데이터셋을 생성.**
- **데이터를 학습(train)과 테스트(test)로 분리.**
- **이미지 크기를 512x512로 리사이즈하고, 픽셀 값을 정규화([0, 1] 또는 [-1, 1]).**
- **데이터 증강(회전, 플립, 밝기 조정 등) 기법 적용.**


### 2. 모델 구성 및 학습

- **성형 전 이미지를 입력, 성형 후 이미지를 출력으로 하는 생성형 모델로 구조를 개편.**
- **학습된 모델에 테스트 데이터의 성형 전 이미지를 입력하여 성형 후 이미지를 생성.**



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



## 데이터 수집


## 모델 학습 및 선택

생성형 모델에도 다양한 유형이 많지만, 본 연구에서는 특정 사진을 입력하면, 원하는 방식대로 변형된 이미지를 생성하는 Image Interpolation 방식의 GAN, 즉 Conditional GAN을 구현하는 데 초점을 맞췄습니다. 이를 위하여 기초적인 모델부터, 현재 가장 많이 사용되고 있는 최신 모델까지 폭넓게 실험하고 학습하였습니다. 

### 1. AutoEncoder (AE)
사람의 형태는 잘 잡히지만, 변형의 정도는 크게 나타나지 않았습니다.
### 2. Variational AutoEncoder (VAE)
복원(생성) 과정에서 Latent Space로 데이터를 복원,생성하므로 //~~~~
### 3. Pix2Pix
변환의 정도는 염색이 달라지고 그림처럼 바뀌는 정도였습니다
### 4. CycleGAN
변환의 정도는 거의 달라지지 않았으며, 약간의 입술 색의 변화나 피부색의 변화를 보였습니다.
### 4. Conditional GAN
### 5. StarGAN
### 6. StarGANv2
### 7. Conditional Diffusion
### 8. Transformer Encoder, Decoder


## 모델 개량

