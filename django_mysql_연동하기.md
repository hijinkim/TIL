# django mysql 연동하기

> 대충 적고 나중에 정리해야지 ..



```shell
$ mysql -u root -p
```

```mysql
> create database db이름 character set utf8;
> create user '유저이름'@'%' identified by '비번';
> grant all on db이름.* to '유저이름'@'%';
> flush privileges; /* 사용자 관련 변경사항 동기화하는 명령인데 grant로 직접 권한 부여한 경우 실행하지 않아도 되는 명령어*/
```
host의 종류는 두 가지가 있다.

* localhost : 로컬에서만 접속 가능
* % : 모든 외부 접속 가능



```
pip install mysqlclient
```



settings.py

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
		'NAME' : 'mysql db 이름',
		'USER' : 'mysql user 이름(기본적으로는 root)',
		'PASSWORD' : '비밀번호',
		'HOST' : 'localhost',
		'PORT' : '포트번호',
    }
}
```



```
$ python manage.py makemigrations
$ python manage.py migrate
```



```mysql
mysql -u 유저이름 -p
> use db이름
> show tables;
```



++ 이미 사용 중인 포트일 경우 현재 그 포트를 사용하는 프로그램 죽이는 법