## Скрипт для автоматического резервного копирования файлов



### Код

```
#!/bin/bash

# Директория для резервного копирования
source_dir="/home/user/Documents"

# Директория для хранения резервных копий
backup_dir="/home/user/Backup"

# Получение текущей даты и времени
datetime=$(date +"%Y-%m-%d_%H-%M-%S")

# Имя файла архива
backup_file="$backup_dir/backup_$datetime.tar.gz"

# Создание архива
tar -czvf "$backup_file" "$source_dir"

# Вывод сообщения
echo "Резервная копия успешно создана: $backup_file"

```



