# Raifhack-DS-2021
Хакатон от Райфайзен по Data Science. Ссылка: https://apply.raifhack.ru/competition

### ~160 место(TOP-40%).

## Задача:
Реализация модели оценки стоимости коммерческой недвижимости. 

Данные в обучающей выборке делятся на 2 типа:
  1) наблюдения с price_type = 1 (цена получена в результате ручной оценки);
  2) наблюдения с price_type = 0 (цена из объявления).

В тестовой выборке только наблюдения price_type = 1, поэтому мы обучали наши модели только на данных с ценами такого же типа.

Решение в файле `raifhack_main.ipynb`

Описание признаков в файле `opisanie_priznakov.pdf`

Final submission в файле `raif_final_sub.csv`

## Ход решения:
- ручная обработка признака floor и создание признака с количеством занимаемых помещением этажей;
- кодирование категориальных признаков с применением алгоритма Target Encoding;
- генерация новых признаков на основе признаков с самой высокой корреляцией с целевой переменной;
- заполнение пропусков константой;
- кластеризация данных по долготе и широте,
- логарифмирование целевой переменной.

Методы, которые не улучшили метрику:
- отбор признаков на основе корреляционного анализа;
- отбор признаков на основе важности признаков;
- генерация новых признаков на основе важности признаков;
- логарифмирование признака total_square(общая площадь помещения);
- заполнение пропусков в числовых признаках медианой или средним, группируя данные по региону.

## Установка
- войдите в google colab
- `pip install -U -r requirements.txt`

## Обучение и прогноз:
- разбиваем обучающую выборку на 8 фолдов, группируя по месяцам;
- поочередно обучаем 8 моделей **XGBRegressor** на подгруппах из всех месяцев, кроме одного, который используем для валидации;
- на каждом шаге прогнозируем тестовую выборку;
- усредняем результаты 8 моделей;
- на последнем шаге наш результат усредняем с прогнозом на основе реализации бейзлайна от организаторов(`target_03.csv`).

## Оценка:
Организаторами была предложена кастомная метрика, с которой можно ознакомиться в ноутбуке `raifhack_main.ipynb` в разделе "Метрика".

raif_metric:
- public score - **1.3852143678029196**;
- private score - **1.244600101577711**.

