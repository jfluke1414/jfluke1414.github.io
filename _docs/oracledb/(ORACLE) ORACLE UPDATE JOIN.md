---
title: (ORACLE) ORACLE UPDATE JOIN
category: Oracledb
order: 14
---

oracle 에서 두테이블 join을 이용한 update
 
UPDATE AA
set c = ( select c 
          from BB
          where AA.a = 1
          and AA.b = 10
          and BB.a = AA.a
          and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
위와 같은 문장은 SET절에 쓰이는 서브쿼리와는 상관없이
WHERE 절에 해당하는 AA.a = 1 AND AA.b = 10 인 자료는 모두 업데이트 하는 것입니다.
업데이트의 기준은 어디까지나 WHERE 절이라는 거죠..
그러다 보니 SET절의 서브쿼리에 맞는 데이터가 없으면 Null값으로 업데이트를 하게 됩니다.
 
일단은 위의 문장에서 불필요한 부분을 지적하고 싶군요..
SET절의 서브쿼리에서 AA 테이블과 관련된 조건은 불필요합니다.
이미 메인쿼리의 WHERE절에서 제한을 하고 있기때문이죠..
글구 SET절의 서브쿼리에서 C컬럼에 대한 정의가 불분명하군요..
이런 사항을 고쳐보면..
 
UPDATE AA
set c = ( select BB.c 
          from BB
          where BB.a = AA.a
          and   BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
이 되겠죠..

1)가장 쉽게 바꾸는 방법은 NVL처리를 해주는 것입니다. 
윗분처럼 안쪽에서 하는 방법은 의미없고 바깥쪽에서 해주어야 합니다.
 
UPDATE AA
set c = NVL(select BB.c 
            from BB
            where BB.a = AA.a
            and BB.b < AA.b ), AA.c)
where AA.a = 1
and AA.b   = 10;
 
같은 맥락으로 Group 함수를 취한 후에 NVL처리를 해도 됩니다.
UPDATE AA
set c = (select NVL(MAX(BB.c), AA.c) 
         from BB
         where BB.a = AA.a
         and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
그러나 위의 문장은 자료에는 이상이 없겠지만, 
서브쿼리에서의 조인에 해당하지 않는 값에 대해 
불필요한 업데이트가 발생한다는 것입니다.
비효율적이죠..
 
2)두번째 방법은 EXISTS 체크조건을 주는 것입니다.
SET절과 같은 방법으로 체크조건을 주어 WHERE절의 해당 데이터를
한정하는 것이죠..
 
UPDATE AA
set c = ( select BB.c 
          from BB
          where BB.a = AA.a
          and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10
AND EXISTS
   (select 'X' 
    from BB
    where BB.a = AA.a
    and BB.b < AA.b )
    
그러나 이것은 BB 테이블을 중복하여 엑세스하는 단점이 있죠..
두번 읽을 수 밖에 없다는 거죠..
 
3) 세번째 방법은 수정가능조인뷰를 이용하는 방법입니다.
UPDATE ( select AA.C AA_C,
                BB.c BB_C
          from AA, BB
          where AA.a = 1
          and AA.b = 10
          and BB.a = AA.a
          and BB.b < AA.b )
SET AA_C = BB_C
 
이 방법이 가장 효율적입니다.
불필요한 업데이트로 발생하지 않으며, 중복처리도 없습니다.
위의 뷰를 실제 뷰로 만들어도 결과는 같습니다.
 
위의 모든 내용은 처음의 SET절에 있는 서브쿼리가 하나 이하의 값을 
리턴해야 한다는 전제가 있는 건 당연한 얘기겠죠..
 
자세한 내용은 대용량데이터베이스솔루션 2권의 
제1장 SQL의 활용 에서 3.3. UPDATE의 활용 을 참고하시기 바랍니다.


oracle 에서 두테이블 join을 이용한 update
 
UPDATE AA
set c = ( select c 
          from BB
          where AA.a = 1
          and AA.b = 10
          and BB.a = AA.a
          and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
위와 같은 문장은 SET절에 쓰이는 서브쿼리와는 상관없이
WHERE 절에 해당하는 AA.a = 1 AND AA.b = 10 인 자료는 모두 업데이트 하는 것입니다.
업데이트의 기준은 어디까지나 WHERE 절이라는 거죠..
그러다 보니 SET절의 서브쿼리에 맞는 데이터가 없으면 Null값으로 업데이트를 하게 됩니다.
 
일단은 위의 문장에서 불필요한 부분을 지적하고 싶군요..
SET절의 서브쿼리에서 AA 테이블과 관련된 조건은 불필요합니다.
이미 메인쿼리의 WHERE절에서 제한을 하고 있기때문이죠..
글구 SET절의 서브쿼리에서 C컬럼에 대한 정의가 불분명하군요..
이런 사항을 고쳐보면..
 
UPDATE AA
set c = ( select BB.c 
          from BB
          where BB.a = AA.a
          and   BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
이 되겠죠..

1)가장 쉽게 바꾸는 방법은 NVL처리를 해주는 것입니다. 
윗분처럼 안쪽에서 하는 방법은 의미없고 바깥쪽에서 해주어야 합니다.
 
UPDATE AA
set c = NVL(select BB.c 
            from BB
            where BB.a = AA.a
            and BB.b < AA.b ), AA.c)
where AA.a = 1
and AA.b   = 10;
 
같은 맥락으로 Group 함수를 취한 후에 NVL처리를 해도 됩니다.
UPDATE AA
set c = (select NVL(MAX(BB.c), AA.c) 
         from BB
         where BB.a = AA.a
         and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10;
 
그러나 위의 문장은 자료에는 이상이 없겠지만, 
서브쿼리에서의 조인에 해당하지 않는 값에 대해 
불필요한 업데이트가 발생한다는 것입니다.
비효율적이죠..
 
2)두번째 방법은 EXISTS 체크조건을 주는 것입니다.
SET절과 같은 방법으로 체크조건을 주어 WHERE절의 해당 데이터를
한정하는 것이죠..
 
UPDATE AA
set c = ( select BB.c 
          from BB
          where BB.a = AA.a
          and BB.b < AA.b )
where AA.a = 1
and AA.b   = 10
AND EXISTS
   (select 'X' 
    from BB
    where BB.a = AA.a
    and BB.b < AA.b )
    
그러나 이것은 BB 테이블을 중복하여 엑세스하는 단점이 있죠..
두번 읽을 수 밖에 없다는 거죠..
 
3) 세번째 방법은 수정가능조인뷰를 이용하는 방법입니다.
UPDATE ( select AA.C AA_C,
                BB.c BB_C
          from AA, BB
          where AA.a = 1
          and AA.b = 10
          and BB.a = AA.a
          and BB.b < AA.b )
SET AA_C = BB_C
 
이 방법이 가장 효율적입니다.
불필요한 업데이트로 발생하지 않으며, 중복처리도 없습니다.
위의 뷰를 실제 뷰로 만들어도 결과는 같습니다.
 
위의 모든 내용은 처음의 SET절에 있는 서브쿼리가 하나 이하의 값을 
리턴해야 한다는 전제가 있는 건 당연한 얘기겠죠..
 
자세한 내용은 대용량데이터베이스솔루션 2권의 
제1장 SQL의 활용 에서 3.3. UPDATE의 활용 을 참고하시기 바랍니다.

출처 : http://cafe.naver.com/sanovice/14 
방식1)
update
(select a.a a1, a.b a2, a.c a3,
b.a b1, b.b b2, b.c b3
from target a, dest b
where a.x = b.x and a.y = b.y)
set
a1 = b1, a2 = b2, a3 = b3;

방식2)
update target a
set a.a = (select a from dest 
where x = a.x and y = a.y) ;
 
update cmt_loca_ma set cmt_loca_ma.SiteGubun = (select Site_Gubun from SiteTemp where site_code = cmt_loca_ma.lot_cde)
 
update cmt_flot_ma set cmt_flot_ma.use_yn = (select use_yn from cmt_flot_ma3 where cmt_flot_ma3.usr_idn = cmt_flot_ma.usr_idn and cmt_flot_ma3.lot_cde = cmt_flot_ma.lot_cde)
<----반드시 범위가 작은것을 기준으로 연결해야함(범위가 작은것이 왼쪽) -> 대단히 중요
