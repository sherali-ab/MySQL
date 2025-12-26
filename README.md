# MySQL
#####################          BILET 1 
Удаление существующих таблиц:
DROP TABLE IF EXISTS
Удаление существующих обьектов:
DROP DATABASE IF EXISTS 

Создание таблиц:
CREATE TABLE(...);

Связь с таблицами:
FOREIGN KEY (название дланных) REFERENCES 'название таблиц' (название данных)

Заполнение таблиц данными:
INSERT INTO 'название таблицы' (данные таблицы) VALUES
Перечисление...;

-- ============================================
-- КОНТРОЛЬНО-ОЦЕНОЧНОЕ ЗАДАНИЕ 3: ЗАПРОСЫ
-- ============================================

-- Запрос 1: Отчет о продажах за выбранный месяц
-- (поля: дата, название книги, автор, количество, выручка (кол-во*цена), ФИО продавца)
-- Пример: за май 2024
SELECT 
    s.sale_date AS 'Дата',
    b.title AS 'Название книги',
    b.author AS 'Автор',
    s.quantity_sold AS 'Количество',
    (s.quantity_sold * b.sale_price) AS 'Выручка',
    se.name AS 'ФИО продавца'
FROM Sales s
JOIN Books b ON s.book_id = b.book_id
JOIN Sellers se ON s.seller_id = se.seller_id
WHERE MONTH(s.sale_date) = 5 AND YEAR(s.sale_date) = 2024
ORDER BY s.sale_date;

-- Запрос 2: Показать книги, цена продажи которых выше средней цены по магазину
SELECT 
    book_id AS 'ISBN',
    title AS 'Название книги',
    author AS 'Автор',
    sale_price AS 'Цена продажи'
FROM Books
WHERE sale_price > (SELECT AVG(sale_price) FROM Books)
ORDER BY sale_price DESC;

-- Запрос 3: Показать книги, которые есть в каталоге магазина, но отсутствуют на складе (кол-во = 0)
SELECT 
    book_id AS 'ISBN',
    title AS 'Название книги',
    author AS 'Автор',
    quantity_in_stock AS 'Количество на складе'
FROM Books
WHERE quantity_in_stock = 0;

UPDATE Books
SET sale_price = purchase_price * 1.10 * 1.25,
    purchase_price = purchase_price * 1.10
WHERE publisher_id = 1;
