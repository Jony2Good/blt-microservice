# Контракты взамиодействия сервисов
  + Сервис оформления заказов (Order Service)
      1. Проверка клиента: Запрос к Auth Service. Метод POST. Маршрут auth/check_users. В заголовке должен быть JWT-токен. Ответ (userId, name, email, address, auth: true/false)
      2. Выбор магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores?lat={latitude}&lon={longitude}&delivery={true/false}. Входные данные: координаты клиента (lat, lon), флаг доставки (delivery). Ответ (id, title, address, supportDelivery: true/false, distance)
      3. Меню магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores/{storeId}/menu. Входные данные: ID магазина (storeId). Ответ (storeId: [menu: [itemId, name, price, available]])
      4. Применение скидок (не аутентифицированный пользователь) : Запрос к Discount Service. Метод POST. Маршрут /discounts/users. Входные данные (orderId, storeId, items, price). Ответ (discount_title, new_price)
      5. Применение скидок (аутентифицированный пользователь) : Запрос к Discount Service. Метод POST. Маршрут /discounts/users. Входные данные (userId, orderId, storeId, items, price). Если выбрана скидка добавляется ключ discountId к запросу. Ответ (discount_title, new_price)
      6. Оплата: Запрос к Payment Service. Метод POST. Маршрут /payments/create. Входные данные (orderId, amount, payment_method, store_id). Ответ (paymentId, amount, status: complited(онлайн), pending(магазин/курьер))
      7. Доставка: Запрос к Delivery Service. Метод POST. Маршрут /deliveries/create Входные данные (orderId, stroeId, user: [id, phone, address]). Ответ (deliveryId, delivery_time, status)
      8. Время готовности заказа: Запрос к Store Managment Service. Метод GET. Маршрут /stores/{storeId}/readiness?items={itemIds}. Ответ (storeId, readiness)
      9. Уведомления клиента: Запрос к Notification Service. Метод POST. Маршрут /notifications. Входные данные (user:[id, phone,email], message, socket_channel). Ответ (userId, status)
      10. Обратная связь от Payment Service: Получает обновление статуса оплаты (POST /orders/{orderId}/payment-status). Входные данные (orderId, paymentId, status).
      11. Обратная связь от Delivery Service. Получает статус доставки (POST /orders/{orderId}/delivery-status). Входные данные (orderId, deliveryId, status).
  + Сервис аутентификации (Authentication Service)
       1. Проверка клиента. Ответ для Order Service. Метод: POST auth/check_users. Входные данные (JWT-токен в заголовке). Ответ (userId, name, email, address, auth: true/false)
       2. Уведомление клиента. Запрос к Notification Service. Метод: POST /notifications. Входные данные (userId, message, socket_channel}. Ответ (userId, status)
  + Сервис управления магазинами (Store Management Service)
       1. Список магазинов. Ответ для Order Service.  Метод GET. Маршрут /stores?lat={latitude}&lon={longitude}&delivery={true/false}. Входные данные: координаты клиента (lat, lon), флаг доставки (delivery). Ответ (id, title, address, supportDelivery: true/false, distance)
       2. Меню магазина. Ответ для Order Service.  Метод GET. Маршрут /stores/{storeId}/menu. Входные данные: ID магазина (storeId). Ответ (storeId: [menu: [itemId, name, price, available]])
       3. Время готовности заказа. Ответ для Order Service. Метод GET. Маршрут /stores/{storeId}/readiness?items={itemIds}. Ответ (storeId, readiness)
       4. Адрес для доставки. Ответ для Delivery Service. Метод: GET /stores/{storeId}. Ответ (storeId, address).













 













  






