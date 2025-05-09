### 項目簡介
這是的實驗實現了一個基於PyTorch的支持向量機（SVM）分類器，並應用K-anonymity算法來對成人數據集（Adult Dataset）進行匿名化處理。該項目旨在展示如何在保持資料隱私的前提下進行機器學習模型的訓練和評估。

### 使用套件
```
Python 3.8
pandas
numpy
torch
scikit-learn
```

### 使用說明
1. 直接運行main.ipynb

2. main.ipynb的功能包括:
> 讀取和預處理成人數據集\
> 對資料進行K-anonymity匿名化處理\
> 使用PyTorch定義和訓練SVM模型\
> 評估模型性能並打印結果

### 數據處理
這次使用的是Mondrian K-anonymity 算法來處理數據，具體步驟如下:\
1.分割屬性：選擇一個屬性並根據其中位數將數據分成兩部分。\
2.遞歸分割：對每個部分遞歸應用上述分割，直到每個部分的大小至少為K。\
3.泛化數據：對每個分割部分中的數據進行泛化，對於數值屬性使用均值，對於類別屬性使用最常見值。

## 模型說明
### 模型定義
這次的模型使用的是簡單的線性SVM模型來進行分類
```
class SVM(nn.Module):
    def __init__(self, input_dim):
        super(SVM, self).__init__()
        self.linear = nn.Linear(input_dim, 1)

    def forward(self, x):
        return self.linear(x)
```


## 運行結果
原始數據
```
Adult Dataset:
   age          workclass  fnlwgt   education  education-num  
0   39          State-gov   77516   Bachelors             13   
1   50   Self-emp-not-inc   83311   Bachelors             13   
2   38            Private  215646     HS-grad              9   
3   53            Private  234721        11th              7   
4   28            Private  338409   Bachelors             13   

        marital-status          occupation    relationship    race      sex  
0        Never-married        Adm-clerical   Not-in-family   White     Male   
1   Married-civ-spouse     Exec-managerial         Husband   White     Male   
2             Divorced   Handlers-cleaners   Not-in-family   White     Male   
3   Married-civ-spouse   Handlers-cleaners         Husband   Black     Male   
4   Married-civ-spouse      Prof-specialty            Wife   Black   Female   

   capital-gain  capital-loss  hours-per-week  native-country  income  
0          2174             0              40   United-States   <=50K  
1             0             0              13   United-States   <=50K  
2             0             0              40   United-States   <=50K  
3             0             0              40   United-States   <=50K  
4             0             0              40            Cuba   <=50K  
```
## 處理過後的數據
### 使用的K值為3
```
Anonymized Adult Dataset:
        age  workclass    fnlwgt  education  education-num  marital-status  \
0 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
1 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
2 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
3 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
4 -1.061172   0.315205 -1.604159   0.699390      -0.243656        0.280286   

   occupation  relationship      race       sex  capital-gain  capital-loss  \
0    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
1    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
2    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
3    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
4   -0.052078      0.519361 -0.812994 -0.909352     -0.147445     -0.218586   

   hours-per-week  native-country  income  
0       -0.599446       -0.103610      -1  
1       -0.599446       -0.103610      -1  
2       -0.599446       -0.103610      -1  
3       -0.599446       -0.103610      -1  
4       -0.495104        0.264924      -1  
```
### 使用的K值為4
```
Anonymized Adult Dataset:
        age  workclass    fnlwgt  education  education-num  marital-status  \
0 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
1 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
2 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
3 -1.422816  -0.208955 -1.620590  -0.612178      -1.027984        0.614067   
4 -1.061172   0.315205 -1.604159   0.699390      -0.243656        0.280286   

   occupation  relationship      race       sex  capital-gain  capital-loss  \
0    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
1    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
2    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
3    0.444261      0.363239 -2.310546 -0.909352     -0.009014     -0.218586   
4   -0.052078      0.519361 -0.812994 -0.909352     -0.147445     -0.218586   

   hours-per-week  native-country  income  
0       -0.599446       -0.103610      -1  
1       -0.599446       -0.103610      -1  
2       -0.599446       -0.103610      -1  
3       -0.599446       -0.103610      -1  
4       -0.495104        0.264924      -1  
```
### 使用的K值為5
```
Anonymized Adult Dataset:
        age  workclass    fnlwgt  education  education-num  marital-status  
0 -1.241994   0.053125 -1.612375   0.043606       -0.63582        0.447176   
1 -1.241994   0.053125 -1.612375   0.043606       -0.63582        0.447176   
2 -1.241994   0.053125 -1.612375   0.043606       -0.63582        0.447176   
3 -1.241994   0.053125 -1.612375   0.043606       -0.63582        0.447176   
4 -1.241994   0.053125 -1.612375   0.043606       -0.63582        0.447176   

   occupation  relationship     race       sex  capital-gain  capital-loss  
0    0.196091        0.4413 -1.56177 -0.909352     -0.078229     -0.218586   
1    0.196091        0.4413 -1.56177 -0.909352     -0.078229     -0.218586   
2    0.196091        0.4413 -1.56177 -0.909352     -0.078229     -0.218586   
3    0.196091        0.4413 -1.56177 -0.909352     -0.078229     -0.218586   
4    0.196091        0.4413 -1.56177 -0.909352     -0.078229     -0.218586   

   hours-per-week  native-country  income  
0       -0.547275        0.080657      -1  
1       -0.547275        0.080657      -1  
2       -0.547275        0.080657      -1  
3       -0.547275        0.080657      -1  
4       -0.547275        0.080657      -1  
```

## 實驗結果
### 使用的K值為3
```
Evaluation Results:
           Original Data  Anonymized Data
Accuracy        0.816886         0.759531
Precision       0.713602         0.530166
Recall          0.457493         0.311613
AUC             0.697788         0.609951
```
### 使用的K值為4
```
Evaluation Results:
           Original Data  Anonymized Data
Accuracy        0.812908         0.749807
Precision       0.743187         0.516689
Recall          0.394391         0.169069
AUC             0.674216         0.557760
```
### 使用的K值為5
```
Evaluation Results:
           Original Data  Anonymized Data
Accuracy        0.818986         0.746712
Precision       0.728369         0.512153
Recall          0.450044         0.127927
AUC             0.696723         0.543127
```

### 感想
在這個專案中，我們成功地將K-anonymity算法應用於成人數據集，並使用PyTorch實現了SVM分類器。這次實驗讓我能夠更好地理解了K-anonymity的概念及其在保護資料隱私方面的重要性。

然而，我們也注意到，K-anonymity可能會對資料集的有效性和模型的性能產生影響。例如，過度的泛化可能導致模型無法充分學習數據的特徵。\
這表示在實際應用中，如何在隱私保護和數據有效性之間取得平衡是一個需要深入研究的課題。
