# DCGAN for classification tutorial

## 개요

---

- GAN 이란?
    - Generative Adversarial Networks
    - 두 개의 모델이 존재하며, 하나의 모델은 가짜를 생성하고 다른 모델은 진짜 중에서 생성된 가짜를 구별하며 학습하는 신경망
- DCGAN 이란?
    - Deep Convolution Generative Adversarial Networks
    - 즉, Convolution layer를 여러개(Deep)하게 쌓아 GAN을 구성

## GAN

---

- 두 개의 모델이 존재
- 하나는 생성자(Generator)이며, 다른 하나는 판별자(Discriminator)
- 생성자는 실제 데이터의 분포를 학습하여 실제와 유사한 가짜 데이터를 생성
- 판별자는 실제 데이터와 생성자가 만들어낸 가짜 데이터를 구별할 수 있도록 학습

![https://user-images.githubusercontent.com/37301677/84800902-6dcd0a80-b039-11ea-8754-5e6bc53698b6.png](https://user-images.githubusercontent.com/37301677/84800902-6dcd0a80-b039-11ea-8754-5e6bc53698b6.png)

## DCGAN

---

### 1. 시스템 구조

![https://pytorch.org/tutorials/_images/dcgan_generator.png](https://pytorch.org/tutorials/_images/dcgan_generator.png)

- 위 그림은 생성자에 대한 모델을 나타냄
- 입력으로 z라는 잠재 벡터를 받음. (num_z, 1, 1) 크기를 갖고 있음
- deconvolution을 반복하여 실제 이미지 크기인 (channel, height, width) 크기의 데이터를 생성
- deconvolution은 convolution과 반대로 하나의 픽셀을 보고 커널 사이즈 만큼 이미지 사이즈를 확장함
- 생성된 가짜 이미지는 분류기에 입력으로 사용됨
- 분류기는 생성자와 반대로 이미지를 convolution하여 positive, negative로 분류함
- 생성자는 분류기가 생성된 가짜 이미지를 positive라고 판단할수록 작은 loss를 가지며 학습함
- 분류기는 진짜 이미지를 positive로, 생성된 이미지를 negative로 판단할수록 작은 loss를 가지며 학습함
- 결과적으로, 생성자는 점점 진짜와 같은 이미지를 생성하고, 분류기는 진짜와 구별하기 어려운 생성자의 이미지도 진짜와 구별할 수 있게 됨

### 2. 사람 얼굴 분류

![https://pytorch.org/tutorials/_images/sphx_glr_dcgan_faces_tutorial_001.png](https://pytorch.org/tutorials/_images/sphx_glr_dcgan_faces_tutorial_001.png)

- [Celeb-A Faces dataset](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)을 사용함 (img_align_celeba.zip)
- 위 예시들과 같이 유명인들의 얼굴들로 구성되어 있음
- DCGAN을 사용해 생성된 사람 얼굴 이미지 예시

![https://pytorch.org/tutorials/_images/sphx_glr_dcgan_faces_tutorial_003.png](https://pytorch.org/tutorials/_images/sphx_glr_dcgan_faces_tutorial_003.png)

---

출처

- [https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html](https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html)
- [https://ysbsb.github.io/gan/2020/06/17/GAN-newbie-guide.html](https://ysbsb.github.io/gan/2020/06/17/GAN-newbie-guide.html)