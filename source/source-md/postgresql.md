# pgsql



## 一. 安装使用(mac)

- 安装 : `brew install postgresql`

- 启动: `brew services start postgresql`

- 创建用户: `createuser -P test`

- 创建数据库: `createdb -O test -E utf8 test_db`

- 连接数据库: `psql -U test test_db -h localhost -W`

  

## 二. 基操

### 1. 数据库

| 命令             | 说明                   |
| ---------------- | ---------------------- |
| \l               | list of databases      |
| \c database_name | 切换数据库             |
| \dt              | 查看当前数据库下所有表 |
| \d table_name    | 查看表结构             |

