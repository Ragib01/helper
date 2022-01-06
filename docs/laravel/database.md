## migration
```
php artisan migrate:refresh --path=/database/migrations/create_table_name.php
```

## create table

```
CREATE TABLE failed_jobs (
id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
uuid VARCHAR(256) NOT NULL UNIQUE,
connection TEXT NULL,
queue TEXT NULL,
payload LONGTEXT NULL,
exception LONGTEXT NULL
)
```