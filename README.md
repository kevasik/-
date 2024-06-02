### Шаг 0 - Выбор темы
Мы решили анализировать репетиторов по нескольким предметам из Москвы. Работать решили с сайтом репетитор.ру, на котором размещены анкеты репетиторов с достаточной для нашей задачи информацией. Мы хотели проанализировать рынок репетиторских услуг в Мосвке, рассмотреть ценообразование, оценить, какие характеристики влияют на стоимость и посмотреть на инетересные закономерности в данных.
Основная цель состоит в разработке модели для предсказания стоимости репетиторских услуг. Проект состоит из несколько шагов, описание которых представлено ниже. 

### Шаг 1 - Сбор данных 
Мы парсили данные с сайта repetitor.ru с помощью BeatifulSoup, парсинг был выполнен 01.06.2024. Парсинг состоит из нескольких функий: get_information - функция делает запрос на сайт и возвращает даннные сайта, get_href - получаем ссылки на всех преподавателей и сохраняем в формате "преподаватель : предмет" ну и заключительное - get_tutor - обращается к странице конкретного преподавателя и собирается нужную нам информацию.

### Шаг 2 - Предварительная обработка
Мы получили следующие признаки:
1. Личность подтверждена - бинарный признак со значением {0,1}. Данные о том, предоставил ли репетитор свои паспортные данные платформе.
2. Статус - категориальный признак, область значения которого следующая: 'Частный преподаватель', 'Школьный преподаватель' 'Преподаватель университета или колледжа', 'Аспирант или ординатор очной формы обучения', 'Студент'.некоторая текущая "должность" преподавателя.
3. Стаж - числовой признак, дающий понимание о том, какое количество лет преподаватель обучает своему предмету. Область значения признака - R+.
4. На сайте - числовой признак, отображающий количество времени, прошедшего с регистрации тьютора на сайте repetitor.ru. Область значения признака - R+.
5. Заказы в работе - числовой признак, иллюстрирующий какое количество учеников у конкретного преподавателя было на момент парсинга 01.06.2024. Область значения признака - Z.
6. Оценка - числовой признак, отображающий среднюю оценку по отзывам учеников. Область значения признака - [0,5].
7. Количество отзывов - числовой признак, количество оставленных учениками отзывов о преподавателе. Область значения признака - Z.
8. Формат обучения - категорильный признак, предлогаемый репетитором формат занятий, область значения - {Дистанционно, У ученика, У преподавателя}.
9. Образование - категориальный признак, ВУЗ - который закончил преподаватель. Область значения - название ВУЗов России и мира.
10. Предмет - категориальный признак, предмет, который преподает тьютор. Область значений - ключи словаря object_list со 2 шага парсинга
11. Цена - таргет, который мы собираемся предсказывать. Область значения - R+
12. С отличием - бинарный признак, отображающий, был ли закончен ВУЗ преподавателем с отличием или нет.
В данних были пропуски, каждый тип из которых мы по-разному, в файле есть уточнения. 

### Шаг 3+4 - Визуализация + Создание новых признаков
Построили много разных визуализаций для признаков + создали несколько новых признаков для классификации некоторых категориальных переменных по здравому смыслу - например среди всех вузов выделили топ-10 и топ-20, но на визуализации увидели, что топ-20 вузов особо бессмысленно выделять, и оставили только 1-ый; поделили предметы по 3 классификациям, одна оказалась неинформативной (из визуализации). Проанализировали также и график для таргета - он будет позже в части с гипотезами. А еще добавили квадратов и полиномов в качестве вторичных признаков.

### Шаг 5 - Гипотезы 



### Шаг 6 - Машинное обучение


### Общие выводы
Рынок репетиторов, представленный на сайте repetitor.ru крайне разношерстен и не гомогенен: есть разные преподаватели с большим и маленьким стажем, преподающие логику или школьную математику. Также сами данные оказались неидальны: у многих тьюторов не было отзывов или были указаны неверно написанные названия ВУЗов, которые тот или иной тьютор окончил. Вследствие этого и некоторых других факторов построенные модели машинного обучения показали не лучший результат, метрики качества были далеки от идеала. Однако некоторые результаты от обучения модели были получены: важны комбинации таких признаков, как Стаж, Количество отзывов и На сайте. Полиноы, образованные от этих признаков, была наиболее информативны для предсказания цены.
