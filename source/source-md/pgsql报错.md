



# Flask-Migrate  + pgsql 执行报错psycopg2.errors.DuplicateTable: relation "user" already exists



**问题出现**: 全新项目, 本来是打算用mysql, 后来换pgsql, 一开始用mysql时执行过 `flask db migrate / flask db upgrade`, 测试ORM,, 换成pgsql后再执行`flask db upgrade`出现如上报错, 看字面意思是表已存在, 可pgsql中并没有此表!



**原因**: 一开始执行 `flask db migrate` 时 alembic 已经创建了记录(versions目录下的.py文件), 也就是说对 alembic 来说是已经创建过数据表了, 在sql语句执行前就被报错拦截住了, 所以即使数据库没有user表, 报错也提示表已存在!



**解决**: 直接把 versions 目录下记录全部删除, 重新执行 `flask db upgrade ` 