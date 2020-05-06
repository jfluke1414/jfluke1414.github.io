---
order: 17
title: Get current timestamp
category: Php
---

//$date2 = new DateTime('now', new DateTimeZone('ICT'));
$date2 = new DateTime();				
$this->logger->debug("ttt".$date2->getTimeStamp());
