# mysqldump导出数据


mysqldump
+ -h server address, localhost default
+ -t table: 只导出表数据
+ -d --no-data, 只导出表结构

### 只导出表结构，不导出数据
``` sql
mysqldump -uroot -p123 -d test_database > output.sql
```
### 只导出表数据，不导出结构
``` sql
mysqldump -uroot -p123 -t test_database > output.sql
```
### 导出整个数据库，表结构&数据
``` sql
mysqldump -uroot -p123 test_database > output.sql
```

### 导出单张表结构（不包含数据）
``` sql
mysqldump -uroot -p123 -d test_database test_tbl > output.sql
```
### 导出单张表数据（不包含表结构）
``` sql
mysqldump -uroot -p123 -t test_database test_tbl > output.sql
```
### 导出单个表 (表结构&表数据)
``` sql
mysqldump -uroot -p123 test_database test_tbl > output.sql
```

### 导出的表结构的时候去掉 auto_increment
```
mysqldump -uroot -p123 -d test_database | sed 's/ AUTO_INCREMENT=[0-9]*\b//g' > output.sql
```





