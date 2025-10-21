# Таблица перехода Saga-транзакций

| Исходное состояние | Переходное состояние | Событие |
| --- | --- | --- |
| CREATE_PAYMENT | BANK_RESERVATION | Успешное создание запроса платежа |
| BANK_RESERVATION | FRAUD_VALIDATION | Успешная резервация средств клиента |
| FRAUD_VALIDATION | BANK_WITHDRAW | Успешная проверка на антифрод |
| BANK_WITHDRAW | PARTNER_TRANSFER | Успешное списание средств клиента |
| PARTNER_TRANSFER | PAYMENT_COMPLETED | Успешный перевод денег партнеру |
| BANK_RESERVATION | ABORT_PAYMENT | Не удалось зарезервировать средства |
| FRAUD_VALIDATION | ABORT_BANK_RESERVATION | Платеж отклонен |
| FRAUD_VALIDATION | FRAUD_MANUAL_CHECK | Требуется ручной анализ |
| FRAUD_VALIDATION | FRAUD_NOTIFICATION | Операция отклонена |
| FRAUD_MANUAL_CHECK | BANK_WITHDRAW | Ручная проверка подтверждена |
| FRAUD_MANUAL_CHECK | BANK_WITHDRAW | Ручная проверка не была завершена в течении 20 минут |
| FRAUD_MANUAL_CHECK | ABORT_BANK_RESERVATION | Платеж отклонен |
| FRAUD_MANUAL_CHECK | FRAUD_NOTIFICATION | Операция отклонена |
| PARTNER_TRANSFER | BANK_REFUND | Не удалось провести перевод партнеру в течении 1 часа |
| BANK_REFUND | ABORT_PAYMENT | Отмена платежа |
