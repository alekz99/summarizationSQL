# summarizationSQL

# summarizationRussianNews

# Суммаризация sql-запросов

Набор данных доступен по ссылке: https://github.com/ai-spiderweb/pauq

В данной работе были рассмотрены существующие sequence-to-seqence модели. Были дообучены четыре 
модели для суммаризации sql-запросов на русском и английском языках. Для дообучения моделей
использовался набор данных pauq, который состоит из запросов на языке SQL и вопросов-
пояснений на английском и русском языке.

Модель mBart показала лучшее качество на русском языке, но само качество модели невысокое.
Модель Bart показала лучшее качество суммаризации запросов на английском языке, кроме того,
полученное качество модели является высоким.

## Результаты обучения модели

|       | mbart-large-cc25| mt5-base | bart-large | codet5-base-multi-sum|
|-------|--------|---------|---------|---------|
|BLEU| 8.8664 | 5.0035 | 25.053 | 23.0288 |


## Примеры оригинальных и сгенерированных вопросов на русском языке

|Оригинальный запрос | Оригинальный вопрос | mbart-large-cc25 | mt5-base|
|-----------------------|---------------------------|---------------------------|---------------------------|
|select count ( * ) from singer ; | Сколько у нас певцов? | Какое общее количество исполнителей? | Найдите количество исполнителей, у которых есть песни. |
|select location , name from stadium where capacity between 5000 and 10000 ; | Каково расположение и названия всех станций вместимостью от 5000 до 10000? | Найдите местоположения и названия стадионов с вместимостью от 5000 до 10000 человек. | Найдите место и названия стадионов, в которых есть вместимость более 5000 и 10000. | 
|select country from singer where age > 40 intersect select country from singer where age < 30 ; | Показать страны происхождения певца старше 40 лет и певца младше 30 лет. | Найдите страны, в которых есть исполнители старше 40 лет и исполнители младше 30 лет. | Каковы страны, в которых есть певцы, которые более 40 лет? |
|select count ( * ) from pets where weight > 10 ; | Найдите количество домашних животных, вес которых превышает 10. | Найдите количество домашних животных весом более 10 кг. |  Найдите количество pets, вес которых менее 10 кг. |
|select t1.fname from student as t1 join has_pet as t2 on t1.stuid = t2.stuid join pets as t3 on t3.petid = t2.petid where t3.pettype = "черепаха" intersect select t1.fname from student as t1 join has_pet as t2 on t1.stuid = t2.stuid join pets as t3 on t3.petid = t2.petid where t3.pettype = "попугай" ; | Как зовут учеников, у которых в качестве домашних животных есть и черепахи, и попугаи? | Найдите имена студентов, у которых есть домашние животные, которые могут быть как кровавыми, так и лошадиными. | Найдите имена студентов, у которых есть черепаха. |

## Примеры оригинальных и сгенерированных вопросов на английском языке

|Оригинальный запрос | Оригинальный вопрос | bart-large | codet5-base-multi-sum|
|-----------------------|---------------------------|---------------------------|---------------------------|
|select count ( * ) from singer ; | How many singers do we have? | How many singers are there? | How many singers are there? |
|select location , name from stadium where capacity between 5000 and 10000 ; | What are the locations and names of all stations with capacity between 5000 and 10000? | What are the locations and names of stadiums with capacity between 5000 and 10000? | What are the locations and names of all stadiums with capacity between 5000 and 10000?  | 
|select country from singer where age > 40 intersect select country from singer where age < 30 ; | Show countries where a singer above age 40 and a singer below 30 are from. | What are the countries that have both singers older than 40 and singers younger than 30?  | What are the countries that have more than 40 and less than 30 singers? |
|select count ( * ) from pets where weight > 10 ; | Find the number of pets whose weight is heavier than 10. | How many pets have a weight greater than 10? |  How many pets have weight greater than 10?  |
|select t1.fname from student as t1 join has_pet as t2 on t1.stuid = t2.stuid join pets as t3 on t3.petid = t2.petid where t3.pettype = "черепаха" intersect select t1.fname from student as t1 join has_pet as t2 on t1.stuid = t2.stuid join pets as t3 on t3.petid = t2.petid where t3.pettype = "попугай" ; | What are the students' first names who have both cats and dogs as pets? | What are the first names of students who have both cats and dogs? | What are the first names of students who have cat or dog pet? |
