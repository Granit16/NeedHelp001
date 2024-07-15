# NeedHelp001
Добрый день!

Создал image используя файл https://github.com/Granit16/NeedHelp001/blob/main/Dockerfile.python

Создал compose.yaml

Выполняю docker compose up -d
контейнер shvirtd-example-python-mysql-1 живет, а shvirtd-example-python-mypython-1 отлетает, в логах сообщение об ошибке подключения:
Traceback (most recent call last):
  File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 334, in _open_connection
    self._cmysql.connect(**cnx_kwargs)
_mysql_connector.MySQLInterfaceError: Can't connect to MySQL server on 'mysql:3306' (111)

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/app/main.py", line 15, in <module>
    db = mysql.connector.connect(
  File "/usr/local/lib/python3.9/site-packages/mysql/connector/pooling.py", line 322, in connect
    return CMySQLConnection(*args, **kwargs)
  File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 151, in __init__
    self.connect(**kwargs)
  File "/usr/local/lib/python3.9/site-packages/mysql/connector/abstracts.py", line 1399, in connect
    self._open_connection()
  File "/usr/local/lib/python3.9/site-packages/mysql/connector/connection_cext.py", line 339, in _open_connection
    raise get_mysql_exception(
mysql.connector.errors.DatabaseError: 2003 (HY000): Can't connect to MySQL server on 'mysql:3306' (111)
