---
order: 41
title: (LINUX) creating Symbol link
category: Linux
---

ln -s <링크 대상 파일명> <링크 파일명>
ex) ln -s basefile symbollink
 symbollink -> basefile
 
심볼릭 링크는 단순히 원본 파일과 연결만 되는 것으로 윈도우의 바로가기 아이콘과 같은 기능을
하는 것이다.
심볼릭 링크의 경우 원본 파일이 원래 위치에서 삭제 되거나 이동되면 연결이 끊어지게 된다.
