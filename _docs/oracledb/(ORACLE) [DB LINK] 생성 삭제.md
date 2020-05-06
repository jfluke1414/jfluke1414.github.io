---
order: 25
title: [DB LINK] 생성 삭제
category: Oracledb
---

리눅스기준
$ORACLE_HOME/network/admin  의 위치에 tnsnames.ora 파일이 있습니다

db_alias =
  (DESCRIPTION =
          (ADDRESS = (PROTOCOL = TCP)(HOST = 접속하려는곳주소)(PORT = 1521))
                     (CONNECT_DATA =
               (SERVER = DEDICATED)
       (SERVICE_NAME = 접속대상DB의 SID)
                             )  
                         )
 
db_alias 를 testdb2 로 지정하고 접속할주소는 testdb2.com 이며 해당 db SID가 orcl 이라면
아래와같이 추가 해주면 됩니다

testdb2=
  (DESCRIPTION =
          (ADDRESS = (PROTOCOL = TCP)(HOST = testdb2.com)(PORT = 1521))
                     (CONNECT_DATA =
               (SERVER = DEDICATED)
       (SERVICE_NAME = orcl)
                             )  
                         )


DB LINK 생성
  CREATE [PUBLIC] DATABASE LINK link_name
         [CONNECT TO CURRENT_USER]
         [USING 'connect_string']
      

CREATE DATABASE LINK 링크이름
CONNECT TO <연결하고자 하는 user> 
IDENTIFIED BY <연결하고자 하는 user password>
USING '원격 db alias'
 
이렇게 생성하면 생성한 유저만 이용이 가능하며 동일한데

아래와 같이 public 옵션이 들어가면 누구나 이용 가능하게 된다.
CREATE PUBLIC DATABASE LINK 링크이름
CONNECT TO <연결하고자 하는 user> 
IDENTIFIED BY <연결하고자 하는 user password>
USING '원격 db alias'


삭제 할 때 에도 생성된 형태에 따라 삭제 방법이 약간 다릅니다
누구나 사용이 가능한 public 형태로 존재 한다면

drop public database link db_link이름;
생성된 사용자만 이용 가능한 private 하게 되어있다면 해당유저로 접속해서
drop database link db_link이름;           하면 됩니다

일반유저가 Private DB LINK 생성권한 부여
grant create database link to 유저명;
 
public 으로 생성 할 수 있는 권한 부여
grant create public database link to 유저명;
  
dba_db_links dictionary 에서 자세한 내용 조회 가능합니다
select * from dba_db_links;

간단한 사용법은 
select 컬럼명 from 테이블명@db_link명
