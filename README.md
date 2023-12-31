### Домашнее задание к занятию 1. «Типы и структура СУБД» Баранов Сергей


## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/tree/virt-11/additional).


### Задача 1


Архитектор ПО решил проконсультироваться у вас, какой тип БД 
лучше выбрать для хранения определённых данных.

Он вам предоставил следующие типы сущностей, которые нужно будет хранить в БД:

- электронные чеки в json-виде,
- склады и автомобильные дороги для логистической компании,
- генеалогические деревья,
- кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации,
- отношения клиент-покупка для интернет-магазина.

Выберите подходящие типы СУБД для каждой сущности и объясните свой выбор.

- Электронные чеки в json виде:
Документо-ориентированный NoSQL, т.к. такие БД хранят данные как документы.
- Склады и автомобильные дороги для логистической компании:
Графовые БД, т.к. в такой структуре можно задавать дополнительные атрибуты для выбора оптимального маршрута.
- Генеалогические деревья:
Иерархическая БД. В ней данные представлены в виде древовидной структуры (родитель - потомок). Каждая запись имеет не более одного родителя и несколько потомков, что подходит для наших задач.
- Кэш идентификаторов клиентов с ограниченным временем жизни для движка аутентификации:
Key-Value БД. Например, можно использовать Redis, так как у него есть поддержка TTL, хранение данных в оперативной памяти и возможность масштабирования. Эти преимущества идеально подходят для кэша.
- Отношения клиент-покупка для интернет-магазина
Реляционные БД, так как они обеспечивают связанность данных между различными таблицами между собой (например, список клиентов и список товаров). В данном случае нам важно хранить данные о клиенте, о том, что покупал, какое кол-во, в какой период, в таком случае мы можем получать статистику и аналитику по людям.


--- 


## Задача 2

Вы создали распределённое высоконагруженное приложение и хотите классифицировать его согласно 
CAP-теореме. Какой классификации по CAP-теореме соответствует ваша система, если 
(каждый пункт — это отдельная реализация вашей системы и для каждого пункта нужно привести классификацию):

- данные записываются на все узлы с задержкой до часа (асинхронная запись);

СА
ЕL/PC

- при сетевых сбоях система может разделиться на 2 раздельных кластера;

AP
PA/EL

- система может не прислать корректный ответ или сбросить соединение.

CP
PA/EC

Согласно PACELC-теореме как бы вы классифицировали эти реализации?


--- 

## Задача 3

Могут ли в одной системе сочетаться принципы BASE и ACID? Почему?

Не могут, т.к. это два противоположных принципа. В основе BASE - доступность данных даже в ущерб согласованности. ACID основывается на согласованности данных и надежности в случае сбоев. 


---


## Задача 4

Вам дали задачу написать системное решение, основой которого бы послужили:

- фиксация некоторых значений с временем жизни,
- реакция на истечение таймаута.

Вы слышали о key-value-хранилище, которое имеет механизм Pub/Sub. 
Что это за система? Какие минусы выбора этой системы?

Key-value хранилище с механизмом pub/sub - это Redis. 
Redis - БД с высокой производительностью, за счет хранения данных в памяти, это с одной стороны плюс и в то же время может быть расценен, как минус, хранение в памяти позволяет быстро получить доступ к данным, но есть риск потери данных, в том числе сильно ограничены в рамках памяти. По этой причине подобного рода БД хорошо зарекомендовали себя в рамках кеша, могут использоваться, как модуль большой системы и работать в паре с другими сервисами в рамках микро сервисной архитектуры. Также, если рассматривать redis, как sub/pub систему, то БД не хранит у себя сообщения, отправляет потребителям и затем удаляет. 

К его недостаткам можно отнести:
- Хранение данных в ОЗУ. То есть размер базы ограничен памятью и есть проблемы с надежностью хранения данных;
- Не поддерживает SQL.

---

