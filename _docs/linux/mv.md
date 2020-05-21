---   
order: 22   
title: (LINUX) mv   
category: Linux   
---   
   
### 1. 기능   
파일을 현재의 위치나 다른 디렉토리로 복사(copy)한다.    
   
### 2. 문법    
# cp [ 옵션 ] 파일명1 파일명2    
# cp [ 옵션 ] 파일명(들) 디렉토리    
   
### 3. 옵션    
-a : 가능한 한 원 파일의 구조와 속성을 그대로 복사한다.    
-b : 복사할 때 덮어쓰게 되는 파일은 백업을 만든다.    
-d : 심볼릭 링크는 심볼릭 링크로 복사한다. 그리고 원본 파일과의 하드 링크 관계를 유지한다.    
-f : 복사 위치에 존재하는 파일을 제거하고 복사한다.    
-i : 복사 시 같은 이름의 파일이 존재한다면 덮어쓸 것인가 확인한다.    
-I : 하드 링크를 만든다.    
-P : 원본 파일의 소유자, 그룹, 권한, 시간 기록을 그대로 복사한다.    
-R , -r : 파일과 하위 디렉토리에 포함된 파일 모두를 복사한다.    
-s : 디렉토리가 아닌 파일의 심볼릭 링크를 만든다. 소스 파일의 이름은 전체 경로 이름으로 한다. 목적지 파일 이름은 전체 경로를 주지 않아도 현재 디렉토리로 간주되므로 상관없다.    
-u : 파일의 정보를 갱신한다.    
-x : 다른 파일 시스템인 하위 디렉토리는 무시한다.    
   
### 4. 사용방법 및 정보   
가) 만일 파일명2가 이미 존재하는 파일의 이름이라면 기존에 있던 파일은 사라지고 새로운 복사본 파일로 바뀐다. 안전을 위해 i 옵션이 환경변수로 설정되어 있다. -i 옵션은 파일명2가 이미 존재하는 이름이라면 그대로 복사할 것인지 아닌지를 선택할 수 있게 물어온다.    
   
<shell>   
[root@sense ~]# cp file1 file2   
cp: overwrite `file2'? y   
</shell>   
   
나) 여러 파일을 한 번에 복사할 수도 있다.   
   
<shell>   
[root@sense ~]# mkdir copydirectory   
[root@sense ~]# cp file file1 file2 copydirectory/   
[root@sense ~]# ls copydirectory/   
file file1 file2   
</shell>   
   
다) ?r 옵션을 통해 하위 디렉토리의 파일까지 복사할 수 있다.   
   
<shell>   
[root@sense ~]# cp -r commands copydirectory/   
[root@sense ~]# ls copydirectory/   
anaconda-ks.cfg commands.html copydirectory docs file1   
commands commands index.html Desktop file file2   
[root@sense ~]#   
</shell>   
