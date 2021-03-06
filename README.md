책의 예제 파일과 관련된 추가 설명 파일입니다.

# 5장  MySQL 

## 1.1 root login 
 - mysql -u root -p
## 1.2 create database 
 - CREATE Database scrapingdata DEFAULT character set utf8;
## 1.3 create user 
 - CREATE USER 'scrapingman' identified by 'myPassword-1'; 
## 1.4 Gant user 
 - GRANT ALL on scrapingdata.* To scrapingman;
  
  

## 1.5 Python library 
- logging   : eliot  
- concurrent processing : concurrent.Future
- pydub : mp3 editing 
- Celery : pip install redis  celery  
- Celery Web UI : flower 

## 1.6 running Celery 
- Running Worker 
```
- celery -A crawler_with_celery_sample multi start download   -Q download -c 2 -l info --logfile=./worker-download.log --pidfile=./worker-download.pid 
- celery -A crawler_with_celery_sample multi start media   -Q media  -c 2 -l info --logfile=./worker-media.log --pidfile=./worker-media.pid
```

- Running Crawling 
```
- python crawler_with_celery_sample.py
```

- Celery WebUI 
```
- celery -A crawler_with_celery_sample flower 
```


# 6장 

## BOOK_DB Database Setup 

- mysql) create database book_db DEFAULT character set utf8;
- mysql) use book_db ; 

- mysql> CREATE table languages ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 name varchar(8) NOT NULL DEFAULT '' , 
 created_at timestamp NOT NULL Default current_timestamp  ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id ) )
 ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT  CHARSET=utf8mb4;

- mysql>  insert into languages ( id ,name ) values ( 1, '한국어') , ( 2, '영어');   

- mysql> CREATE table publishers ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 name varchar(128) NOT NULL DEFAULT '' , 
 created_at timestamp NOT NULL Default current_timestamp   ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id ) )
 ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT  CHARSET=utf8mb4;

- mysql> insert into publishers ( id, name) values ( 1, '위키 북스') , ( 2, '한빛미디어') , ( 3, ' Addison-Wesley') ;

- mysql> CREATE table books ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 publisher_id  int(11) NOT NULL DEFAULT '' ,
 title varchar(255) not null default '', 
 created_at timestamp NOT NULL Default current_timestamp   ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id ) )
 ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT  CHARSET=utf8mb4;

- mysql> insert into books  ( id, title, publisher_id , language_id ) values (  34973284, 'HTML5 웹 프로그래밍' , 2 ,1 ) , 
                       ( 57556147 ,  ' Hello Coding Python' , 2 ,1  ) , ( 71051687 , ' 파이썬을 이용한 머신러닝' , 1, 1 ) ;


## Scrapy Database Setup 

- mysql) create database quotes DEFAULT character set utf8;
- mysql) use quotes ; 

- mysql> CREATE table quotes ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 author varchar(255) NOT NULL DEFAULT '' ,
 text text, 
 text_hash  char(64) Default Null , 
 created_at timestamp NOT NULL Default current_timestamp  ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id ) ,
 Unique key text_hash( text_hash )  ) 
 ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT  CHARSET=utf8mb4;



- mysql> CREATE table tags  ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 name varchar(255) NOT NULL DEFAULT '' , 
 created_at timestamp NOT NULL Default current_timestamp   ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id ) ,
 unique key tag( name) )
 ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT  CHARSET=utf8mb4;



- mysql> CREATE table quotes_tags  ( 
 id int(11) unsigned NOT NULL AUTO_INCREMENT ,
 quote_id  int(11) NOT NULL DEFAULT '' ,
 tag_id int(11) not null , 
 title varchar(255) not null default '', 
 created_at timestamp NOT NULL Default current_timestamp   ,
 updated_at timestamp NOT NULL Default current_timestamp on UPDATE current_timestamp ,
 Primary Key( id )  , 
 unique key quote_tag ( quote_id, tag_id ) )
 ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT  CHARSET=utf8mb4;




## 프로젝트 파일의 일부
프로젝트를 만드는 경우, 프로젝트 파일 전체를 예제 파일로 넣는 것은 찾아보는 것을 오히려 힘들게 만들 수 있을 것이라 생각해서, 필요한 파일만 넣었습니다. 복사해서 사용해주세요.

- 코드 6-13 items.py = chapter_6/items.py
- 코드 6-14 quotes.py = chapter_6/quotes_1.py
- 코드 6-15 quotes.py = chapter_6/quotes_2.py
- 코드 6-18 quotes.py = chapter_6/quotes_3.py
- 코드 6-22 quotes.py = chapter_6/quotes_4.py
- 코드 6-24 piplines.py = chapter_6/piplines.py

## 설정 변화에 의해 바뀔 수 있는 코드
코드 6-26, 코드 6-27과 같은 설정 파일은 Scrapy 버전 변화에 따라서 바뀌는 경우가 굉장히 많습니다. 프로젝트를 생성한 후, 책에 적혀있는 것들만 추가해주세요. 복사해서 사용할 수 있게 첨부해보았습니다.

```python
ITEM_PIPELINES = {
    'my_project.pipelines.DatabasePipeline': 300,
}
```
```python
DEPTH_LIMIT = 1
ORATOR_CONFIG = {
    'mysql': {
        'driver': 'mysql',
        'host': 'localhost',
        'database': 'quotes',
        'user': 'root',
        'password': '',
        'prefix': '',
        'log_queries': True,
    }
}
```


# 7장

## Feed Generator 

- pip install feedgen 
- https://feedly.com 


## SAKILA Database 
- https://dev.mysql.com/doc/sakila/en/
- https://dev.mysql.com/doc/index-other.html 
- https://downloads.mysql.com/docs/sakila-db.tar.gz 
- mysql -u root < sakila-schema.sql
- mysql -u root < sakila-data.sql 


## Flashk app run
- pip install Flash 
- pip install peewee  : ORM library 
- pip install flask-restful : REST service 
- FLASK_APP=hell.py flask run 
- coding db.py  from ` python -m pwiz -e mysql -u root sakila ` 





## 프로젝트 파일의 일부

- 코드 7-15 models.py = chapter_7/models.py
- 코드 7-17 views.py = chapter_7/views.py
- 코드 7-18 urls.py = chapter_7/urls.py

## 설정 변화에 의해 바뀔 수 있는 코드
코드 7-16와 같은 설정 파일은 Django 버전 변화에 따라서 바뀌는 경우가 굉장히 많습니다. 프로젝트를 생성한 후, 책에 적혀있는 것들만 추가해주세요. 조금 긴 부분은 ➐의 다음 부분인데, 이는 복사해서 사용할 수 있게 첨부해보았습니다.

```python
REST_FRAMEWORK = { 
    'DEFAULT_FILTER_BACKENDS': (
        'rest_framework.filters.SearchFilter',
        'rest_framework.filters.OrderingFilter',
    ),
    'PAGE_SIZE': 10
}
```

# 8장

## 프로젝트 파일의 일부

- 코드 8-8 models.py = chapter_8/models.py
- 코드 8-10 admin.py = chapter_8/admin.py

