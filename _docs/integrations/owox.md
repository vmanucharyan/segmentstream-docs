---
layout: page
section: integrations
title: "OWOX"
order: 1
---

OWOX - платформа для стриминга сырых данных в Google BigQuery. SegmentStream позволяет отправлять данные о поведении ваших пользователей одновременно как в [Google Analytics](/integrations/google-analytics), так и в BigQuery с помощью сервиса стриминга от [OWOX](https://owox.ru/).

> Подключить OWOX можно только в том случае, если интеграция с [Google Analytics настроена через SegmentStream](/integrations/google-analytics)

### Навигация по странице
------
<ul class="page-navigation">
  <li><a href="#introduction">Введение</a></li>
  <li><a href="#trackerName">Имя трекера</a></li>
  <li><a href="#sessionStreaming">Включить сессионный стриминг</a></li>
  <li><a href="#integrationSetupCheck">Проверка корректности настройки интеграции</a></li>
</ul>

### <a name="introduction"></a>Введение
Чтобы настроить интеграцию с OWOX:
1. авторизуйтесь на сайте [segmentstream.com](https://admin.segmentstream.com/) и перейдите к панели управления интеграциями
2. Войдите на вкладку "Интеграции" и кликните по блоку с логотипом OWOX.
3. В открывшейся панели - настройте интеграцию.
![](/img/integrations.owox.1.png)

>Убедитесь, что в модуле SegmentStream "Приоритеты" интеграцию OWOX идет по важности после интеграции Google Analytics (правее и ниже).

### <a name="trackerName"></a>Имя трекера
------
OWOX полностью дублирует запросы, которые отправляет трекер Google Analytics к себе на сервера. Так как библиотека analytics.js может создавать несколько трекеров на одной странице, OWOX должен знать имя этого трекера. Скопируйте имя трекера из настроек [google analytics](/integrations/google-analytics/#15).

Просто откройте интеграцию с Google Analytics в интерфейсе SegmentStream, найдите поле "Имя трекера", скопируйте его и вставьте в поле "Имя трекера" в окне настройки OWOX.

>Если в настройке интеграции Google Analytics не задано Имя трекера, то и в настройке OWOX поле "Имя Трекера" нужно оставить пустым.

### <a name="sessionStreaming"></a>Включить сессионный стриминг
------
1. Активируйте тумблер "Включить сессионный стриминг"
2. Создайте в интерфейсе Google Analytics пользовательскую переменную с областью действия - сеанс.
![](/img/integrations.owox.2.png)
3. Заполните поле "Индекс пользовательской переменной" номером пользовательской переменной.

### <a name="integrationSetupCheck"></a>Проверка корректности настройки интеграции
------
После настройки интеграции в интерфейсе SegmentStream, но ДО ПУБЛИКАЦИИ - перейдите на сайт в режиме test_mode, [пройдитесь по воронке конверсии и проверьте, нет ли ошибок](/for-analyst/integrations#testing).
Если ошибок нет - опубликуйте текущую версию.
