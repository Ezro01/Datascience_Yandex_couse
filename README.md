# 1. Постановка задачи

Интернет-магазин «В один клик» столкнулся с проблемой снижения активности покупателей. Для удержания клиентов и повышения их вовлечённости необходимо:

1. Разработать модель, предсказывающую вероятность снижения покупательской активности.
2. Выделить сегменты клиентов с высоким риском снижения активности и предложить для них персонализированные стратегии.

Целевая переменная:
- Покупательская активность (бинарная: «снизилась» / «прежний уровень»).

# 2. Используемые данные
Данные содержат информацию о поведении клиентов, их взаимодействии с маркетинговыми кампаниями и финансовых показателях:
- market_file.csv — активность, сервисные характеристики, маркетинговые метрики.
- market_money.csv — выручка по периодам.
- market_time.csv — время, проведённое на сайте.
- money.csv — среднемесячная прибыль с клиента.

# 3. Предобработка данных

Проведены:

- Объединение таблиц (market_money и market_time преобразованы в широкий формат).
- Очистка от пропусков и дубликатов.
- Анализ выбросов и корреляций (удалены мультиколлинеарные признаки).
- Кодирование категориальных переменных (One-Hot, Label Encoding).
- Масштабирование числовых признаков (StandardScaler, MinMaxScaler).

# 4. Моделирование
Использованные модели
1. Логистическая регрессия (LogisticRegression)
2. Метод k-ближайших соседей (KNeighborsClassifier)
3. Дерево решений (DecisionTreeClassifier)
4. Метод опорных векторов (SVC)

## Метрики
Основная метрика — ##ROC-AUC## (учитывает дисбаланс классов).

## Лучшая модель
SVC (Support Vector Classifier) показал наивысшее качество:

- ROC-AUC = 0.907
- F1-score = 0.88
- Точность (Accuracy) = 0.906

# 5. Анализ важности признаков (SHAP)
Ключевые факторы, влияющие на активность:
1. Акционные_покупки (чем выше доля покупок по акции, тем ниже риск снижения активности).
2. Неоплаченные_продукты_штук_квартал (неоплаченные товары в корзине — негативный сигнал).
3. Страниц_за_визит и Средний_просмотр_категорий_за_визит (активные пользователи просматривают больше страниц).
4. Минут (предыдущий месяц) (снижение времени на сайте — индикатор падения интереса).

# 6. Сегментация клиентов
Выделен сегмент с высокой вероятностью снижения активности:

- Характеристики:
  - Высокая доля покупок по акциям.
  - Много неоплаченных товаров в корзине.
  - Низкое время на сайте в предыдущем месяце.
  - Малое количество просмотренных категорий.

## Рекомендации для сегмента
1. Персонализированные скидки на товары, оставленные в корзине.

2. Программы лояльности (бонусы за активность, например, за просмотр >5 категорий).

3. Таргетированные рассылки с напоминаниями о неоплаченных заказах.

4. Улучшение сервиса (снижение числа ошибок, упрощение checkout-процесса).

# 7. Итоги
- Разработана модель SVC, предсказывающая снижение активности с ROC-AUC = 0.907.
- Выделены ключевые факторы риска (акции, неоплаченные товары, активность на сайте).
- Предложены меры для удержания клиентов из риск-сегмента.

Автор: Зверков Роман
Дата: 17.05.2025
Используемые технологии: Python, Pandas, Scikit-learn, SHAP, Matplotlib/Seaborn.
