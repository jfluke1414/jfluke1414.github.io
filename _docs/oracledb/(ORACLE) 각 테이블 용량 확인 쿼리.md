---
order: 39
title: (ORACLE) 각 테이블 용량 확인 쿼리
category: Oracledb
---

1. 먼저  analyze 한번도 하지 않은 테이블이라면 실행해줘야 한다.
2. 테이블 단위
analyze table 테이블명 compute statistics;
계정 단위
Exec dbms_utility.analyze_schema('SCOTT','COMPUTE')

3. 각 테이블 용량 추출 쿼리
select 
        table_name, 
        num_rows,
        num_rows * avg_row_len, 
        round((num_rows * avg_row_len/1024/1024),2) "SIZE(Mb)", 
        round((num_rows * avg_row_len/1024/1024/1024),2) "SIZE(Gb)",
        last_analyzed
from user_tables
order by TABLE_NAME


