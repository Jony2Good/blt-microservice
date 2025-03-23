# Контракты взамиодействия сервисов
  1. Сервис оформления заказов (Order Service)
    Проверка клиента
      Запрос к Auth Service. Метод POST. Маршрут auth/check_users. В заголовке должен быть JWT-токен. Ответ (userId, name, email, address, auth: true/false)
