---
order: 5
title: (Javascript) bool isset 
category: Javascript
---

변수가 세트되어있으면서 NULL 이 아닌지를 체크하는 함수입니다.

변수가 존재하고 NULL 이 아닌 값을 가지고 있으면 TRUE를 리턴합니다.
그 외에는 FALSE를 리턴합니다.

unset()함수로 변수를 unset 시킨 후, isset()으로 확인하면, FALSE가 리턴되지요.

함수의 인자로 여러개의 변수를 줄 수 있는데, 이때는 모든 변수가 세트되어 있어야 TRUE를 리턴합니다.




unset() 함수

void unset ( mixed $var [, mixed $... ] )

