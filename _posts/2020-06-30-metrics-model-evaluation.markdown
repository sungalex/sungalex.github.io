---
layout: post
title:  "[Stydy10] 모델 성능 평가지표와 측정"
date:   2020-06-30 02:15:00
categories: Python AI AI&QA
---

*(create: '20.6.30, update: '20.8.12)*

*reference:*
  - *<https://scikit-learn.org/stable/modules/classes.html?highlight=metrics#module-sklearn.metrics>*
  - *<https://datascienceschool.net/view-notebook/731e0d2ef52c41c686ba53dcaf346f32/>*

## 모델 평가와 성능 향상

(source: <https://github.com/sungalex/aiqa/blob/master/model-evaluation-and-improvement.ipynb>)

  - Train/Validation/Test Data

    ![validataion_set](/img/validation_dataset.png)

  - 교차 검증(Cross Validation)

    ![cross-validation](/img/cross-validation.png)

  - K-겹 교차 검증(K-Fold Cross Validation)

    ![k-fold](/img/k-fold-cross-validation.png)

  - 평가 지표 및 측정

>> **최종 목표를 기억하라** : 학습되지 않은 새로운 데이터에서의 예측 성능을 높이는 것이 중요하다.

  - 오차 행렬(Confusion matrics)

    ![confusion_matrix](/img/confusion_matrix.png)

    - TN : True Negative (실제 Negative를 Negative로 정확히 예측한 데이터)
    - FN : False Negative (실제 Positive를 Negative로 잘못 예측한 데이터)
    - FP : False Positive (실제 Negative를 Positive로 잘못 예측한 데이터)
    - TP : True Positive (실제 Positive를 Positive로 정확히 예측한 데이터)

  - 정확도, 정밀도, 재현율, F-점수

    - 정확도(Accuracy)와 오차행렬(Confusion_Matrix) 관계

      ![accuracy-cm](/img/accuracy-confusion_matrix.PNG)

    - 정밀도, 재현율, F-점수

      ![Precision-Recall](/img/precision-recall-f_ma.PNG)
