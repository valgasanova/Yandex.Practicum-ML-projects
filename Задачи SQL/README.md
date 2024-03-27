## В самостоятельном проекте вам нужно проанализировать данные о фондах и инвестициях и написать запросы к базе. 

Описание базы данных:
1) acquisition
Содержит информацию о покупках одних компаний другими.
Таблица включает такие поля:
- первичный ключ id — идентификатор или уникальный номер покупки;
- внешний ключ acquiring_company_id — ссылается на таблицу company — идентификатор компании-покупателя, то есть той, что покупает другую компанию;
- внешний ключ acquired_company_id — ссылается на таблицу company — идентификатор компании, которую покупают;
- term_code — способ оплаты сделки:
   - cash — наличными;
   - stock — акциями компании;
   - cash_and_stock — смешанный тип оплаты: наличные и акции.
- price_amount — сумма покупки в долларах;
- acquired_at — дата совершения сделки;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

2)company
Содержит информацию о компаниях-стартапах.
- первичный ключ id — идентификатор, или уникальный номер компании;
- name — название компании;
- category_code — категория деятельности компании, например:
- news — специализируется на работе с новостями;
- social — специализируется на социальной работе.
- status — статус компании:
- acquired — приобретена;
- operating — действует;
- ipo — вышла на IPO;
- closed — перестала существовать.
- founded_at — дата основания компании;
- closed_at — дата закрытия компании, которую указывают в том случае, если компании больше не существует;
- domain — домен сайта компании;
- network_username — профиль фонда в корпоративной сети биржи;
- country_code — код страны, например, USA для США, GBR для Великобритании;
- investment_rounds — число раундов, в которых компания участвовала как инвестор;
- funding_rounds — число раундов, в которых компания привлекала инвестиции;
- funding_total — сумма привлечённых инвестиций в долларах;
- milestones — количество важных этапов в истории компании;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

3) education
Хранит информацию об уровне образования сотрудников компаний.
- первичный ключ id — уникальный номер записи с информацией об образовании;
- внешний ключ person_id — ссылается на таблицу people — идентификатор человека, информация о котором представлена в записи;
- degree_type — учебная степень, например:
- BA — Bachelor of Arts — бакалавр гуманитарных наук;
- MS — Master of Science — магистр естественных наук.
- instituition — учебное заведение, название университета;
- graduated_at — дата завершения обучения, выпуска;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

4) fund
Хранит информацию о венчурных фондах. 
- первичный ключ id — уникальный номер венчурного фонда;
- name — название венчурного фонда;
- founded_at — дата основания фонда;
- domain — домен сайта фонда;
- network_username — профиль фонда в корпоративной сети биржи;
- country_code — код страны фонда;
- investment_rounds — число инвестиционных раундов, в которых фонд принимал участие;
- invested_companies — число компаний, в которые инвестировал фонд;
- milestones — количество важных этапов в истории фонда;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

5) funding_round
Содержит информацию о раундах инвестиций. 
- первичный ключ id — уникальный номер инвестиционного раунда;
- внешний ключ company_id — ссылается на таблицу company — уникальный номер компании, участвовавшей в инвестиционном раунде;
- funded_at — дата проведения раунда;
- funding_round_type — тип инвестиционного раунда, например:
- venture — венчурный раунд;
- angel — ангельский раунд;
- series_a — раунд А.
- raised_amount — сумма инвестиций, которую привлекла компания в этом раунде в долларах;
- pre_money_valuation — предварительная, проведённая до инвестиций оценка стоимости компании в долларах;
- participants — количество участников инвестиционного раунда;
- is_first_round — является ли этот раунд первым для компании;
- is_last_round — является ли этот раунд последним для компании;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

6) investment
Содержит информацию об инвестициях венчурных фондов в компании-стартапы.
- первичный ключ id — уникальный номер инвестиции;
- внешний ключ funding_round_id — ссылается на таблицу funding_round — уникальный номер раунда инвестиции;
- внешний ключ company_id — ссылается на таблицу company — уникальный номер компании-стартапа, в которую инвестируют;
- внешний ключ fund_id — ссылается на таблицу fund — уникальный номер фонда, инвестирующего в компанию-стартап;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

7) people
Содержит информацию о сотрудниках компаний-стартапов.
- первичный ключ id — уникальный номер сотрудника;
- first_name — имя сотрудника;
- last_name — фамилия сотрудника;
- внешний ключ company_id — ссылается на таблицу company — уникальный номер компании-стартапа;
- network_username — профиль фонда в корпоративной сети биржи;
- created_at — дата и время создания записи в таблице;
- updated_at — дата и время обновления записи в таблице.

## Задачи

1. Отобразите все записи из таблицы company по компаниям, которые закрылись.

SELECT *
FROM company
WHERE status = 'closed';

2. Отобразите количество привлечённых средств для новостных компаний США. Используйте данные из таблицы company. Отсортируйте таблицу по убыванию значений в поле funding_total.

SELECT funding_total
FROM company
WHERE category_code='news' AND country_code='USA'
ORDER BY funding_total DESC;

3. Найдите общую сумму сделок по покупке одних компаний другими в долларах. Отберите сделки, которые осуществлялись только за наличные с 2011 по 2013 год включительно.

SELECT SUM(price_amount)
FROM acquisition
WHERE term_code='cash' AND EXTRACT(YEAR FROM acquired_at::date) BETWEEN 2011 AND 2013;

4. Отобразите имя, фамилию и названия аккаунтов людей в поле network_username, у которых названия аккаунтов начинаются на 'Silver'.

SELECT first_name,
       last_name,
       network_username
FROM people
WHERE network_username LIKE 'Silver%';

5. Выведите на экран всю информацию о людях, у которых названия аккаунтов в поле network_username содержат подстроку 'money', а фамилия начинается на 'K'.

SELECT *
FROM people
WHERE network_username LIKE '%money%' AND last_name LIKE 'K%';

6. Для каждой страны отобразите общую сумму привлечённых инвестиций, которые получили компании, зарегистрированные в этой стране. Страну, в которой зарегистрирована компания, можно определить по коду страны. Отсортируйте данные по убыванию суммы.

SELECT country_code,
       SUM(funding_total)
FROM company
GROUP BY country_code
ORDER BY SUM(funding_total) DESC;

7. Составьте таблицу, в которую войдёт дата проведения раунда, а также минимальное и максимальное значения суммы инвестиций, привлечённых в эту дату.
Оставьте в итоговой таблице только те записи, в которых минимальное значение суммы инвестиций не равно нулю и не равно максимальному значению.

SELECT funded_at,
       MIN(raised_amount) AS min_amt, 
       MAX(raised_amount) AS max_amt
FROM funding_round
GROUP BY funded_at
HAVING MIN(raised_amount)!=0 AND MIN(raised_amount)!=MAX(raised_amount);

8. Создайте поле с категориями:
- Для фондов, которые инвестируют в 100 и более компаний, назначьте категорию high_activity.
- Для фондов, которые инвестируют в 20 и более компаний до 100, назначьте категорию middle_activity.
- Если количество инвестируемых компаний фонда не достигает 20, назначьте категорию low_activity.
Отобразите все поля таблицы fund и новое поле с категориями.

SELECT *,
       CASE
           WHEN invested_companies>=100 THEN 'high_activity'
           WHEN invested_companies<100 AND invested_companies>=20 THEN 'middle_activity'
           WHEN invested_companies<20 THEN 'low_activity'
       END
FROM fund;   

9. Для каждой из категорий, назначенных в предыдущем задании, посчитайте округлённое до ближайшего целого числа среднее количество инвестиционных раундов, в которых фонд принимал участие. Выведите на экран категории и среднее число инвестиционных раундов. Отсортируйте таблицу по возрастанию среднего.

SELECT CASE
           WHEN invested_companies>=100 THEN 'high_activity'
           WHEN invested_companies>=20 THEN 'middle_activity'
           ELSE 'low_activity'
       END AS activity,
       ROUND(AVG(investment_rounds)) as avg_rounds
FROM fund
GROUP BY activity
ORDER BY avg_rounds;

10. Проанализируйте, в каких странах находятся фонды, которые чаще всего инвестируют в стартапы. 
Для каждой страны посчитайте минимальное, максимальное и среднее число компаний, в которые инвестировали фонды этой страны, основанные с 2010 по 2012 год включительно. Исключите страны с фондами, у которых минимальное число компаний, получивших инвестиции, равно нулю. 
Выгрузите десять самых активных стран-инвесторов: отсортируйте таблицу по среднему количеству компаний от большего к меньшему. Затем добавьте сортировку по коду страны в лексикографическом порядке.

SELECT country_code,
       MIN(invested_companies) AS min_companies,
       MAX(invested_companies) AS max_companies,
       AVG(invested_companies) AS avg_companies
FROM fund      
WHERE EXTRACT(YEAR FROM founded_at) BETWEEN 2010 AND 2012   
GROUP BY country_code
HAVING MIN(invested_companies) > 0
ORDER BY avg_companies DESC, country_code
LIMIT 10;

11. Отобразите имя и фамилию всех сотрудников стартапов. Добавьте поле с названием учебного заведения, которое окончил сотрудник, если эта информация известна.

SELECT p.first_name,
       p.last_name,
       e.instituition
FROM people AS p
LEFT JOIN education AS e ON p.id=e.person_id;

12. Для каждой компании найдите количество учебных заведений, которые окончили её сотрудники. Выведите название компании и число уникальных названий учебных заведений. Составьте топ-5 компаний по количеству университетов.

SELECT c.name,
       COUNT(DISTINCT e.instituition)
FROM company AS c
INNER JOIN people AS p ON c.id=p.company_id
INNER JOIN education AS e ON p.id=e.person_id
GROUP BY c.name
ORDER BY COUNT(DISTINCT e.instituition) DESC
LIMIT 5;

13. Составьте список с уникальными названиями закрытых компаний, для которых первый раунд финансирования оказался последним.

SELECT DISTINCT c.name
FROM (SELECT company_id
      FROM funding_round
      WHERE is_first_round= 1 AND is_last_round=1) AS cid
INNER JOIN company AS c ON cid.company_id=c.id
WHERE c.status='closed'; 

14. Составьте список уникальных номеров сотрудников, которые работают в компаниях, отобранных в предыдущем задании.

SELECT DISTINCT p.id
FROM people AS p
INNER JOIN (SELECT DISTINCT cid.company_id
            FROM (SELECT company_id
                  FROM funding_round
                  WHERE is_first_round= 1 AND is_last_round=1) AS cid
            INNER JOIN company AS c ON cid.company_id=c.id
            WHERE c.status='closed') AS clc ON p.company_id=clc.company_id;

15. Составьте таблицу, куда войдут уникальные пары с номерами сотрудников из предыдущей задачи и учебным заведением, которое окончил сотрудник.

SELECT DISTINCT pid.id,
       e.instituition
FROM (SELECT DISTINCT p.id
      FROM people AS p
      INNER JOIN (SELECT DISTINCT cid.company_id
                  FROM (SELECT company_id
                        FROM funding_round
                        WHERE is_first_round= 1 AND is_last_round=1) AS cid
                  INNER JOIN company AS c ON cid.company_id=c.id
                  WHERE c.status='closed') AS clc ON p.company_id=clc.company_id) AS pid
INNER JOIN education AS e ON pid.id=e.person_id;   

16. Посчитайте количество учебных заведений для каждого сотрудника из предыдущего задания. При подсчёте учитывайте, что некоторые сотрудники могли окончить одно и то же заведение дважды.

SELECT DISTINCT pid.id,
       COUNT(e.instituition)
FROM (SELECT DISTINCT p.id
      FROM people AS p
      INNER JOIN (SELECT DISTINCT cid.company_id
                  FROM (SELECT company_id
                        FROM funding_round
                        WHERE is_first_round= 1 AND is_last_round=1) AS cid
                  INNER JOIN company AS c ON cid.company_id=c.id
                  WHERE c.status='closed') AS clc ON p.company_id=clc.company_id) AS pid
INNER JOIN education AS e ON pid.id=e.person_id
GROUP BY pid.id;     

17. Дополните предыдущий запрос и выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники разных компаний. Нужно вывести только одну запись, группировка здесь не понадобится.

SELECT AVG(count_inst)
FROM (SELECT pid.id,
       COUNT(e.instituition) AS count_inst
FROM (SELECT DISTINCT p.id
      FROM people AS p
      INNER JOIN (SELECT DISTINCT cid.company_id
                  FROM (SELECT company_id
                        FROM funding_round
                        WHERE is_first_round= 1 AND is_last_round=1) AS cid
                  INNER JOIN company AS c ON cid.company_id=c.id
                  WHERE c.status='closed') AS clc ON p.company_id=clc.company_id) AS pid
INNER JOIN education AS e ON pid.id=e.person_id
GROUP BY pid.id) AS edu;  

18. Напишите похожий запрос: выведите среднее число учебных заведений (всех, не только уникальных), которые окончили сотрудники Socialnet.

SELECT AVG(count_inst)
FROM (SELECT pid.id,
      COUNT(e.instituition) AS count_inst
      FROM (SELECT DISTINCT p.id
            FROM people AS p
            INNER JOIN (SELECT DISTINCT c.id
                        FROM company AS c
                        WHERE name='Socialnet') AS csn ON p.company_id=csn.id) AS pid
INNER JOIN education AS e ON pid.id=e.person_id
GROUP BY pid.id) AS edu; 

19. Составьте таблицу из полей:
- name_of_fund — название фонда;
- name_of_company — название компании;
- amount — сумма инвестиций, которую привлекла компания в раунде.
В таблицу войдут данные о компаниях, в истории которых было больше шести важных этапов, а раунды финансирования проходили с 2012 по 2013 год включительно.

SELECT f.name AS name_of_fund,
       c.name AS name_of_company,
       fr.raised_amount AS amount
FROM investment AS inv
INNER JOIN company AS c ON inv.company_id=c.id
INNER JOIN fund AS f ON inv.fund_id=f.id
INNER JOIN funding_round AS fr ON inv.funding_round_id=fr.id
WHERE c.milestones>6
AND EXTRACT(YEAR FROM fr.funded_at) BETWEEN 2012 AND 2023;

20. Выгрузите таблицу, в которой будут такие поля:
- название компании-покупателя;
- сумма сделки;
- название компании, которую купили;
- сумма инвестиций, вложенных в купленную компанию;
- доля, которая отображает, во сколько раз сумма покупки превысила сумму вложенных в компанию инвестиций, округлённая до ближайшего целого числа.
Не учитывайте те сделки, в которых сумма покупки равна нулю. Если сумма инвестиций в компанию равна нулю, исключите такую компанию из таблицы. 
Отсортируйте таблицу по сумме сделки от большей к меньшей, а затем по названию купленной компании в лексикографическом порядке. Ограничьте таблицу первыми десятью записями.

WITH
    acquiring AS (SELECT company.name AS buyer,
                         acquisition.price_amount AS price,
                         acquisition.id
                  FROM acquisition
                  LEFT JOIN company ON acquisition.acquiring_company_id=company.id
                  WHERE acquisition.price_amount>0),
    acquired AS (SELECT company.name AS bought,
                        company.funding_total AS investment,
                        acquisition.id
                 FROM acquisition
                 LEFT JOIN company ON acquisition.acquired_company_id=company.id
                 WHERE company.funding_total > 0)     
SELECT acqg.buyer,
       acqg.price,
       acqd.bought,
       acqd.investment,
       ROUND(acqg.price/acqd.investment) AS difference
FROM acquiring AS acqg 
JOIN acquired AS acqd ON acqg.id=acqd.id
ORDER BY acqg.price DESC, acqd.bought
LIMIT 10;

21. Выгрузите таблицу, в которую войдут названия компаний из категории social, получившие финансирование с 2010 по 2013 год включительно. Проверьте, что сумма инвестиций не равна нулю. Выведите также номер месяца, в котором проходил раунд финансирования.

SELECT c.name,
       fr.month
FROM company AS c
JOIN (SELECT company_id,
             EXTRACT(MONTH FROM funded_at) as month
      FROM funding_round
      WHERE EXTRACT(YEAR FROM funded_at) BETWEEN 2010 AND 2013
      AND raised_amount!=0) AS fr ON c.id=fr.company_id
WHERE c.category_code='social';

22. Отберите данные по месяцам с 2010 по 2013 год, когда проходили инвестиционные раунды. Сгруппируйте данные по номеру месяца и получите таблицу, в которой будут поля:
- номер месяца, в котором проходили раунды;
- количество уникальных названий фондов из США, которые инвестировали в этом месяце;
- количество компаний, купленных за этот месяц;
- общая сумма сделок по покупкам в этом месяце.

WITH 
funding AS (SELECT EXTRACT(MONTH FROM fr.funded_at::date) AS funding_month,
                   COUNT(DISTINCT f.id) AS usa_fund_id
            FROM fund AS f
            LEFT JOIN investment AS i ON f.id=i.fund_id
            LEFT JOIN funding_round AS fr ON i.funding_round_id=fr.id
            WHERE EXTRACT(YEAR FROM fr.funded_at::date) BETWEEN 2010 AND 2013
            AND f.country_code='USA'
            GROUP BY funding_month),
acquired AS (SELECT EXTRACT(MONTH FROM acq.acquired_at::date) AS deal_month,
                       COUNT(acquired_company_id) AS acquired_id_count,
                       SUM(price_amount) AS total_sum
                FROM acquisition AS acq
                WHERE EXTRACT(YEAR FROM acq.acquired_at::date) BETWEEN 2010 AND 2013
                GROUP BY deal_month)         
                
SELECT fu.funding_month,
       fu.usa_fund_id,
       acqd.acquired_id_count,
       acqd.total_sum
FROM funding AS fu
LEFT JOIN acquired AS acqd ON fu.funding_month=acqd.deal_month;

23. Составьте сводную таблицу и выведите среднюю сумму инвестиций для стран, в которых есть стартапы, зарегистрированные в 2011, 2012 и 2013 годах. Данные за каждый год должны быть в отдельном поле. Отсортируйте таблицу по среднему значению инвестиций за 2011 год от большего к меньшему.

WITH
     inv_2011 AS (SELECT country_code,
                         AVG(funding_total) AS avg_funding_2011
                 FROM company
                 WHERE EXTRACT(YEAR FROM founded_at::date)=2011
                 GROUP BY country_code),  
     inv_2012 AS (SELECT country_code,
                         AVG(funding_total) AS avg_funding_2012
                 FROM company
                 WHERE EXTRACT(YEAR FROM founded_at::date)=2012
                 GROUP BY country_code),
     inv_2013 AS (SELECT country_code,
                         AVG(funding_total) AS avg_funding_2013
                 FROM company
                 WHERE EXTRACT(YEAR FROM founded_at::date)=2013
                 GROUP BY country_code)                 
SELECT inv_2011.country_code,
       inv_2011.avg_funding_2011,
       inv_2012.avg_funding_2012,
       inv_2013.avg_funding_2013
FROM inv_2011
INNER JOIN inv_2012 ON inv_2011.country_code=inv_2012.country_code
INNER JOIN inv_2013 ON inv_2011.country_code=inv_2013.country_code
ORDER BY inv_2011.avg_funding_2011 DESC;
