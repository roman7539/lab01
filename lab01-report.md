# Лабораторна робота 1. Робота з СУБД PostgreSQL та основи SQL

## Загальна інформація

**Здобувач освіти:** [Борис Роман Михайлович]
**Група:** [ІПЗ-23]
**Обраний рівень складності:** [1/2/3]

## Виконання завдань
Вивести назви товарів та їхні ціни
Показати контактні дані співробітників
Завдання: Знайти всіх клієнтів з міста Київ
### Список таблиць

```sql
Рівень 1
SELECT * FROM orders 
WHERE order_status = 'delivered';
SELECT * FROM employees 
WHERE title LIKE '%продаж%';
SELECT * FROM products 
ORDER BY unit_price ASC;
SELECT * FROM customers 
ORDER BY contact_name ASC;
SELECT * FROM orders 
ORDER BY order_date DESC;
SELECT * FROM products 
ORDER BY unit_price DESC 
LIMIT 10;
SELECT * FROM orders 
ORDER BY order_date DESC 
LIMIT 5;
SELECT * FROM customers 
ORDER BY contact_name ASC 
LIMIT 8;

рівень 2
-- Клієнти на ім'я Іван
SELECT * FROM customers WHERE contact_name LIKE 'Іван%';

-- Товари зі словом "телефон" або "phone"
SELECT * FROM products WHERE product_name ILIKE '%телефон%' OR product_name ILIKE '%phone%';

-- Самостійні LIKE (бізнес-логіка: пошук за поштовими доменами та категоріями)
SELECT * FROM customers WHERE email LIKE '%@gmail.com'; -- Клієнти з поштою Gmail
SELECT * FROM products WHERE product_name LIKE '%iPhone%'; -- Тільки техніка Apple
SELECT * FROM suppliers WHERE company_name LIKE '%ТОВ%'; -- Тільки товариства з обмеженою відповідальністю

-- Діапазони та списки
SELECT * FROM products WHERE unit_price BETWEEN 15000 AND 50000;
SELECT * FROM customers WHERE city IN ('Київ', 'Харків', 'Одеса', 'Дніпро');

-- Перевірка на NULL (бізнес-логіка: знайти замовлення, які ще в дорозі)
SELECT * FROM orders WHERE shipped_date IS NULL;

рівень 3
-- Складна умова: Бренди без чохлів
SELECT * FROM products 
WHERE (product_name ILIKE '%Samsung%' OR product_name ILIKE '%Apple%') 
AND product_name NOT LIKE '%чохол%';

-- Вкладені умови (Категорії 1,2 дорожче 20к АБО все дешевше 5к)
SELECT * FROM products 
WHERE (unit_price > 20000 AND category_id IN (1, 2)) 
OR (unit_price < 5000);

-- Аналіз географії (бізнес-логіка: замовлення по конкретних регіонах)
SELECT * FROM orders WHERE ship_city = 'Київ' AND freight > 100;

-- Складне сортування (пагінація)
SELECT * FROM products 
ORDER BY category_id ASC, unit_price DESC 
LIMIT 5 OFFSET 10;
```

Результат: У базі даних створено 8 основних таблиць: categories, customers, employees, order_items, orders, products, regions, suppliers.
Результат 1: Отримано повний список клієнтів магазину. Це дозволяє побачити загальну кількість покупців, їхні типи (фізичні чи юридичні особи) та контактну інформацію.
Скріншот.
Результат 2: Сформовано перелік усіх товарів із цінами. Цей запит корисний для швидкої перевірки вартості продукції без зайвої технічної інформації.
Результат 3: Вибрано тільки тих клієнтів, які проживають у Києві. Це допомагає проаналізувати попит у столичному регіоні.
Результат 4: Отримано список найдорожчих товарів (ціна яких перевищує 25 000 грн). Це важливо для аналізу продажів у високому ціновому сегменті.
...


### Отримати всі записи з таблиці customers.

```sql
SELECT * FROM customers;
```
Результат: Виконання цього запиту дозволило отримати повний перелік клієнтів магазину.

Скріншот
рівень 1
<img width="1916" heig<img width="1916" height="686" alt="Знімок екрана 2026-01-18 134827" src="https://github.com/user-attachments/assets/6df00f38-53ba-4587-a243-2dcbe8b5cec0" />
рівень 2
<img width="1887" height="548" alt="image" src="https://github.com/user-attachments/assets/cdc1eb63-6324-47ee-8b5b-fb9e0aacda13" />
Рівень 3
<img width="1918" height="584" alt="image" src="https://github.com/user-attachments/assets/620e4c93-8682-4ece-bf15-18e5e862c737" />

[Продовжити для всіх завдань обраного рівня]


## Висновки
Обґрунтування: У ході виконання лабораторної роботи я успішно опанував основи мови SQL та роботу з СУБД PostgreSQL. Зокрема, я навчився:
Формувати базові запити за допомогою SELECT та FROM для отримання даних з різних таблиць. 
Фільтрувати інформацію за допомогою оператора WHERE, використовуючи текстові шаблони (LIKE, ILIKE) та чисельні діапазони (BETWEEN). 
Сортувати та обмежувати результати за допомогою ORDER BY та LIMIT, що дозволяє виділяти найбільш актуальні або топові записи. 
Працювати зі складною логікою, комбінуючи декілька умов за допомогою операторів AND та OR.
**Самооцінка**: [ваша оцінка роботи, 3-5]

**Обгрунтування**: [обґрунтування самооцінки]
