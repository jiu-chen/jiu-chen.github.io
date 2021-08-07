# sqlalchemy filter和filter_by区别


## 区别
| 方法      | 语法                   | > <（大于，小于）查询 | AND, OR查询 |
| --------- | ---------------------- | --------------------- | ----------- |
| filter    | 类名.用属性名，比较用= | 支持                  | 支持        |
| filter_by | 直接用属性名，比较用== | 支持                  | 支持        |

## Examples
```python
# filter
db.session.query(UserInfo.id).filter(UserInfo.id='1001').first()

db.session.query(UserInfo.id).filter(UserInfo.id='1001', UserInfo.name='chen').first()
```

```python
# filter_by
db.session.query(UserInfo.id).filter_by(id=='1001').first()
db.session.query(UserInfo.id).filter(id='1001', name='chen').first()
```


