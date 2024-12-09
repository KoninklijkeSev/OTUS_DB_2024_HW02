# OTUS_DB_2024_HW02

## **Домашнее задание**

Добавляем в модель данных дополнительные индексы и ограничения

**Цель:**
Применять индексы в реальном проекте.

**Описание/Пошаговая инструкция выполнения домашнего задания:**
1. Проводим анализ возможных запросов\отчетов\поиска данных.  
2. Предполагаем возможную кардинальность поля.
3. Создаем дополнительные индексы - простые или композитные.
4. На каждый индекс пишем краткое описание зачем он нужен (почему по этому полю\полям).
5. Думаем какие логические ограничения в БД нужно добавить - например какие поля должны быть уникальны, в какие нужно добавить условия, чтобы не нарушить бизнес логику. Пример - нельзя провести операцию по переводу средств на отрицательную сумму.
6. Создаем ограничения по выбранным полям.

**Решение:**
1. Создание дополнительных индексов.
```sql
   CREATE INDEX idx_offers_area ON offers(area);
```
фывыф
