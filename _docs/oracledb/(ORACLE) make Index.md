---
order: 35
title: (ORACLE) Make index
category: Oracledb
---

CREATE INDEX RCH20.IDX_RSS_CURL_1
ON RCH20.TB_ARTICLE_SEARCH_RSS_1
(
	URL ASC
)
NOLOGGING
NOCOMPRESS
NOPARALLEL ;
