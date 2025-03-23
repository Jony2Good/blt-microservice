# Контракты взамиодействия сервисов
  1. Сервис оформления заказов (Order Service)
      - Проверка клиента: Запрос к Auth Service. Метод POST. Маршрут auth/check_users. В заголовке должен быть JWT-токен. Ответ (userId, name, email, address, auth: true/false)
      - Выбор магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores?lat={latitude}&lon={longitude}&delivery={true/false}. Входные данные: координаты клиента (lat, lon), флаг доставки (delivery). Ответ (id, title, address, supportDelivery: true/false, distance)
      - Меню магазина: Запрос к Store Managment Service. Метод GET. Маршрут /stores/{storeId}/menu. Входные данные: ID магазина (storeId). Ответ (storeId: [menu: [itemId, name, price, available]] )

  






