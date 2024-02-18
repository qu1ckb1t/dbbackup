# Домашнее задание к занятию "`Резервное копирование баз данных`" - `Аблогин Павел`


---

### Задание 1

1.1. `Подойдет инкрементное или дифференциальное резерное копирование`

1.2. `Подойдет резервное копирование на уровне файловой системы в сочетании с копированием журналов предзаписи (WAL)`

1.3. `Кейс возможен при использовании репликации. Т.е. можно slave перевести в режим работы master в случае поломки master`

---

### Задание 2

2.1. ```
Сохранение дампа БД в сжатый архивный файл настраиваемого формата:

  pg_dump -Fc mydb > db.dump

Восстановление архивного файла в ту же БД, из которой он был сохранен, удаляя текущее содержимое этой БД:

  pg_restore -d postgres --clean --create db.dump

```

2.2. ```

Запуск резервирования может быть автоматизирован с помощью cron.

#crontab -e

#Выполнять дамп БД каждую неделю в понедельник в час ночи
* 1 * * 1 pg_dump -Fc mydb > /data/backup/`date +%Y%m%d`/db.dump

```
---

### Задание 3

1. ```

# Инкрементное резервное копирование в каталог /incr-backup/thursday на основе базового каталога /incr-backup/wednesday:
 
mysqlbackup --defaults-file=/home/dbadmin/my.cnf --incremental \
  --incremental-base=dir:/incr-backup/wednesday \
  --incremental-backup-dir=/incr-backup/thursday \
  backup

```

2. ```  Использование реплики даст преимущество в большинстве случаев, особенно там, где остановка БД для сервисного окна недопустима либо приведет к большим издержкам, например, при использовании в высоконагруженных системах. 
  Применение реплик в небольших проектах, например, для персональных блогов, вряд ли оправдано.`

---
