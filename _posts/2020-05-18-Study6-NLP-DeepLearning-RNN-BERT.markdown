---
layout: post
title:  "[Study6] NLP(Natural Language Processing) - RNN/LSTM에서 BERT까지"
date:   2020-05-18 16:15:00 +0900
categories: AI&QA AI&NLP
---

*[AI와 QA의 만남] - Study Day6 (학습일: '20.06.10, update: '20.06.08)*

## 딥러닝을 이용한 자연어처리(업데이트중...)

### NLP Model 역사

![NLP Model](/img/study6/NLP_Model_history.png)

### RNN & LSTM

- RNN 기본 모델

  ![vanilla RNN](/img/study6/vanilla_RNN.png)

- RNN Examples

  ![RNN Examples](/img/study6/RNN_examples.png)

  - one to one : 이미지 입력 -> 이미지 분류 (개/고양이 사진 분류)
  - one to many : 이미지 입력 -> 이미지 Captioning (문장 생성)
  - many to one : 문장 입력 -> 감정분석 결과 (긍정/부정)
  - many to many : 문장 입력 -> 문장 출력 (기계번역)
  - many to many :  비디오 입력 -> (동기화된) 결과 출력 (비디오 프레임별 분류)

- LSTM

  ![LSTM](/img/study6/LSTM.png)

- RNN & LSTM 참고자료

  - [RNN 언어 모델(Recurrent Neural Network Language Model, wikidocs](https://wikidocs.net/46496)
  - [RNN을 이용한 텍스트 생성(Text Generation using RNN), wikidocs](https://wikidocs.net/45101)

  - [순환 신경망(RNN, Recurrent Neural Network), Excelsior-JH's Blog](https://excelsior-cjh.tistory.com/183)
  - [[러닝 텐서플로]Chap05 - 텍스트 1: 텍스트와 시퀀스 처리 및 텐서보드 시각화, Excelsior-JH's Blog](https://excelsior-cjh.tistory.com/154?category=940399)

  - [RNN과 LSTM을 이해해보자!, ratsgo's Blog](https://ratsgo.github.io/natural%20language%20processing/2017/03/09/rnnlstm/)

  - [Tensorflow 튜토리얼 - RNN을 사용한 텍스트 분류](https://www.tensorflow.org/tutorials/text/text_classification_rnn?hl=ko)
  - [Tensorflow 튜토리얼 - RNN을 사용한 텍스트 생성](https://www.tensorflow.org/tutorials/text/text_generation?hl=ko)

- RNN/LSTM keras 샘플 코드 : [Github Repository](https://github.com/sungalex/aiqa.git)의 "RNN_LSTM_example.ipynb" 파일

### BERT & KoBERT

- BERT(Bidirectional Encoder Representations form Transformer)는 기본적으로 wiki나 book data와 같은 대용랑 unlabeled data로 모델을 미리 학습 시킨 후, 특정 task를 가지고 있는 labeled data로 transfer learning을 하는 모델입니다.

- BERT는 transformer 중에서도 encoder 부분만을 사용합니다.

- BERT는 모델의 크기에 따라 base 모델과 large 모델을 제공합니다.
  - BERT_base : L=12, H=768, A=12, Total Parameters = 110M
  - BERT_large : L=24, H=1024, A=16, Total Parameters = 340M
    - L : transformer block의 layer 수, H : hidden size, A : self-attention heads 수, feed-forward/filter size = 4H

- BERT Structure

  ![BERT Structure](/img/study6/BERT_Structure.png)

- [BERT Github](https://github.com/google-research/bert)

  - BERT 모델은 GPU가 없는 경우, 샘플 코드를 실행하는데 시간이 너무 많이 소요됨

- [KoBERT](https://github.com/SKTBrain/KoBERT)

\[참조1\] [BERT 논문정리, mino-park7's Blog](https://mino-park7.github.io/nlp/2018/12/12/bert-논문정리/)

\[참조2\] Fastcampus On-line 강의("[올인원패키지: 머신러닝과 데이터분석 A-Z](https://www.fastcampus.co.kr/data_online_dataadv/)" - 김용담 강사 강의자료)
