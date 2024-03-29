# Бизнес-контекст
Организация использует специально разработанные программные системы в операционной деятельности по кадастровой оценкой недвижимости. Данные программные системы не предоставляют аналитических функций сотрудникам. Объекты кадастровой оценки недвижимости поступают в виде машино-читаемых пакетов(архив) реестров(XML). Результаты формируемые в системе в ответ на них также в XML. Так же есть необходимость переводить в человеко-читаемый формат входящее реестры, для сотрудников. В организации присутствует запас серверных мощностей и квалифицированные ИТ кадры. Руководство желает использовать ИТ подразделение в разработке. Так же дополнительно необходимо реализовать в системе:
 - подсистему сбора рыночной информации - объявления о продаже объектов недвижимости(что будет называться аналогами) с сайтов;
 - подсистему массового присвоения кодов объектам недвижимости по справочнику.

# Бизнес-цели
Разработать систему аналитики и генерации отчётности сведений получаемых в результате проведения кадастровой оценкой недвижимости.

# Бизнес-драйверы
- Руководство не знает, как приходит кадастровая оценка;
- Нет возможности предоставить отчёт вышестоящему ведомству;
- Сотрудникам необходимы выгрузки в человеко-читаемом формате;
- Нужна основа, для перспективы введения ML в процессы.

# Стейкхолдеры и их потребности
- Руководство. Понимать и влиять на происходящие процессы, а также формировать аналитические отчёты об оценке недвижимости.
- Головное ведомство. Понимать качество и объём проводимой возложенной функции на организацию.
- Граждане. Хотят иметь равные права и сведенные к минимуму ошибок при оценке их объектов недвижимости.
- Работники. Свести к минимуму ошибки при проведении оценки приводящие их к ответственности в том числе и дисциплинарной. Получать выгрузки сведений из системы используемой в дальнейшей работе.

# Пользовательские истории
UC-1. Получение входящих реестров. Пользователи в автоматическом режиме получают выгрузку xlsx из поступивших реестров на оценку.

UC-2. Просмотр базовой статистики.	Пользователи заходят в веб интерфейс и видят статистику: количество реестров, количество объектов в реестре, реестры в работе и т.п.

UC-3. Получение расширенной статистики.	Пользователи используя инструменты(возможно BI) могут запрашивать и выгружать расширенные сведения в различных разрезах.

UC-4. Регистрация.	Пользователи могут зарегистрироваться и получить доступ к сведениям в web.

UC-5. Работа с аналогами.	Пользователи могут выгружать, по месяцам, и просматривать собранную рыночную информацию в виде текстовой информации(Excel) и скриншота каждого объявления.

UC-5. Работа с кодировкой.	Пользователи могут массово по критериям выбирать объекты из реестра и применять к ним код по справочнику.


# Атрибуты качества (и не функциональные требования)
- Импорт реестров в БД до часу. 
- Выполнение простых запросов до 5 минут. 
- Выполнение выгрузок в человеко-читаемом виде до 15 минут. 
- Предположительный объём хранение реестров ГКО за 5 лет - 10Гб. 
- Не допустима потеря сведений о поступивших пакетов реестров.
- Информация об ошибках при прогрузке реестров на почту.
- Постоянное хранение реестров как есть.

# Ограничения (технические и бизнес)
- Доступ к просмотру в веб должен быть ограничен.
- Почтовый сервер MS Exchange, в которую поступают реестры.
- Сервер общей папки на MS Windows Server 2016, в которую происходят выгрузки.
- Форматы файлов данных циркулирующих по системе: zip, pdf, jpg, xml, ods, xlsx, sig.
- Время на реализацию проекта 3 месяца.
- Человеческие ресурсы: сотрудники ИТ подразделения организации.

# Критические сценарии 
- Входящие и исходящие реестры парсятся из XML и загружаются в БД.
- Пользователи могут просматривать базовую статистику, совершать поиск и просмотр истории объекта недвижимости.
- Пользователям приходят сообщения о поступлении новых пакетов реестров вместе ссылкой на человеко-читаемый файл(xlsx) выгрузки данного реестра.
- Пользователи могут делать выгрузки о собранной рыночной информации.
- Пользователи массово присваивают коды к объектам недвижимости и могут выгружать результат.

# Критические характеристики
- врем ответа от системы не должно превышать 5 мин.
- уведомление о неудачных загрузках реестров
- время внедрения – 3 месяца
- доступность сервиса: процент ошибочных ответов(90%)

# Функциональные требования
Система должна обеспечить сбор, накопление и анализ поступающих и исходящих реестров ГКО. 
Реестры ГКО поступают в формат обмена – XML и соответствующей схеме XSD. Файлы XML находятся в архиве ZIP или RAR. Пакеты архива подписаны в формате p7s или SGN, либо отдельно в виде файла с расширением sig. Реестры разделены на два типа: массовая оценка и ежедневная оценка. Объём хранения информации на один реестр от 100Кб до 3Гбайт.
Системы, должна парсить XML файлы и предоставить их в человеко-читаемом виде. 
Система должна собирать и хранить собранную рыночную информацию с сайтов вместе со скриншотами.
Есть возможность присваивать массово, по фильтрам, объектам недвижимости коды.

Источники входящих реестров:
- почтовые сообщения с вложениями;
- почтовые сообщения с ссылкой на облако mail.ru;
- ручная загрузка.

Источники исходящих реестров:
- папка в шаре(smb protocol);
- ручная загрузка.

Источник рыночной информации:
- сайт "Авито".

Необходимо предусмотреть:
- возможность выгрузки реестра в формате Excel(xlsx);
- возможность отправки файла xlsx по почте на специальный адрес;
- просмотр содержимого реестров через web итерфейс;
- выполнение над данными реестров запросов, в том числе агрегированных запросов;
- возможность выполнения сложны аналитических функций;
- возможность выгрузки аналогов рыночной информации;
- массовой кодировки поступающих объектов недвижимости.


# Контекстная схема системы
![Диаграмма контекста](<./images/Диаграмма контекста.jpg>)

# Модель предметной области
Предметная область: аналитика государственная кадастровая оценка.

Способы выделения модели предметной области: объектная схема.

![Модель предметной области](<./images/Модель предметной области.jpg>)

# Функциональная декомпозиция

## На ограниченные контексты

### Контекст входящих реестров
![Контекст входящих реестров](<./images/Контекст реестров недвижимости.jpg>)

### Контекст кодировки
![Контекст кодировки](<./images/Контекст кодировки.jpg>)

### Контекст реестров оценки
![Контекст оценки](<./images/Контекст оценки.jpg>)

### Контекст рыночной информации
![Контекст рыночной информации](<./images/Контекст рыночной информации.jpg>)

## По границам сущностей
![Сущности](<./images/Сущности.jpg>)

# Оценка модифицируемости

## Сценарии изменений

Примеры:
 1. изменился список характеристик объектов недвижимости;
 2. необходимо добавить новый источник аналогов рыночной информации;
 3. возможность применять аналогичную кодировку, из истории ранее присвоенных кодов, к реестру объектов;
 4. возможность ставить в соответствие одному входящему реестру объектов несколько результирующих реестров(оценки, кодировок и зон);
 5. внесение изменений в зоны;
 6. в список характеристик объектов недвижимости добавилась геоинформация и теперь надо добавить геоинформацию к аналогам и оценочным зонам, для дальнейшего анализа.

### По ограниченным контекстам

 1. ВхР(входящие реестры) + К(кодировки);
 2. РИ(рыночная информация);
 3. К;
 4. К + РО(реестр оценок);
 5. РИ + К;
 6. ВхР + К + РИ.

### По границам сущностей

 1. О(объекты недвижимости);
 2. РИ(аналоги);
 3. РК(реестр кодировок);
 4. О + РК + РЗ(реестр зон) + РО(реестр оценки);
 5. РЗ + РИ;
 6. О + РЗ + РИ.

### Сравнительный анализ

|наименование контекста|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|входящие реестры|+|   |   |   |   |+|
|кодировка|+|   |+|+|+|+|
|оценки|   |   |   |+|   |   |
|рыночная информация|   |+|   |   |+|+|

|наименование сущности|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|объекты недвижимости|+| | |+| |+|
|рыночная информация | |+| | |+|+|
|реестр кодировок    | | |+|+| | |
|реестр зон          | | | |+|+|+|
|реестр оценки       | | | |+| | |

### Выводы

- Декомпозиция по контекстам:
    - внесение изменений затрагивает больше контекстов;
    - кодировка сильно загружена;
- Декомпозиция по сущностям:
    - внесение изменений затрагивает меньше сущностей;
    - многие сущности связаны с сущностью "объекты недвижимости".

# Взаимодействие сервисов

Критический сценарий:
    - Пользователи массово присваивают коды к объектам недвижимости и могут выгружать результат.

Причина оценки решения: первичная.

# Сервисы

## Сервис "Реестр объектов"

Описание: Сервис по управлению входящими реестра объектов недвижимости

Запросы:
 - получить объекты из входного реестра.

Команды: -

События: -

Зависимости: -

## Сервис "Реестр кодировки"

Описание: Сервис по кодированию и зонированию входящих объектов недвижимости входного реестра

Запросы:
 - получить все объекты из реестра кодирования;
 - получить объекты из реестра кодирования по фильтру; 
 - получить список кодировок по справочнику;
 - получить список зон.

Команды:
 - создать реестр кодирования;
 - заполнить реестр кодирования объектами из заданного входного реестра;
 - применить код и зону к объектам реестра кодирования согласно фильтру.

События: -

Зависимости:
 - Реестр объектов;
 - Реестр зон.

## Сервис "Реестр зон"

Описание: Сервис по управлению зон оценки.

Запросы:
 - получить актуальные зоны из реестра зон.

Команды: -

События: -

Зависимости: -

# Диаграмма последовательности

![Диаграмма последовательности](<./images/Диаграмма последовательности.jpg>)

# Оценка атрибутов качества

Определив ключевые характеристики архитектуры для этого решения, мы сможем затем определить наименее худшее решение.

## Функциональные требования

Сценарий: пользователи массово присваивают коды к объектам недвижимости и могут выгружать результат.

Характеристики:
 - решение частично реализует сценарий - необходимо добавить выгрузку.
 - Стоимость изменений

    CAPEX = Стоимость з/п.
    Стоимость инфраструктуры = 0, так как инфраструктуру под проект уже имеется.

    OPEX = Стоимость поддержки (Стоимость з/п).
    Стоимость лицензий = 0, будем использовать open source решения.

 - Скорость изменений: в следствии микросервисной архитектуры, то скорость изменений будет приемлемой.

## Отказоустойчивость

Кодировка одна из самых важных частей системы.

Сценарии:

    1. Падение одного из сервисов или СУБД.
    Доступность для клиента = Доступности всех сервисов и БД.

Комментарии: возможно необходимо проработать вопрос кэширования "Реестра зон" на стороне "Реестра кодировки". Так же необходимо продумать сценарий восстановления БД из бэкапа.

## Производительность

Сценарии:
    
    1. Система должна иметь приемлемый отклик при повышении объёма данных.

    - Время ответа для клиента, поскольку взаимодействие синхронное можно
    оценить как максимальное время одного из сервиса.
    Latency для клиента = максимальное время отклика одного из сервиса
    
    - Пропускная способность.
    RPS = минимальным RPS одного из сервиса.

Комментарии: производительность системы является важным атрибутом качества. Система должно иметь оптимизированное хранилище данных способная обрабатывать большой объем данных. 

## Модифицируемость

Сценарии:

    1. Изменение модели данных "Реестра объектов"
    
    - Стоимость изменений = И(поправить схему "Реестра объектов") + И(поправить схему "Реестра кодировки")

Комментарии: возможно стоит хранить данные "Реестра кодировки" и возможно "Реестра объектов" в не реляционной БД.


## Масштабируемость

Сценарии:

    1. Увеличение объема хранимых данных в 10 раз за год
    
    Система должна масштабироваться под увеличивающийся объём данных.
    
    Стоимость масштабирования = затраты на инфраструктуру
    
    Оценка деградация производительности оценить сложно ввиду многих влияния факторов: индексы, запросы и структура.

Комментарии: необходимо предусмотреть правильную структуру и подбор индексов БД, влияющих на производительность. Возможность масштабирования возможно достигнуть: вертикальным масштабированием - увеличение памяти, процессоров и т.д.; горизонтальным масштабированием  - вводом дополнительных нод.


# Диаграмма контейнеров
![Диаграмма контейнеров](<./images/Диаграмма контейнеров.jpg>)

# Декомпозиция слоя данных
![Декомпозиция слоя данных](<./images/ERD.jpg>)

### Витрина:

![Декомпозиция слоя данных - витрина](<./images/data_marts.jpg>)

# Деплоймент диаграмма
![Деплоймент диаграмма](<./images/Deployment.jpg>)

# [ADR](./ADR.md)
Перейдите по ссылке.
