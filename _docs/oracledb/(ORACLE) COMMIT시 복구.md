---
order: 38
title: (ORACLE) COMMIT시 복구
category: Oracledb
---

대용량 데이터 및 시간이 오래 지날 경우 복구 되지 않음.
 
(SELECT site_id, site_category FROM TB_CRAWL_SITE AS OF timestamp(systimestamp -interval '20' minute) b WHERE site_type = 'M')
