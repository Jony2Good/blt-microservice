# Контракты взамиодействия сервисов
  1. Сервис оформления заказов (Order Service)
      - Проверка клиента: Запрос к Auth Service. Метод POST. Маршрут auth/check_users. В заголовке должен быть JWT-токен. Ответ (userId, name, email, address, auth: true/false)
      - Выбор магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores?lat={latitude}&lon={longitude}&delivery={true/false}. Входные данные: координаты клиента (lat, lon), флаг доставки (delivery). Ответ (id, title, address, supportDelivery: true/false, distance)
      - Меню магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores/{storeId}/menu. Входные данные: ID магазина (storeId). Ответ (storeId: [menu: [itemId, name, price, available]])
      - Применение скидок (не аутентифицированный пользователь) : Запрос к Discount Service. Метод POST. Маршрут /discounts/users. Входные данные (orderId, storeId, items, price). Ответ (discount_title, new_price)
      - Применение скидок (аутентифицированный пользователь) : Запрос к Discount Service. Метод POST. Маршрут /discounts/users. Входные данные (userId, orderId, storeId, items, price). Если выбрана скидка добавляется ключ discountId к запросу. Ответ (discount_title, new_price)
      - Оплата: Запрос к Payment Service. Метод POST. Маршрут /payments/create. Входные данные (orderId, amount, payment_method, store_id). Ответ (paymentId, amount, status: complited(онлайн), pending(магазин/курьер))
      - Доставка: Запрос к Delivery Service. Метод POST. Маршрут /deliveries/create Входные данные (orderId, stroeId, user: [id, phone, address]). Ответ (deliveryId, delivery_time, status)
      - Время готовности заказа: Запрос к Store Managment Service. Метод GET. Маршрут /stores/{storeId}/readiness?items={itemIds}. Ответ (storeId, readiness)
      - Уведомления клиента: Запрос к Notification Service. Метод POST. Маршрут /notifications. Входные данные (user:[id, phone,email], message, socket_channel). Ответ (userId, status)
      - Обратная связь от Payment Service: Получает обновление статуса оплаты (POST /orders/{orderId}/payment-status). Входные данные (orderId, paymentId, status).
      - Обратная связь от Delivery Service. Получает статус доставки (POST /orders/{orderId}/delivery-status). Входные данные (orderId, deliveryId, status).
  2. Сервис аутентификации (Authentication Service)





 













  






