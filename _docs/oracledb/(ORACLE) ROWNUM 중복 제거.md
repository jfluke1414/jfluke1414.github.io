---
title: ROWNUM 중복 제거
category: Oracledb
order: 17
---

기본키(primary) 가 없는 상태에서 중복되는 데이터가 있을경우 

나중에 들어온 중복 데이터 삭제하기. 

DELETE FROM 테이블 A
          WHERE ROWID > (SELECT MIN(ROWID) 
                                       FROM 테이블 B
                                      WHERE A.컬럼 = B.컬럼

먼저 들어온 중복 데이터 삭제하기

DELETE FROM 테이블 A
          WHERE ROWID < (SELECT MAX(ROWID) 
                                       FROM 테이블 B
                                      WHERE A.컬럼 = B.컬럼 

------------------------------------------------------------------

DELETE FROM TB_ARTICLE_MASTER A WHERE ROWID > (SELECT MIN(ROWID) 
FROM TB_ARTICLE_MASTER B
WHERE A.CONTENT_ID = B.CONTENT_ID
AND B.CONTENT_ID in ( )

------------------------------------------------------------------

-- RSS ADDRESS 중복 체크 --
SELECT *
FROM(
SELECT URL, COUNT(*) CNT
FROM TB_CRAWL_SITE
WHERE SITE_TYPE ='R'
GROUP BY URL 
)
WHERE CNT > 1;




DELETE FROM TB_CRAWL_SITE A WHERE ROWID > (SELECT MIN(ROWID) 
FROM TB_CRAWL_SITE B
WHERE A.URL = B.URL

AND B.URL in ( )
