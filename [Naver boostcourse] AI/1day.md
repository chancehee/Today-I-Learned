## 1-1. 딥러닝 기본 용어 설명  
#### what make you a good deep learner?  
1. 구현실력  
2. 수학(선형대수학, 확률론)  
3. 연구결과(논문)  
-> 3가지 역량이 딥러닝에서 중요하다고 한다. 3가지 측면을 생각하면서 학습해야겠다.  

#### AI 관련 용어에 대한 간단한 정의  
- 인공지능: 인간의 지능 모방  
- 머신러닝: 데이터를 통한 학습  
- 딥 러닝: 뉴럴 네트워크  

#### 딥러닝의 중요한 요소 4가지와 예  
1. 데이터: classification, semantic segmentation, detection, pose estimation, visual QnA   
3. 모델: AlexNet, GoogLeNet, ResNet, DenseNet, LSTM, CAN, Deep Auto Encoders
4. 손실 함수: Regression Task, classification Task, probabilistic Task
5. 알고리즘(최적화): Dropout, Early stopping, k-fold validation, weight decay, Batch normalization, Mix up, Esemble, Bayesian Optimization  
-> 처음 들어보는 용어들이 많지만, 학습 하다 보면 익숙한 용어가 될 것이라고 생각한다.  

## 1-2. Historical Review (역사적으로 딥러닝이 큰 임팩트 있던 순간)  
- 2012: Alex Net (이미지 처리 관련, 첫 딥러닝 방법론)
- 2013: DQN (알파고 관련, 강화 학습)
- 2014: Encoder/Decoder (구글 번역기, NLP)
- 2015: GAN (술집이 들어간 논문, 생성 탐지 신경망), ResNet (딥러닝의 이유 = 많은 네트워크가 성능 저하가 아닌 경우를 보여준 논문)
- 2017: Transformer (Attention IS All You Need)
- 2018: BERT (find-tuned NLP models)
- 2019: BIG Language Models (파라미터가 많다.)
- 2020: self-supervised Learning (simCLR)  

## 1-3. 벡터  
- 벡터: 숫자를 원소로 가지는 리스트 또는 배열 (np.array는 행벡터이다.) 
- 벡터는 공간에서 한 점을 나타낸다.
- 벡터는 원점으로부터 상대적 위치를 표현한다.
- 벡터에 숫자를 곱해주면 길이만 변한다.(스칼라곱)(0보다 작을 때는 반대방향이다.)
- 벡터끼리 같은 모양을 가지면 덧셈, 뺄셈, 성분곱을 계산할 수 있다.
- 두 벡터의 덧셈은 다른 벡터로부터 상대적 위치이동을 표현한다.
- 벡터의 노름(norm)은 원점에서부터의 거리를 말한다.
- 노름은 L1, L2 두가지가 존재한다.(노름의 종류에 따라 기하학적 성질이 달라진다.)
- L1노름은 각 성분의 변화량의 절대값을 모두 더한다.
- L2노름은 피타고라서 정리를 이용해 유클리드 거리를 계산한다.
```python
def L1_norm(X):
  x_norm = np.abs(X)
  x_norm = np.sum(x_norm)
  return x_norm

def L2_norm(X):
  x_norm = X * X
  x_norm = np.sum(x_norm)
  x_norm = np.sqrt(x_norm)
  return x_norm
```  
- L1, L2 노름을 이용해 두 벡터 사이의 거리를 계산할 수 있다.
![KakaoTalk_20220627_234215497](https://user-images.githubusercontent.com/59447235/175968498-ba875c5b-1df3-4cd7-92f2-9c9c2d6d8c35.jpg)
- 두 벡터 사이의 거리를 이용하여 각도 계산 가능하다. (단, L2 노름만 가능)
![KakaoTalk_20220627_234215497_01](https://user-images.githubusercontent.com/59447235/175968637-00e812d0-5f0a-4943-8b68-59253832a4fc.jpg)
- 내적은 정사영된 벡터의 길이와 관련 있다.
![KakaoTalk_20220627_234215497_02](https://user-images.githubusercontent.com/59447235/175968732-43396825-2946-4339-8ab3-ebac7daa5165.jpg)
- 내적은 두 벡터의 유사도를 측정하는데 사용 가능하다.
