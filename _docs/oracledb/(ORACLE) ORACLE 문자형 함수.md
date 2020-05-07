---
title: (ORACLE) ORACLE 문자형 함수
category: Oracledb
order: 13
---

1) 문자형 함수 

LOWER             모든 문자를 소문자로
더보기
UPPER              모든 문자를 대문자로
더보기
INITCAP            첫 글자는 대문자,나머지는 소문자로
CANCAT            첫 번째 문자와 두 번째 문자를 연결
더보기
SUBSTR            문자의 길이를 리턴할 때
LENGTH            문자의 길이를 리턴할 때
NVL                  널값을 다른 값으로 대체할 때
NVL2                조건에 의해 널값을 다른 값으로 대체할 때
더보기

SUBSTR            특정 문자의 문자열중 필요 부분만 선별하여 사용
더보기

RTRIM               서브 스트림의 정확한 위치와 길이를 요구(오른쪽)
더보기

LTRIM               서브 스트림의 정확한 위치와 길이를 요구(왼쪽)
RPAD                문자열을 제외한 공간에 지정한 문자열로 대체(오른쪽)
더보기

LPAD                문자열을 제외한 공간에 지정한 문자열로 대체(왼쪽)
TRANSLATE       첫 문자는 탐색집합의 첫 문자로 대체(2번째도 동일)
REPLACE          특정 문자열을 다른 문자열로 대체
더보기

SOUNDX            같은 단어 또는 유사한 사운드 단어를 음성학적으로
LENGTH            문자의 실제 길이를 변환할 때
LENGTHB          문자열의 실제 길이를 변환할 때
INTSTR             문자열 내의 특정 스트림의 위치
NULLIF             조건이 같으면 NULL,다르면 지정된 값을 리턴할 때
더보기

COALESCE       조건에 따라 여러 가지 값을 리턴할 때

2. 시스템 함수

USER               현재 DB 사용자
USERID            현재 DB 사용자에게 할당되는 사용자번호

3. 숫자형 함수

ROUND             해당 소수점 자리에서 반올림할 때
TRUNC             해당 소수점 자리에서 절삭할 때
MOD(m/n)        m을 n으로 나누고 남은 나머지를 리턴할 때
ABS                 숫자 값을 절대값으로 바꾼다
SIGN                숫자가 양수:+1, 음수:-1, 0:0
FLOOR             실수값을 정수값으로
CEIL                그 수보다 가장 크거나 작은값을 리턴
POWER            해당 수에 대한 지수값을 표현
LOG                로그값으로 변환
SIN                  SIN값
COS                COS값
TAN                 TAN값


4. 날짜형 함수

SYSDATE         현재 시스템 날짜를 보여줄 때
ADD_MONTHS   지정한 날짜에 몇 월을 추가한 결과의 월을 계산할 때
LAST_DAY        해당 월의 마지막 날짜를 알고자 할 때
NEW_TIME        해당 표준시로 시간을 변환할 때
NEXT_DAY        해당 날짜의 다음 지정한 날짜로 현환할 때
NONTH_BETWEEN   지정된 월 간의 월수를 알고자 할 때

더보기

5. 변환 함수

TO_CHAR       숫자,날짜 타입의 Data를 varchar2타입으로 변환
TO_NUMBER   숫자를 포함하는 문자 String을 number 타입으로 변환
TO_DATE        문자 String을 날짜 타입으로 변환
