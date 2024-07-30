### 項目簡介
這是的實驗實現了一個基於PyTorch的支持向量機（SVM）分類器，並應用K-anonymity算法來對成人數據集（Adult Dataset）進行匿名化處理。該項目旨在展示如何在保持資料隱私的前提下進行機器學習模型的訓練和評估。

### 使用套件
```
    Python 3.7+
    pandas
    numpy
    torch
    scikit-learn
```

### 使用說明
1.直接運行main.ipynb

2.main.ipynb的功能包括:
    讀取和預處理成人數據集
    對資料進行K-anonymity匿名化處理
    使用PyTorch定義和訓練SVM模型
    評估模型性能並打印結果

### 運行結果
```
Adult Dataset:
   age  workclass  fnlwgt  education  education-num      marital-status  \
0   39          7   77516         10             13             4   
1   50          6   83311         10             13             2   
2   38          4  215646         12              9             2   
3   53          4  234721          1              7             2   
4   28          4  338409          9             14             2   

   occupation  relationship  race  sex  capital-gain  capital-loss  \
0          3             1     4    1             0             0   
1          5             5     4    1             0             0   
2          9             5     2    1             0             0   
3          9             5     2    1             0             0   
4          9             5     2    0             0             0   

   hours-per-week  native-country  income  
0              40              38       0  
1              13              38       0  
2              40              38       0  
3              40              38       0  
4              40              38       0  

Anonymized Adult Dataset:
   age  workclass        fnlwgt  education  education-num  marital-status  \
0  0.441383        0  2.960034e-16  -1.527243       -0.041667        0.674225   
1  0.441383        0  2.960034e-16  -1.527243       -0.041667        0.674225   
2 -0.036251        0  2.960034e-16  -1.527243       -0.041667        0.674225   
3 -0.513885        0  2.960034e-16  -1.527243       -0.041667        0.674225   
4  0.879367        0  2.960034e-16  -1.527243       -0.041667        0.674225   

   occupation  relationship  race       sex  capital-gain  capital-loss  \
0        0.0        0.459815   0.0  0.959251  -7.391986e-16  1.208683e-15   
1        0.0        0.459815   0.0  0.959251  -7.391986e-16  1.208683e-15   
2        0.0        0.459815   0.0  0.959251  -7.391986e-16  1.208683e-15   
3        0.0        0.459815   0.0  0.959251  -7.391986e-16  1.208683e-15   
4        0.0        0.459815   0.0  0.959251  -7.391986e-16  1.208683e-15   

   hours-per-week  native-country  income  
0       0.032411   0.874418       0  
1       0.032411   0.874418       0  
2       0.032411   0.874418       0  
3       0.032411   0.874418       0  
4       0.032411   0.874418       0  

Evaluation Results:
           Original Data  Anonymized Data
Accuracy        0.252183         0.251188
Precision       0.252183         0.251188
Recall          1.000000         1.000000
AUC             0.500000         0.500000

```

### 感想
在這個專案中，我們成功地將K-anonymity算法應用於成人數據集，並使用PyTorch實現了支持向量機（SVM）分類器。這次實驗讓我們更好地理解了K-anonymity的概念及其在保護資料隱私方面的重要性。

然而，我們也注意到，K-anonymity可能會對資料集的有效性和模型的性能產生影響。例如，過度的泛化可能導致模型無法充分學習數據的特徵。這表明在實際應用中，如何在隱私保護和數據有效性之間取得平衡是一個需要深入研究的課題。
