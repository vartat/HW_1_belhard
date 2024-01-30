# HW1-15-_belhard
Classification problem
Построение модели классификации для определения класса пассажира. Целевая переменная ‘Class’ может принимать одно из трех значений: ‘Business’, ‘Eco’, ‘Eco Plus’.


Данные **Airline Passenger Satisfaction**
1.	Gender: male or female
2.	Customer type: regular or non-regular airline customer
3.	Age: the actual age of the passenger
4.	Type of travel: the purpose of the passenger's flight (personal or business travel)
5.	Class: business, economy, economy plus
6.	Flight distance
7.	Inflight wifi service: satisfaction level with Wi-Fi service on board (0: not rated; 1-5)
8.	Departure/Arrival time convenient: departure/arrival time satisfaction level (0: not rated; 1-5)
9.	Ease of Online booking: online booking satisfaction rate (0: not rated; 1-5)
10.	Gate location: level of satisfaction with the gate location (0: not rated; 1-5)
11.	Food and drink: food and drink satisfaction level (0: not rated; 1-5)
12.	Online boarding: satisfaction level with online boarding (0: not rated; 1-5)
13.	Seat comfort: seat satisfaction level (0: not rated; 1-5)
14.	Inflight entertainment: satisfaction with inflight entertainment (0: not rated; 1-5)
15.	On-board service: level of satisfaction with on-board service (0: not rated; 1-5)
16.	Leg room service: level of satisfaction with leg room service (0: not rated; 1-5)
17.	Baggage handling: level of satisfaction with baggage handling (0: not rated; 1-5)
18.	Checkin service: level of satisfaction with checkin service (0: not rated; 1-5)
19.	Inflight service: level of satisfaction with inflight service (0: not rated; 1-5)
20.	Cleanliness: level of satisfaction with cleanliness (0: not rated; 1-5)
21.	Departure delay in minutes
22.	Arrival delay in minutes
Изначально данные предназначены для решения задачи классификации уровня удовлетворенности авиакомпанией пассажиром: Satisfaction или Neutral or dissatisfied.

Для решения использовалась **логистическая** и **полиномиальная регрессия** (2 степень).
Логистическая регрессия решает задачу бинарной классификации, но так как у целевого признака три категории ('Eco','Eco Plus','Business') рассмотрим подходы мультиклассовой логистической регрессии.

Для подхода one-vs-rest в классе LogisticRegression, необходимо использовать значение параметра multi_class = ‘ovr’, чтобы использовать softmax логистическую регрессию в sklearn, параметр multi_class = ‘multinomial’.

При исследовании оба параметра дают практически одинаковый результат, чуть лучше при multi_class = ‘multinomial’.


В датасете есть характеристики 'Class', 'Gender', 'Customer Type', 'Type of Travel', 'satisfaction' типа object, которые преобразовывались в категориальные. С последними ни логистическая, ни полиномиальная регрессия не работает. Использовались два подхода:
-  данные удалялись;
- трансформировались в числовые, используя LabelEncoder.

| accuracy       | LogisticRegression | PolynomialFeatures|
| ------------- |:------------------:| -----:|
| без категориальных данных     | 0.71077148|0.7759855|
| с преобразованными через LabelEncoder|0.78176008|0.828572528|

| confusion_matrix       | LogisticRegression | PolynomialFeatures|
| ------------- |:------------------:| -----:|
|без категориальных данных|[9243, 2344,  346],|[10170,  1578,   292],|
| |[3252, 9220, 1571],|[ 2324,  9985,  1623],|
| |[   0,    0,    0]|[    1,     1,     2]|
|с преобразованными через LabelEncoder|[10604,  1861,   470],|[11043,  1083,   262],|
| |[ 1891,  9703,  1447],|[ 1451, 10471,  1646],|
| |[   0,    0,    0]|[    1,     10,     9]|


Дерево решений (from sklearn import tree) дало результат accuracy=0.7896904835232522.
