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
   CREATE INDEX idx_products_name_description ON products(name,description);
   ...

   CREATE INDEX idx_categories_name ON categories(name);

   CREATE INDEX idx_manufacturers_name_address_phone_email ON manufacturers(name,address,phone,email);

   CREATE INDEX idx_suppliers_name_address_phone_email ON suppliers(name,address,phone,email);

   CREATE INDEX idx_prices_price ON prices(price);

   CREATE INDEX idx_customers_name_address_phone_email ON customers(name,address,phone,email);
```
   idx_products_name_description - быстрый поиск по имени продукта и его описанию
   idx_categories_name - быстрый поиск по категории продукта
   idx_manufacturers_name_address_phone_email - быстрый поиск по данным производителя
   idx_suppliers_name_address_phone_email - быстрый поиск по данным поставщика
   idx_prices_price - быстрый поиск по цене
   idx_customers_name_address_phone_email - быстрый поиск по данным покупателя

2. Логические ограничения в БД.

   ```sql
   CREATE TABLE "products"(
    "id" BIGINT UNIQUE NOT NULL,
    "category_id" BIGINT NOT NULL REFERENCES users ON ,
    "name" VARCHAR(255) NOT NULL,
    "description" TEXT NOT NULL,
    "manufacturer_id" BIGINT NOT NULL,
    "supplier_id" BIGINT NOT NULL,
    PRIMARY KEY ("id")
);

   СREATE TABLE "categories"(
    "id" BIGINT UNIQUE NOT NULL,
    "name" VARCHAR(255) NOT NULL
    PRIMARY KEY ("id")
);

   CREATE TABLE "manufacturers"(
    "id" BIGINT NOT NULL,
    "name" VARCHAR(255) NOT NULL,
    "address" VARCHAR(255) NOT NULL,
    "phone" VARCHAR(255) NOT NULL,
    "email" VARCHAR(255) NOT NULL
    PRIMARY KEY ("id")
);

   CREATE TABLE "prices"(
    "id" BIGINT NOT NULL,
    "product_id" BIGINT NOT NULL,
    "price" BIGINT NOT NULL CHECK (price > 0)
);
'''
