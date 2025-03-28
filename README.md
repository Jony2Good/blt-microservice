# Национальная сеть магазинов сэндвичей "I'll Have the BLT"

**Учебная задача**: используя один из паттернов декомпозиции, подготовить варианты разбиения на микросервисы.

**В качестве решения предоставить**:
1. Пользовательские сценарии.
2. Общую схему взаимодействия сервисов.
3. Для каждого сервиса описать назначение сервиса и его зону ответственности.
4. Описать контракты взаимодействия сервисов.

**Содержание задачи**:
Национальная сеть магазинов сэндвичей хочет включить услугу «факс в вашем заказе», но через Интернет (в дополнение к их текущей услуге отправки факсов)

Пользователи: тысячи, возможно, когда-нибудь миллионы

*Требования:*
- Пользователи размещают заказ, затем им сообщают время, когда они могут забрать свой сэндвич, и указания, как добраться до магазина (который должен быть интегрирован с несколькими внешними картографическими сервисами, включающими информацию о дорожном движении).
- Если магазин предлагает услугу доставки, отправьте водителя с сэндвичем к пользователю.
- Доступность мобильных устройств.
- Предлагать ежедневные национальные акции/специальные предложения.
- Предлагать местные ежедневные акции/специальные предложения.
- Сервис принимает оплату онлайн или лично/при доставке.

*Дополнительный контекст:*
- Сэндвич-магазины работают по франшизе, у каждого из них свой владелец.
- Головная компания планирует в ближайшем будущем выйти на зарубежный рынок.
- Цель корпорации — нанять недорогую рабочую силу для максимизации прибыли.

### Решение задачи

Используемые паттерны декомпозиции: Business Capability и Domain-Driven design.

*Ссылки на решение:*
[1. Пользовательские сценарии][1]
[2. Общая схема взаимодействия сервисов][2]
[3. Описание назначение сервисов и зоны их ответственности][3]
[4. Описание контрактов взаимодействия][4]
[5. Спецификация по стандартам OpenApi][5]

[1]: https://github.com/Jony2Good/blt-microservice/blob/main/scenario.md "Пользовательские сценарии"
[2]: https://github.com/Jony2Good/blt-microservice/blob/main/interaction-schema.md "Общая схема взаимодействия сервисов"
[3]: https://github.com/Jony2Good/blt-microservice/blob/main/purpose-area.md "Описание назначение сервисов и зоны их ответственности"
[4]: https://github.com/Jony2Good/blt-microservice/blob/main/contracts.md " Описание контрактов взаимодействия"
[5]: https://github.com/Jony2Good/blt-microservice/blob/main/specification-openapi.yaml "Спецификация по стандартам OpenApi"
