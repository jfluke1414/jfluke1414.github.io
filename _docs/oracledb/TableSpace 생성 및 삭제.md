---
order: 26
title: TableSpace 생성 및 삭제
category: Oracledb
---

1. Tablespace 생성
SQL> create tablespace [테이블 스페이스 이름] datafile [저장될 경로\파일이름.ora] size [용량]m;

우리 회사의 경우, 2기가를 기본으로 사용하며 테이블 스페이스의 자동용량증가라거나 그러한 옵션을 절대 사용하지 않기 때문에 여기까지.

또한, 테이블 스페이스를 추가하는 방법은 아래와 같다.

2. Tablespace 추가
SQL> alter tablespace [테이블 스페이스 이름] add datafile [저장될 경로\파일이름.ora] size [용량]m;

이러한 방법으로 가능하다.

3. Tablespace 삭제
삭제방법은 약간 까다로운데, 나같은 경우엔 잘못된 이름지정으로 삭제를 하였다. 다른 경우에는 뭐 어찌될 지 모르겠다.

SQL> drop tablespace [테이블 스페이스 이름]
그런데 때때로 데이터가 들어있는 이유나 그 외 이유로 테이블스페이스가 삭제되지 않는 경우도 있다.
그럴 땐 아래와같이 입력해보자.

SQL> drop tablespace [테이블 스페이스 이름] including contents and datafiles;
이 명령어는 무조건 다 삭제한다.
