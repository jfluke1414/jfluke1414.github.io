---
title: Oracle hashcode 적용
category: Oracledb
order: 12
---

SELECT * FROM TB_CRAWL_SITE 
WHERE PRIORITY = 1 AND SITE_TYPE IN ( 'T','R' )
ORDER BY DBMS_UTILITY.GET_HASH_VALUE(URL, 2,1048576)


Tb_crawl_site 타입에 상관없이 골고루 분산하기 위해 사용
