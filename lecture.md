<<<<<<< HEAD
# volume 생성
- 볼륨 생성
```bash
$ docker volume create --name my-volume
my-volume
```


- 볼륨 목록 확인
```bash
docker volume ls
```


# 볼륨 마운트하기
- 컨테이너 생성 시, 볼륨 마운트
- docker container [opts] : '--mount'
    + 링크 :
```bash
docker container --(생략)--\
--mount type=volume,source=my-volume,destination=/my-work 


$ docker container run \
--name ubuntu1 \
--rm \
--interactive \
--tty \
--mount type=volume,source=my-volume,destination=/my-work \
ubuntu:24.04
```
# 텍스트 파일 생성
```bash
root@ebb744e50054:/# echo 'Hello World From Container, Volume.' > /my-work/hello.txt
root@ebb744e50054:/# ls /my-work/
hello.txt
```


- volume 지우기
```bash
docker volume rm my-volume 
```

# 새로운 볼륨 작성 후, MySQL 컨테이너 마운트하기


```bash
# 생성
docker volume create --name db-volume

# MuSQL 설정 파일 확인
docker container run --rm mysql:8.4.2 cat /etc/my.cnf
# 아래 결과 중에서 datadir 부분을 destination에 넣는다.
# host-cache-size=0
# skip-name-resolve
# datadir=/var/lib/mysql
# socket=/var/run/mysqld/mysqld.sock
# secure-file-priv=/var/lib/mysql-files
# user=mysql

# pid-file=/var/run/mysqld/mysqld.pid
# [client]
# socket=/var/run/mysqld/mysqld.sock

# !includedir /etc/mysql/conf.d/


```
-컨테이너 생성
```bash
docker container run --name db1 --rm --detach --env MYSQL_ROOT_PASSWORD=1234 --env MYSQL_DATABASE=sample --publish 3306:3306 --mount type=volume,source=db-volume,destination=/var/lib/mysql \mysql:8.4.2
# f6313e71823c109931584a669fcb3ac2e64a1ddfdc1863af209a2b7970302416
```


- MySQL 접속
```bash
mysql --host=127.0.0.1 --port=3306 --user=root --password=1234 sample
```


-DB 생성 및 데이터 추가
```bash
create table user ( id int, name varchar(32) );
insert into user ( id, name) values (1, 'John' );
insert into user ( id, name) values (2, 'Evan' );
select * from user;
```
# DB 볼륨 확인
- 환경 변수가 불필요함 (이유 : Volume 데이터 안에 db1의 mysql 정보가 같이 저장됨)
- 두번째부터 컨테이너 생성할 때는 굳이 환경 변수 지정 안해도 됨!
```bash
docker container run --name db0 --rm --detach --publish
mysql --host=127.0.0.1 --port=3306 --user=root --password=1234 sample
create table user ( id int, name varchar(32) );
insert into user ( id, name) values (1, 'John' );
insert into user ( id, name) values (2, 'Evan' );
select * from user;
```

=======
# ruby 관련 파일
- 파일명 : hello.rb

# 컨테이너 실행
```bash
docker container run \
--name ruby \
--rm \
--interactive \
--tty \
--mount type=bind,source="$(pwd)",destination=/my-work \
ruby:3.3.4 \
bash
```
>>>>>>> fc54a95007cb1646cf275d737e6a3bd1bff29f80
