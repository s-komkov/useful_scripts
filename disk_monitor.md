# Disk_monitor

### Скрипт для отправки алерта в телеграм о превышении заданного порога

```

#!/bin/bash

# Telegram bot token
bot_token="mybot_token"

# Telegram chat ID
chat_id="user_chat_id"

# Функция для отправки сообщения в Telegram
send_telegram_message() {
  curl -s -X POST https://api.telegram.org/bot$bot_token/sendMessage -d chat_id=$chat_id -d text="$1" > /dev/null
}

# Порог использования диска (в процентах)
threshold=30


# Получение информации об использовании диска
df -h | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{print $5 " " $6}' | while read output;
do
  # Разделение информации на использование и точку монтирования
  usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1)
  partition=$(echo $output | awk '{ print $2 }' )

  
  # Проверка, превышает ли использование порог
  if [ $usep -ge $threshold ]; then
    # Отправка уведомления в Telegram
    send_telegram_message "Внимание! На разделе $partition осталось мало места: $usep% использовано."
  fi
done

```