# Чек-лист проверки процедуры получения кредита через мобильное приложение

## 1. Предварительные условия
- Клиент авторизован в системе
- Профиль клиента верифицирован
- Доступ к камере/галерее для загрузки документов
- Подключение к интернету стабильное

## 2. Инициирование заявки
- Отображение персональных кредитных предложений
- Работа кредитного калькулятора (сумма/срок/платеж)
- Валидация вводимых значений:
  - Минимальная/максимальная сумма
  - Корректность срока кредита
- Автоподстановка цели кредита

## 3. Заполнение данных
- Автозаполнение:
  - Персональные данные из профиля
  - Паспортные данные (если привязаны)
  - Данные о доходе (анализ транзакций)
  - Контактная информация
- Для залогового кредита:
  - Поиск по кадастровому номеру/VIN
  - Автоподгрузка данных из Росреестра/ГИБДД
  - Расчет предварительной стоимости имущества
- Загрузка документов:
  - Поддерживаемые форматы (PDF, JPG, PNG)
  - OCR-распознавание текста
  - Проверка читаемости фото

## 4. Проверки перед отправкой
- Валидация обязательных полей
- Проверка согласий:
  - Кредитная история
  - Обработка персданных
  - Условия договора
- Контроль ЛТВ (Loan-to-Value) для залога

## 5. Отправка заявки
- Индикатор отправки данных
- Push-уведомление о получении заявки
- SMS-подтверждение подачи заявки

## 6. Скоринг и проверки
- Автоматический скоринг (до 60 сек)
- Антифрод-проверка:
  - Анализ устройства
  - Геолокация
- Проверка залога:
  - Отсутствие обременений
  - Юридическая чистота
  - Соответствие оценки

## 7. Уведомления о статусе
- Push при предварительном одобрении
- SMS при полном одобрении
- Push/SMS при необходимости доп. документов
- Уведомление об отказе с кодом ошибки

## 8. Подписание документов
- Доступность договоров в приложении:
  - Кредитный договор
  - Залоговое соглашение (при наличии)
- Работоспособность подписания:
  - Биометрия
  - SMS-код
  - Резервные методы
- Таймер обратного отсчета (24 часа)

## 9. Регистрация залога (если применимо)
- Автоматическая подача в Росреестр/ГИБДД
- Отслеживание статуса регистрации
- Уведомление об успешной регистрации
- Обработка ошибок регистрации

## 10. Выдача средств
- Зачисление на указанный счет в течение 15 мин
- Push/SMS о зачислении
- Отображение кредита в разделе "Мои продукты"
- Формирование графика платежей

## 11. Обработка ошибок
- Некорректные данные:
  - Подсветка ошибочных полей
  - Подсказки по исправлению
- Технические сбои:
  - Сохранение черновика
  - Повторная отправка
- Ошибки интеграций:
  - Альтернативные каналы (чат с поддержкой)
  - Резервные сервисы

## 12. Тайм-ауты и ограничения
- 15-минутное неактивное окно
- 24-часовой лимит на подписание
- Лимит попыток подписания (3 раза)
- Ограничение на повторную подачу после отказа

## 13. Юридические аспекты
- Доступ к полному тексту договора
- Фиксация даты/времени подписания
- Сохранение подписанных копий в профиле
- Уведомление об условиях отзыва согласия

## 14. Тестирование на разных сценариях
- Беззалоговый кредит
- Кредит под недвижимость
- Кредит под автомобиль
- Кредит под оборудование
- Комбинированный залог

## 15. Мониторинг процесса
- Логирование каждого этапа
- Аналитика времени выполнения операций
- Отслеживание частоты ошибок
- Автооповещение поддержки при сбоях

## 16. Финальные проверки
- Корректность списания первого платежа
- Начисление процентов по графику
- Отображение задолженности в ЛК
- Работа досрочного погашения