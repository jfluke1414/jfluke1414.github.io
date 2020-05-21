---   
order: 32   
title: (LINUX) profile  bashrc  bash_profile  inputrc   
category: Linux   
---   
   
/etc/profile            시스템 규모의 환경 설정과 시작 프로그램들   
                        (쉘이 시작할 때 제일 먼저 읽는 파일임)   
   
/etc/bashrc             시스템 규모의 alias와 함수 - bash 셀 설정   
   
/etc/inputrc            시스템 규모의 키 결정(binding)과 기타 내용   
   
$HOME/.bash_profile     사용자 환경 설정과 시작 프로그램들 - bash 셀 설정   
   
$HOME/.bashrc           사용자 alias와 함수들 - bash 셀 설정   
   
$HOME/.inputrc          키 결정(binding)과 기타 내용들    
   
   
etc/ 디렉토리 밑에 있는 것은, 모든 사용자에게 적용되고   
   
home/<로그인ID>/ 디렉토리 밑의 설정 파일들은, 현재 로그인한 사용자에게만 개별적으로 적용되는 것입니다.   
