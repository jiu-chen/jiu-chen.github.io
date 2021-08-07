# mysqldump导出数据


mysqldump
+ -h server address, localhost default
+ -t table
+ -d --no-data, 不导出数据, 仅导出表结构

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


### 导出单个数据表结构（不包含数据）
``` sql
mysqldump -uroot -p123 -d test_database test_tbl > output.sql
```
### 导出单个表数据（不包含结构）
``` sql
mysqldump -uroot -p123 -t test_database test_tbl > output.sql
```
### 导出单个表 (表结构&表数据)
``` sql
mysqldump -uroot -p123 test_database test_tbl > output.sql
```






