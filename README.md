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

- ![image](https://github.com/user-attachments/assets/1a020a83-83f7-4e55-9306-2aea90e30432)


FID (Fréchet Inception Distance): 생성된 이미지와 실제 이미지의 유사성을 평가
- ![image](https://github.com/user-attachments/assets/8a8431c8-0a7c-4111-9f81-ca0a42a7e8ae)


SSIM (Structural Similarity Index): 이미지의 구조적 유사성을 평가.
- ![image](https://github.com/user-attachments/assets/4b1f64ed-d364-46d8-b4be-31da3c9c5e40)


PSNR (Peak Signal-to-Noise Ratio): 이미지의 신호 대 잡음 비율을 평가.
- ![image](https://github.com/user-attachments/assets/74db5916-1b7e-4d17-a3bc-c8733431dae1)


IS (Inception Score): 생성된 이미지의 다양성과 품질을 평가.
- ![image](https://github.com/user-attachments/assets/3f51626a-bafe-4949-9e0e-49e6e02d95c3)


LPIPS (Learned Perceptual Image Patch Similarity): 이미지 간의 지각적 유사성을 평가.



## 데이터 수집


## 모델 학습 및 선택

생성형 모델에도 다양한 유형이 많지만, 본 연구에서는 특정 사진을 입력하면, 원하는 방식대로 변형된 이미지를 생성하는 Image Interpolation 방식의 GAN, 즉 Conditional GAN을 구현하는 데 초점을 맞췄습니다. 이를 위하여 기초적인 모델부터, 현재 가장 많이 사용되고 있는 최신 모델까지 폭넓게 실험하고 학습하였습니다. 

### 1. AutoEncoder (AE)
사람의 형태는 잘 잡히지만, 변형의 정도는 크게 나타나지 않았습니다.
### 2. Variational AutoEncoder (VAE)
복원(생성) 과정에서 Latent Space로 데이터를 복원,생성하므로 이후 모델에 많이 응용되어 사용됐습니다.
### 3. Pix2Pix
변환의 정도는 염색이 달라지고 그림처럼 바뀌는 정도였습니다
### 4. CycleGAN
변환의 정도는 거의 달라지지 않았으며, 약간의 입술 색의 변화나 피부색의 변화를 보였습니다.
### 5. StarGAN
StarGAN은 다중 도메인 간의 변환을 학습하는 모델로, 다중 도메인이라고 할수있는 눈, 코, 턱을 학습시켜야 하는 저희에게는 가장 매력적으로 느껴지는 모델이었습니다. StarGAN의 구조는 여러 도메인을 하나의 모델로 처리할 수 있다는 점에서 저희가 지향하는 방식과 부합하였고, 변형의 정도도 얼굴의 형태 변화가 많이 일어나는 것으로 보였습니다.
### 6. StarGANv2
성형 전 이미지를 입력으로 받아 성형 후의 스타일을 자연스럽게 생성했으며, 피부 톤, 윤곽 변화 등 세부적인 디테일까지 반영할 수 있었습니다. 
### 7. Stable Diffusion
입력 이미지를 잠재 공간(Latent Space)으로 변환한 후, 이를 기반으로 이미지를 복원하거나 새롭게 생성하는 딥러닝 모델입니다. 이는 고해상도의 사진 품질을 유지하면서 다양한 이미지 생성 작업을 수행할 수 있는 특징이 있습니다.
### 8. 기본 GAN 모델
SSIM, PSNR 값이 평균적으로 낮은 값으로 기록되어 품질이 좋지 않음을 알 수 있습니다. 그리고 LPIPS 값은 큰 편에 속하는데 생성된 이미지와 실제 이미지간의 지각적 차이가 큽니다. FID 값은 매우 높은 값이 나왔는데, 전체적인 이미지 품질과 생성된 데이터의 다양성이 부족함을 알 수 있습니다. 
### 9. Style Transfer
성형 후 특정 스타일을 학습해 성형 전 이미지를 해당 스타일로 변환하는 작업에 사용되었습니다. 결과의 세부적 변화가 부족했습니다.


## 모델 변형
### 1. VAE + loss
VAE에 Perceptual Loss (z_mean 기반)을 추가하여 생성 이미지의 디테일과 품질을 개선했습니다.
복잡한 데이터셋에 대한 복원 성능이 제한적이었고, 학습 도중 잠재 공간의 일부 변수가 비활성화되는 문제 (Posterior Collapse)도 발생했습니다.
### 2.CycleGAN + Attention Mechanism[Generator]
CycleGAN에 self attention을 추가하였습니다. 이 시도에서는 Generator에만 추가했습니다.
### 3.CycleGAN + Attention Mechanism[Generator & Discriminator]
CycleGAN에 self attention을 추가하였습니다. 생성자와 판별자 모두에 추가했습니다.
 Attention 메커니즘을 생성기와 판별기에 추가했습니다.
### 4.Stable Diffusion [Training with LoRA]
Stable Diffusion 모델에 LoRA (Low-Rank Adaptation)를 적용해 수술 전-후 이미지 변환을 훈련하고 결과를 생성하였습니다. Stable Diffusion의 UNet 계층에 LoRA를 추가해 가중치 일부만 학습했고, r=4(랭크), alpha=32(스케일링) 설정을 했습니다. before 이미지를 입력으로 받아, after 이미지와 비슷한 결과를 생성했고 생성 이미지와 실제 after 이미지 간 손실(MSE)을 계산해 모델을 업데이트합니다. LoRA로 특정 가중치만 학습하여 자원을 절약해서 몹시 효율적입니다. 사용한 프롬프트는 다음과 같습니다.
A professional portrait of a person after surgery
이를 이용해서 특정 부위의 성형을 한 것을 잘 표현할 수 있다고 생각했습니다. 하지만 일단 저희의 데이터셋에 따라 전체적인 얼굴로만 프롬프트를 설정하고 모델을 훈련했습니다.
그러나 프롬프트 (A professional portrait of a person after surgery)의 영향을 너무 심하게 받는 경향이 있어 폐기했습니다.

### 5.StarGAN + Self-Attention [Generator]
StarGAN의 Generator에 Self-Attention을 추가하여 Generator의 성능을 강화하고자 하였고, 기존 CNN 방식만 사용한 모델과 다르게 Attention을 추가함으로써 지엽적 부분뿐만 아니라, 문맥적 부분도 학습할 수 있을 것이라는 가정을 하고 만든 모델입니다. 그 결과는 그렇게 좋지 못하였고, 특정 부분에 강하게 집중하는 모습을 보이는 듯하지만, 사람의 얼굴을 정확하게 표현하지 못하는 모습을 보였습니다.
### 6.StarGAN + Multi-Head Attention [Generator]
이전 모델에서 Self-Attention 모듈의 개수를 늘려 Multi-Head Attention 구조를 적용하였습니다. 이를 통해, Generator가 더 다양한 패턴에 주의를 기울이고 이미지 전반에 걸쳐 풍부한 표현력을 학습할 수 있을 것이라는 가정을 바탕으로 실험을 진행하였습니다. 그러나 결과는 기대에 미치지 못하였고, 너무 많은 변형을 일으키는 것을 확인하였습니다.
### 7.StarGAN + Self-Attention [Generator] (Loss Ratio Adjustment)
이미지 변형에 제한을 걸기 위하여 Reconstruction Loss의 비율을 대폭 
   상승시켰습니다. 그렇지만, 좋지 못한 결과를 불러왔습니다.
### 8.StarGAN + Multi-Head Attention [Generator] (Loss Ratio djustment)
이미지 변형에 제한을 걸기 위하여 Reconstruction Loss의 비율을 대폭 
  상승시켰습니다. 그렇지만, 좋지 못한 결과를 불러왔습니다.
### 9.StarGAN + Self-Attention [Generator & Discriminator] (Loss Ratio Adjustment)
