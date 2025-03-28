# Пользовательские сценарии

### Заказ товара через мобильное/десктопное приложение
 - Клиент открывает мобильное/десктопное приложение «I'll Have the BLT».
 - Выбирает ближайший магазин из списка доступных (с учетом геолокации или вручную).
 - Добавляет сэндвич в корзину.
 - Клиент (если зарегистрирован) видит доступные акции и бонусы (например, скидка 10% или значок «колбаска» за заказ), выбирает и применяет их к корзине; незарегистрированный клиент видит только стандартные акции.
 - Выбирает способ получения заказа:
    - самовывоз;
    - доставка (доступна, если магазин поддерживает эту услугу, для доставки требуется подтвержденный мобильный телефон).
 - Выбирает способ оплаты:
    - онлайн (карта, QR-код, счет для юрлиц через внешний платежный шлюз);
    - в магазине (карта, QR-код, наличные);
    - курьеру (карта, QR-код, наличные).
 - Завершает оформление заказа:
    - если выбрана оплата онлайн или по счету: клиент оплачивает через внешний шлюз, после успешной оплаты заказ автоматически формируется;
    - если выбрана оплата в магазине или курьеру: клиент нажимает «Сформировать заказ» для подтверждения;
    - если клиент выбрал доставку, то перед оплатой система потребует подтвердить мобильный телефон с помощью временного кода (если ранее данный номер не был подтвержден).
 - Клиент получает уведомление (push в приложении, email или SMS):
    - номер заказа и статус (например, «Ваш заказ принят, готовность через 15 минут»);
    - если самовывоз: маршрут до магазина с учетом трафика (через внешний картографический сервис);
    - если доставка: ориентировочное время доставки и данные курьера (при необходимости).
    
#### Условия и правила
 Зарегистрированные клиенты:
   - имеют доступ к программе лояльности, т.е. накапливают бонусы (например, значки «колбаска», «сырок», «звездочки») за заказы, которые можно обменять на скидки.
   - получают приоритетные уведомления о пятничных, праздничных или национальных акциях. 
 Незарегистрированные клиенты:
   - могут использовать только стандартные акции, доступные в приложении.
   - при выборе доставки должны ввести имя, телефон и email для получения чека или интернет-факса.    
 Выбор оплаты
    1) онлайн (с помощью внешней системы – карта, qr-код, оплата по счету для юр лиц)
    2) оплата в магазине (карта, qr-код, наличные)
    3) оплата курьеру (qr-код, карта)     
 Онлайн-оплата или счет для юрлиц: 
   - заказ формируется автоматически после успешной транзакции.    
 Оплата наличными или курьеру: 
   - требует ручного подтверждения клиентом через кнопку «Сформировать/Подтвердить заказ».    
 При выборе магазина отображается информации о загрузке магазина и ориентировочное время ожидания выполнения заказа.
 При невозможности магазином выполнить заказ (нет ингредиентов, технические проблемы и т.д.):
   - клиент получает уведомление с предложением выбрать другой магазин или отменить заказ.
 Корзина:
   - для клиентов, которые 
       1) не зарегистрированы, 
       2) впервые зарегистрировались в сервисе
       3) делали заказы товаров менее полугода, если количество позиций в корзине превышает 20 штук, потребуется подтверждение оператора. Об этом факте в приложении появится соответствующее уведомление (к примеру, «ваш заказ превышает установленные лимиты. Дождитесь звонка оператора для подтверждения заказа»). Заказа получит статус только после подтверждения оператором.
    
------------

Схема:
![Схема взаимодействия клиент-заказ](https://github.com/Jony2Good/blt-microservice/blob/main/schema-client-order.jpg "Схема взаимодействия клиент-заказ")

------------


### Регистрация клиента в десктопном или мобильном приложении

1. Клиент запускает приложение «I'll Have the BLT» впервые (или после установки) или после перехода по url на десктопную версию. 
2. На главной странице приложения система отображает предложение зарегистрироваться (например, кнопка «Создать аккаунт» рядом с «Войти»). Может не регистрироваться и делать заказа без процедуры создания аккаунта. Но приложение должно прорекламировать «пользу» регистрации. 
3. Клиент выбирает «Создать аккаунт» и переходит на страницу регистрации.
4. На странице регистрации клиент должен ввести:
   - имя;
   - адрес электронной почты;
   - пароль;
   - подтверждение пароля
5. Клиент, проставив галочку в чек-бокс, выражает согласие с обработкой персональных данных системой.
6. Далее клиент нажимает кнопку  «Зарегистрироваться».
7. Система отправляет письмо с уникальной ссылкой для подтверждения email на указанный адрес. Клиент переходит по ссылке из письма для верификации почты. Срок действия ссылки 1 сутки.
8. После подтверждения email и перехода по ссылке система предлагает подключить двухфакторную аутентификацию:
   - клиент вводит номер телефона.
   - система отправляет временный код через SMS.
   - клиент вводит код для подтверждения номера телефона.
Клиент может пропустить этот шаг, нажав «Пропустить» или «Подключить позже».
9. После успешной регистрации, т.е. перехода по специально сгенерированной ссылке (и возможного подключения 2FA) клиент автоматически входит в приложение и попадает на главную страницу.
10. Клиент получает приветственное уведомление (push или email), а также информацию о программе лояльности (например, «Ваш первый значок «колбаска» уже начислен»). 

#### Условия и правила

1. Клиент не имеет аккунта в системе.
2. Обязательные данные: Имя, email, пароль (минимум 8 символов, включая буквы и цифры), подтверждение пароля.
3. Подтверждение email: Регистрация завершается только после перехода по ссылке из письма.
4. Двухфакторная аутентификация требует подтверждения номера телефона через SMS. Клиенту при использовании приложения, если он не подключил 2FA,  будут приходить ежедневно push сообщения с предложением подключить двухфакторную авторизацию (возможно какие-то акции).
5. Программа лояльности: 
    - зарегистрированные клиенты автоматически подключаются к программе и получают приветственный бонус (например, значок или скидку на первый заказ).
6. Регистрация сотрудников компании в приложении будет осуществляться пользователем со статусом  администратор (не относится к клиентскому сценарию).

### Вход клиента в мобильное/десктопное приложение

1. Клиент запускает приложение «I'll Have the BLT» после прошедшего процесса успешной регистрации.  
2. Система автоматически проверяет наличие активной сессии (ранее сохраненного JWT). 
 a) Успешная авторизация: 
  - если токен действителен (и устройство подтверждено при 2FA) на главной странице отображаются данные его профиля (имя и фото).
 b) Провал авторизации:
  - если токена нет или срок его действия истек, клиент пользуется приложение, но видит на месте своего профиля кнопки «Создать аккаунт» и «Войти».
3. Клиент выбирает «Войти» и переходит на страницу входа.
4. На странице входа клиент должен ввести:
 - адрес электронной почты;
 - пароль,
и затем нажимает кнопку «Войти».
5. Если у клиента подключена двухфакторная аутентификация, и он входит с нового устройства:
 - система отправляет временный код через SMS на номер телефона, указанный при регистрации;
 - клиент вводит полученный код в поле на экране и подтверждает устройство.
6. После успешного ввода данных (email/пароль и, при необходимости, кода 2FA):
 - клиент входит в приложение и попадает на главную страницу;
 - система отправляет push-уведомление: «Вы успешно вошли в приложение!»
7. Если вход не удался (например, неверный email/пароль):
 - система отображает сообщение: «Неверный email или пароль, попробуйте снова».
 - клиент может повторить попытку или выбрать «Восстановить пароль?» для восстановления. 
8. Если клиент выбрал «Восстановить пароль?»
 - клиент находится на странице входа в приложение и нажимает ссылку «Восстановить пароль?» (расположена под полями ввода email и пароля).
 - система перенаправляет клиента на страницу восстановления пароля.
 - на странице восстановления клиент вводит адрес электронной почты, связанный с аккаунтом, и нажимает кнопку «Отправить запрос».
 - система проверяет, существует ли аккаунт с указанным email:
  a) если email найден, система отправляет письмо с уникальной временной ссылкой для сброса пароля (срок действия ссылки 5 минут);
  b) если email не найден, система отображает сообщение: «Аккаунт с таким email не найден, проверьте введенные данные».
 - клиент получает письмо, открывает его и переходит по временной ссылке.
 a) ссылка перенаправляет клиента на страницу создания нового пароля в приложении, где он вводит: новый пароль, подтверждение нового пароля, а затем нажимает «Сохранить».
   - если у клиента подключена 2FA:
 a) cистема запрашивает подтверждение через SMS: отправляет временный код на номер телефона, указанный при регистрации;
 b) клиент вводит код для подтверждения личности.
  - после успешного ввода нового пароля (и кода 2FA, если требуется):
 a) система сохраняет новый пароль и завершает процесс восстановления;
 b) клиент видит отображение своего профиля (имя и фото). Имеет доступ к своему личному кабинету.
  - клиент получает push-уведомление: «Ваш пароль успешно изменен, вы вошли в систему».

------------
Схема:

![Схема аутентификации клиента](https://github.com/Jony2Good/blt-microservice/blob/main/auth-shema.jpg "Схема аутентификации клиента")

------------

### Доставка заказ-клиент

1. После подготовки заказа клиент получает уведомление: «Заказ передан курьеру». Имя курьера и ссылка для отслеживания его местоположения в реальном времени (через картографический сервис).
2. Курьер прибывает на адрес:
 - если оплата онлайн: клиент принимает заказ, курьер подтверждает доставку в системе.
 - если оплата курьеру: клиент оплачивает (картой, QR-кодом или наличными), курьер подтверждает оплату и доставку.
3. Клиент получает финальное уведомление: «Заказ успешно доставлен»
 - электронный чек или интернет-факс (отправляется на email или телефон).

#### Условия и правила

Зарегистрированные клиенты:
 - могут отслеживать курьера в реальном времени (если это реализовано).
 - получают бонусы за заказ с доставкой выше определенной суммы (например, значок «звездочка»).
  Незарегистрированные клиенты:
 - должны указать имя, телефон и email для связи и получения чека/факса.
 - отслеживание курьера недоступно 
Оплата:
 - онлайн: оплата проходит до передачи заказа курьеру, клиент не взаимодействует с оплатой при доставке.
 - курьеру: курьер должен иметь терминал для карт/QR-кодов или принимать наличные; оплата подтверждается вручную.
Доставка:
 - время доставки рассчитывается сервисом доставки с учетом трафика и расстояния (интеграция с картографическим сервисом);
 - если курьер задерживается (например, пробки), клиент получает обновленное время доставки через уведомление.
 Исключения:
 - если клиент не открывает дверь или не отвечает: курьер отмечает проблему в системе, заказ возвращается в магазин, клиент уведомляется;
 - если магазин не успевает подготовить заказ вовремя: клиент получает  уведомление с новым временем доставки или предложением отмены.

### Доставка курьер-клиент

1. Курьер получает уведомление о новом заказе через приложение:
 - номер заказа, состав заказа, адрес доставки клиента.
 - рекомендуемый маршрут (построенный через внешний картографический сервис с учетом трафика).
2. Курьер подтверждает готовность забрать заказ в магазине
3. Курьер прибывает в магазин, забирает подготовленный заказ и отмечает в системе статус «Заказ забран».
4. Курьер следует по маршруту к клиенту:
 - система обновляет статус заказа (например, «В пути»);
 - клиент может видеть местоположение курьера в реальном времени.
5. Курьер прибывает к клиенту:
 - если оплата онлайн: передает заказ и подтверждает доставку в приложении;
 - если оплата курьеру: принимает оплату (картой через терминал, QR-кодом или наличными), подтверждает транзакцию и доставку в системе.
6. Курьер завершает заказ, система фиксирует статус «Доставлен».





























