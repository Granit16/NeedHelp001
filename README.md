# NeedHelp001
Добрый день!

Создал image используя файл [Dockerfile.python](https://github.com/Granit16/NeedHelp001/blob/main/Dockerfile.python):

`FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt main.py .
RUN pip install -r requirements.txt
ENV DB_HOST=mysql
ENV DB_USER=root
ENV DB_PASSWORD=very_strong
ENV DB_NAME=example
ENV DB_TABLE_NAME=table
CMD ["python", "main.py"]`


Создал [compose.yaml](https://github.com/Granit16/NeedHelp001/blob/main/compose.yaml):

`version: "3"
services:

  mysql:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=very_strong
    ports:
      - 3306:3306

  mypython:
    image: mypython:1.0.0
    ports:
      - 5000:5000`

Выполняю `docker compose up -d`
https://github.com/Granit16/NeedHelp001/blob/main/docker%20compose%20up%20-d.png?raw=true
контейнер shvirtd-example-python-mysql-1 живет, а shvirtd-example-python-mypython-1 отлетает, в логах сообщение об ошибке подключения:

`Traceback (most recent call last):
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
mysql.connector.errors.DatabaseError: 2003 (HY000): Can't connect to MySQL server on 'mysql:3306' (111)`

https://github.com/Granit16/NeedHelp001/blob/main/docker%20logs%20shvirtd-example-python-mypython-1.png?raw=true
