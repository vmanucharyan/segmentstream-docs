---
layout: page
section: integrationsRU
title: "Criteo"
order: 1
---

В данном разделе вы узнаете:
* Как подключить или отключить Criteo на вашем сайте.
* Как проверить корректности настройки интеграции.
* Как настроить передачу кастомных сегментов.

Criteo - система динамического ретаргетинга. SegmentStream позволяет отправлять данные о поведении ваших пользователей в [Criteo](https://criteo.com/).

### Навигация по странице
------
<ul class="page-navigation">
  <li><a href="#0">Введение</a></li>
  <li><a href="#1">Необходимые события и переменные</a></li>
  <li><a href="#2">Criteo Account Id</a></li>
  <li><a href="#2_1">Используется фид с группами товаров</a></li>
  <li><a href="#3">Переменная DigitalData, где хранится номер сегмента пользователя</a></li>
  <li><a href="#4">Флаг: Использовать собственную дедупликацию</a></li>
  <li><a href="#5">Проверка корректности настройки интеграции</a></li>
</ul>

### <a name="0"></a>Введение
------
С помощью SegmentStream можно полностью интегрировать Criteo с вашим сайтом: события, хешированные email'ы пользователей, дедупликация и прочее. <br />
[Справка Criteo по интеграции с сайтом](https://support.criteo.com/hc/ru/sections/200972171-%D0%9A%D0%B0%D0%BA-%D0%B2%D0%BD%D0%B5%D0%B4%D1%80%D0%B8%D1%82%D1%8C-Criteo-OneTag) <br/><br/>
Чтобы настроить интеграцию с Criteo:
1. Авторизуйтесь на сайте [segmentstream.com](https://admin.segmentstream.com/) и перейдите к панели управления интеграциями
2. Войдите на вкладку "Интеграции" и кликните по блоку с логотипом Criteo.
3. В открывшейся панели - настройте интеграцию.
![](/img/integrations.criteo.settings.png)
<br />
Подробнее о настройках вы можете прочитать ниже.

### <a name="1"></a>Необходимые события и переменные
------
Для корректной работы интеграции вашего сайта с Criteo - необходимо настроить передачу определенных событий в массив `digitalData.events`. Список событий приведен ниже:

**Обязательные события**
* [Viewed Page](/ru/events/viewed-page)
* [Viewed Product Detail](/ru/events/viewed-product-detail)
* [Viewed Product Listing](/ru/events/viewed-product-listing)
* [Searched Products](/ru/events/searched-products)
* [Viewed Cart](/ru/events/viewed-cart)
* [Completed Transaction](/ru/events/completed-transaction)
* [Subscribed](/ru/events/subscribed)

Также необходимо настроить заполнение определенных переменных объекта `digitalData`. Список некоторых переменных приведен ниже:
* `page.type`
* `product` - объект product встречается в нескольких местах объекта `digitalData`: непосредственно в `digitalData.product`, в массивах `items` и `lineItems` объектов `listing`, `cart`, `transaction`.
* объекты `listing`, `cart`, `transaction`
* переменную `user.email` и/или `user.emailHash`
* и другие

> В случае одновременного заполнения переменных `user.email` и `user.emailHash`, **SegmentStream** будет отправлять в Criteo значение переменной `user.emailHash`. В случае отсутствия `user.emailHash`, **SegmentStream** сам будет хэшировать значение переменной `user.email` и передавать в Criteo.

### <a name="2"></a>Criteo Account Id
------
Идентификатор вашего аккаунта вы можете уточнить у вашего аккаунт-менеджера в Criteo. Как правило - это пятизначное число.

### <a name="2_1"></a>Используется фид с группами товаров
------
Criteo получает информацию о товарах, размещенных на сайте через XML-фид. С определенной периодичностью робот Criteo скачивает фид с вашего сервера. Такой фид содержит информацию о всех товарах, представленных на сайте.

[Подробнее о формате фида](https://support.google.com/merchants/answer/7052112)

Для корректной работы интеграции, Criteo также должен получать информацию о взаимодействии пользователей с товарами на сайте - просмотры, добавления в корзину, покупки и т.д. Система должна правильно сопоставить то, что она видит в поступающих событиях с XML-фидом.

[Подробнее о группировке товара](https://support.google.com/merchants/answer/6324507)

-Если вы используете группировку товаров с помощью параметра xml-фида `item_group_id` - обязательно активируйте данную настройку.
  >В данном случае id товара из Вашего XML-фида должен совпадать с `product.skuCode`. Обязательно передавайте `product.skuCode` и `product.id` в каждом объекте `product`.

 -Если вы НЕ используете группировку товаров с помощью параметра xml-фида `item_group_id` - Не активируйте данную настройку.
  >В данном случае id товара из Вашего XML-фида должен совпадать с `product.id` объекта `digitalData`

### <a name="3"></a>Переменная DigitalData, где хранится номер сегмента пользователя
------
Criteo позволяет вместе с каждым событием передавать пользовательские сегменты. Например если вы хотите полностью отключить ретаргетинг для определенного сегмента пользователей - вам необходимо создать числовую переменную в объекте `digitalData` и вставить ее адрес в поле настройки интеграции.
Например, для всех пользователей, на которых вы хотите отключить ретаргетинг, в переменную `digitalData.user.criteoSegment` вы передаете значение 1. Для остальных - 0.
Подробнее о создании переменных читайте в разделе [переменные](/ru/for-analyst/variables).

### <a name="4"></a>Флаг: Использовать собственную дедупликацию
------
Дедупликация - это признак атрибуции, который может быть отправлен в Criteo вместе с заказом. По умолчанию этот признак выключен. Это значит, что Criteo для настройки своих собственных алгоритмов машинного обучения использует свою собственную модель атрибуции.
> Модель атрибуции - это правило, по которому ценность конверсии/(суммы заказа) перераспределяется между всеми источниками трафика, которые приводили пользователя на сайт перед покупкой. Существует большое количество [моделей атрибуции](https://support.google.com/analytics/answer/1665189?hl=ru), самая распространенная из них last non-direct click. При использовании данной модели атрибуции - 100% ценности конверсии будет присвоено последнему непрямому источнику трафика. Например, если пользователь сначала пришел на сайт из поиска, потом из Criteo, потом набрал URL адреса в браузере - вся ценность заказа будет присвоена источнику "Criteo".

В случае использования "собственной дедупликации", SegmentStream будет запоминать источник (значение GET-параметра utm_source). Если это значение будет равно "criteo", транзакция будет атрибутирована источнику Criteo.

[Справка Criteo по параметру дедупликации](https://support.criteo.com/hc/ru/articles/205573701-%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80-%D0%B4%D0%B5%D0%B4%D1%83%D0%BF%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8)

### <a name="5"></a>Проверка корректности настройки интеграции
------
После настройки интеграции в интерфейсе SegmentStream, но ДО ПУБЛИКАЦИИ - перейдите на сайт в режиме test_mode, [пройдитесь по воронке конверсии и проверьте, нет ли ошибок](/ru/for-analyst/integrations#2).
Если ошибок нет - опубликуйте текущую версию.