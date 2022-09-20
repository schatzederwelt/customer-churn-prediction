# Предиктивный анализ оттока клиентов
![churn customer](https://static9.depositphotos.com/1202020/1221/i/600/depositphotos_12212262-stock-photo-marketing-campaign-business-success.jpg)
## Описание проекта

**ЦЕЛЬ ПРОЕКТА:**

Провести исследование и построить модель **прогнозирования ухода клиентов** из банка, что позволит `сократить затраты` на привлечение новых клиентов.

В нашем распоряжении обезличенные данные пользователей и история `использования услуг`.


KPI успеха проекта - `F1-score >= 0.59` 

Это классический таргет для бизнес-задач. Будет отлично, если более **детальный анализ** позволит получить результаты с еще большей точностью)  

=======================================================================================

**ЛИЧНАЯ ЦЕЛЬ:**

В прошлом проекте с рекомендацией тарифов мы успели заметить проблему **дисбаланса классов**, а после обучения моделей обнаружили, что `accuracy` была неподходящей **метрикой**.

Наша логистическая регрессия показывала нулевой precision и recall для 1-го класса:

- Теперь мы вооружены  методами для **борьбы с неравными классами** и сможем протестировать их работу на практике. 


- Научимся правильно интерпретировать `Recall`, `Precision`, `F1_score`, `ROC_AUC` и `PR-кривые`. Посмотрим, действительно ли они могут искажать результаты на imbalanced классах, как об этом пишут.

Также испытаем новые инструменты:

1. Попробуем "на лету" строить **пайплайны** из данных с помощью `Pandas`  и использовать метод `make_pipeline` для трансформеров.


2. Проведем эксперименты подбора базовых гиперпараметров c визуализацией `learning_curve` и `validation_curve`


3. Посмотрим, как дополнительные **методы корреляции** (кроме Пирсона) могут помочь в анализе данных и построении качественной модели.


[Посмотреть проект](Customer_churn_prediction_v1.ipynb)

## Навыки

<div class="alert alert-success">
<br> ✔️ Исследовательский анализ </br>
<br> ✔️ Классификация  ✔️ Борьба с дисбалансом классов </br>
<br> ✔️ Числовые и категориальные признаки </br>
<br> ✔️ Корреляции Спирмена и Пирсона </br>
<br> ✔️ Анализ относительных частот</br>
<br> ✔️ ROC AUC ✔️ F1-score ✔️ Precision ✔️ Recall</br>
<br> ✔️ Пайплайны обработки данных</br>
</div>

## Исходные данные


```python
import pandas as pd

df = pd.read_csv("https://code.s3.yandex.net/datasets/Churn.csv")
display(df.iloc[:, :6].head(3))
df.iloc[:, 6:].head(3)
```


<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>RowNumber</th>
      <th>CustomerId</th>
      <th>Surname</th>
      <th>CreditScore</th>
      <th>Geography</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>15634602</td>
      <td>Hargrave</td>
      <td>619</td>
      <td>France</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>15647311</td>
      <td>Hill</td>
      <td>608</td>
      <td>Spain</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>15619304</td>
      <td>Onio</td>
      <td>502</td>
      <td>France</td>
      <td>Female</td>
    </tr>
  </tbody>
</table>
</div>





<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Tenure</th>
      <th>Balance</th>
      <th>NumOfProducts</th>
      <th>HasCrCard</th>
      <th>IsActiveMember</th>
      <th>EstimatedSalary</th>
      <th>Exited</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>42</td>
      <td>2.0</td>
      <td>0.00</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>101348.88</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41</td>
      <td>1.0</td>
      <td>83807.86</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>112542.58</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>42</td>
      <td>8.0</td>
      <td>159660.80</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>113931.57</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>


