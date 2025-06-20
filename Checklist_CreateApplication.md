# Чек-лист проверки кредитной заявки

## I. Обязательные поля и форматы данных

### Общая информация:
- `application_id`: Соответствует шаблону `XXX-YYYY-NNNNNN`.
- `application_date`: Дата в формате `YYYY-MM-DD`, не превышает текущую дату.
- `status`: Значение `under_review` (на рассмотрении).
- `applicationSource`: Корректное значение (`applicationSource_Mobile`).

### Данные заявителя (`applicant`):

#### Личная информация:
- `full_name`: Полное ФИО в формате "Фамилия Имя Отчество".
- `birth_date`: Возраст ≥ 21 года (дата рождения ≤ 2004-06-20).
- `passport`:
  - Серия: 4 цифры (0000).
  - Номер: 6 цифр (123456).
  - `issue_date`: Не старше 10 лет (≥ 2015-06-20).
  - `issued_by`: Не пустое.
- `snils`: Формат `XXX-XXX-XXX-XX` (11 цифр).
- `inn`: 12 цифр.

#### Контактная информация:
- `phone`: Формат `+7XXXXXXXXXX`.
- `email`: Содержит `@` и домен.
- Адреса (`registration`/`residential`): Не пустые.

#### Занятость:
- `employer`/`position`: Не пустые.
- `experience_months` ≥ 3 (мин. стаж).
- `salary` > 0.
- При `additional_income` > 0 указан `income_source`.

### Детали кредита (`loan_details`):
- `loan_type`: Допустимое значение (`consumer_loan`).
- `amount`: 50 000 ≤ Сумма ≤ 3 000 000 RUB.
- `currency`: `RUB`.
- `term_months`: От 12 до 60 месяцев.
- `purpose`: Не пустое.
- `interest_rate`: 5% ≤ Ставка ≤ 30%.

### Залог (`collateral`):
- `type`: Допустимое значение (`real_estate`).
- `estimated_value` ≥ `loan_amount` × 1.2 (коэффициент покрытия).

### Финансовые обязательства (`financial_obligations`):
- Для `existing_loans`:
  - `creditor`/`amount`/`monthly_payment`/`remaining_term_months` заполнены.
  - `amount` > 0, `monthly_payment` > 0.
- `dependents` ≥ 0.

### Согласия (`consents`):
- `credit_history_check` = `true`.
- `personal_data_processing` = `true`.
- `scoring` = `true`.

### Данные сотрудника банка (`bank_employee`):
- `id`/`name`/`department`: Заполнены.
- `department`: Допустимое значение (`retail_credit`).

### Срок действия (`expiration`):
- `value` > 0.
- `unit`: Допустимое значение (`TimeUnit_Hours`).

## II. Бизнес-логика
- **Платежеспособность**:
  - Ежемесячный платеж по новому кредиту + `existing_loans.monthly_payment` ≤ 50% от общего дохода (`salary` + `additional_income`).
- **Залоговое покрытие**:
  - `collateral.estimated_value` ≥ `loan_amount` × 1.2.
- **Срок действия заявки**:
  - `application_date` + `expiration.value` (часы) ≥ Текущая дата.
- **Валидность паспорта**:
  - Дата выдачи + 20 лет ≥ Текущая дата.
- **Источник дохода**:
  - При `additional_income` > 0 указан легальный источник.

## III. Дополнительные проверки
- Отсутствие дублей `application_id` в системе.
- Корректность адресов: совпадение регистрации и проживания (при наличии различий — флаг для проверки).
- Валидность СНИЛС/ИНН (контрольные суммы).
- История кредитов: Сумма долга (`existing_loans.amount`) ≤ 5 млн RUB.
- Комментарий:
  - Поля `snils`, `inn` и паспорт требуют верификации в государственных базах (ФНС, МВД).
  - При отклонении от стандартных лимитов (например, стаж < 3 мес.) — запрос пояснений от клиента.
  - Если заявка просрочена (`expiration`), статус меняется на `expired`.