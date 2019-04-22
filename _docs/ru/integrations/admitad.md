---
layout: page
section: integrationsRU
title: "Admitad"
order: 1
---

В данном разделе вы узнаете:
* Как подключить или отключить Admitad на вашем сайте.
* Как настроить дедупликацию платных каналов.

Admitad - партнерская сеть, объединяющая рекламодателей и веб-мастеров. SegmentStream позволяет отправлять данные о покупках ваших покупателей в [Admitad](https://admitad.com/ru).

### Навигация по странице
------
<ul class="page-navigation">
  <li><a href="#0">Введение</a></li>
  <li><a href="#0_1">Условия для подключения</a></li>
  <li><a href="#1">Код кампании</a></li>
  <li><a href="#2">Тип действия</a></li>
  <li><a href="#3">Код действия по умолчанию</a></li>
  <li><a href="#4">Название cookie, в которой хранится идентификатор партнера</a></li>
  <li><a href="#5">Автоматический трекинг cookie</a></li>
  <li><a href="#6">Активировать дедупликацию</a></li>
  <li><a href="#7">utm_source переходов из admitad</a></li>
</ul>

### <a name="0"></a>Введение
------
С помощью SegmentStream можно установить пиксель Admitad на страницу "Спасибо за покупку", настроить сохранение источника трафика и идентификатора партнера в cookie, а также подключить модуль Retag.

Чтобы настроить интеграцию с Admitad:
1. Авторизуйтесь на сайте [segmentstream.com](https://admin.segmentstream.com/) и перейдите к панели управления интеграциями
2. Войдите на вкладку "Интеграции" и кликните по блоку с логотипом Admitad.
3. В открывшейся панели - настройте интеграцию.
![](/img/integrations.admitad.1.png)
<br />
Подробнее о настройках вы можете прочитать ниже.

### <a name="0_1"></a>Условия для подключения
------
Перед тем, как приступить к настройке интеграции в панели SegmentStream необходимо зарегистрироваться в подключаемой системе и подготовить все необходимые данные:
 - Запросить у менеджера AdmitAd тестовую ссылку
    - Важно чтобы ссылка содержала следующие GET_параметры: utm_medium, utm_source, admitad_uid. Если данных параметров нет или используются другие параметры, необходимо попросить менеджера AdmitAd привести ссылку к формату https://site.ru/?utm_medium=cpa&utm_source=admitad&utm_campaign=xxxxx&admitad_uid=yyyyyy
 - Код кампании
 - Все возможные коды действия и условия их применения, например:
    - 1 - покупка впервые
    - 2 - повторная покупка
      - или
    - 1 - покупка товаров из категории "Электроника"
    - 2 - покупка товаров из категории "Аксессуары"
    - 3 - ....
 - Идентификатор модуля ReTag, в случае если его нужно подключать
 - Ссылка на товарный фид для модуля ReTag. Нужна для сравнения идентификаторов товаров в фиде и слое digitalData.
 - Если AdmitAd уже работает на сайте необходимо уточнить у разработчика или аналитика название cookie, в которую сохраняется admitad_uid. После подключения интеграции через SegmentStream необходимо будет отключить заполнение cookie на стороне разработчиков.
 - Необходимо знать с какими каналами трафика utm_medium будет настроена дедупликация. Например: со всеми или только с CPA или CPA и CPC.

 Ниже более подробно описаны все поля настроек интеграции.

### <a name="1"></a>Код кампании
------
Код кампании является уникальным идентификатором вашего проекта в сети и выдается сотрудниками Admitad по вашему запросу.

### <a name="2"></a>Тип действия
------
Admitad - это партнерская сеть с оплатой за действие. Есть 2 вида действия: Покупка (Sale) и Заявка (Lead). Уточните тип действия у сотрудников Admitad.

### <a name="3"></a>Код действия по умолчанию
------
В зависимости от договоренностей с Admitad у вас может быть один или более кодов действия. Например, если за первую покупку в вашем интернет-магазине платите одну цену, а за повторную - другую.

Большинство интернет-магазинов платят одинаковую цену за все действия.  В этом случае у ас будет один код действия, который вы сможете узнать у сотрудников Admitad.

Если же у вас несколько кодов действия, необходимо будет настроить "Переменные событий".
В окне настроек интеграции Admitad нажмите на вкладку "Переменные событий" и нажмите добавить.

Ниже приведен пример настройки различных кодов действия в зависимости от номера покупки посетителя:
![](/img/integrations.admitad.2.png)


### <a name="4"></a>Название cookie, в которой хранится идентификатор партнера
------
В сети Admitad у каждого вебмастера есть уникальный идентификатор. Этот идентификатор присутствует во всех рекламных ссылках, ведущих на ваш сайт, в качестве GET-параметра. Чтобы запомнить вебмастера, который привел вам потенциального покупателя, необходимо сохранить идентификатор вебмастера в cookie. Тот вебмастер, чей номер окажется в cookie в момент оформления заказа, получит вознаграждение.

> Если Admitad уже был интегрирован с вашим сайтом ранее, рекомендуем указать в настройках прежнее название cookie, чтобы идентификаторы партнеров, которые в течение последнего времени приводили трафик на сайт, не потерялись.

### <a name="5"></a>Автоматический трекинг cookie
------
SegmentStream умеет автоматически сохранять идентификатор партнера в cookie на определенный срок.
Включите тумблер "Автоматический трекинг cookie", укажите время хранения в днях а также домен cookie.

> Если разные разделы вашего сайта расположены на поддоменах, например корзина расположена по адресу checkout.site.ru, укажите домен верхнего уровня в настройках интеграции

> Если вы уже сохраняете admitad_uid в определенную cookie - укажите ее название. После проверки - попросите разработчика отключить прежнее заполнение cookie.

### <a name="6"></a>Активировать дедупликацию
Дедупликация или атрибуция - это правило, в соответствии с которым ценность от выполненного заказа перераспределяется между всеми источниками трафика, которые приводили пользователя на сайт перед покупкой. В случае с партнерскими сетями чаще всего используется правило 'last cookie wins'. Это значит, что всю ценность забирает последний партнер.

По умолчанию дедупликация выключена. Это значит, что вебмастер, который приводил на сайт пользователя, получит свое вознаграждение не зависимо от того, приводили ли вебмастера других партнерских сетей или системы таргетированной и контекстной рекламы трафик на сайт позже.

Если включить дедупликацию, то система будет запоминать последний источник трафика (utm_source и utm_medium).
Если вы укажите список utm_medium, то SegmentStream не будет передавать в Admitad информацию о покупку, в случае если последний переход пользователя перед покупкой был с соответствующей utm_меткой. Например, если вы укажите 'cpc', то любые переходы из контекстной рекламы (если конечно так размечены объявления вашей контекстной рекламы) будут "затирать" предыдущие переходы по ссылкам вебмастеров.

Если вы укажите не один utm_medium, то любой переход по ссылке с любым utm_medium будет "затирать" предыдущие переходы по ссылкам вебмастеров.

> Если вы работаете одновременно с несколькими партнерскими сетями, настоятельно рекомендуем включить дедупликацию и указать utm_medium ссылок других партнерских сетей.

### <a name="7"></a>utm_source переходов из admitad
Для корректной работы дедупликации и учета партнерских вознаграждений необходимо указать utm_source партнерских ссылок. Имя данного параметра лучше уточнить у сотрудника Admitad.