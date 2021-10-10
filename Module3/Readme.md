# Задание для модуля 3

## Знакомство с клиентом Power BI

### Задание 1
Преобразованы данные из словаря DIM Clients в Power Query из такого вида:

![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task1.1.PNG)

В такой:

![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task1.2.PNG)

### Задание 2
Создан справочник Типов Категорий, чтобы связать таблицу с плановыми показателями и таблицу с фактическими показателями

![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task2.1.PNG)

![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task2.2.PNG)

### Задание 3
Создана мера, которая позволит сравнивать темпы прироста продаж с периодом -7 и -14 дней от текущей даты

```dax
Amount DoD% 7 = 
IF(
	ISFILTERED('Calendar'[Date]),
	ERROR("Быстрые меры временной аналитики можно группировать и фильтровать только по иерархии дат или столбцу первичных дат из Power BI."),
	VAR __PREV_DAYS = CALCULATE(SUM('Fact'[Amount]), DATEADD('Calendar'[Date].[Date], -7, DAY))
	RETURN
		DIVIDE(SUM('Fact'[Amount]) - __PREV_DAYS, __PREV_DAYS)
)
```

```dax
Amount DoD% 14 = 
IF(
	ISFILTERED('Calendar'[Date]),
	ERROR("Быстрые меры временной аналитики можно группировать и фильтровать только по иерархии дат или столбцу первичных дат из Power BI."),
	VAR __PREV_DAYS = CALCULATE(SUM('Fact'[Amount]), DATEADD('Calendar'[Date].[Date], -14, DAY))
	RETURN
		DIVIDE(SUM('Fact'[Amount]) - __PREV_DAYS, __PREV_DAYS)
)
```


![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task3.3.PNG)

### Задание 4
Переведены все продажи в Евро по курсу ЦБ на момент выполнения задания

![alt text](https://github.com/AnastasiaAvakimova/DE-101/blob/main/Module3/images/task4.2.PNG)
