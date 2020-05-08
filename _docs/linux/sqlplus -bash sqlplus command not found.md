---
order: 45
title: (LINUX) sqlplus -bash sqlplus command not found
category: Linux
---

sqlplus -bash: sqlplus: command not found


Export , path를 다 잘 잡아줘야 한다. 아래처럼

PATH=$PATH:$HOME/bin
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

export ORACLE_BASE=/home/oracle/app/oracle
export ORACLE_HOME=/home/oracle/app/oracle/product/11.2.0/dbhome_1
export ORACLE_SID=orcl


# User specific environment and startup programs

PATH=$PATH:$HOME/bin:$ORACLE_HOME/bin:/sbin
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib


export PATH

alias cdhome='cd /home/oracle/app/oracle/product/11.2.0/dbhome_1'
~

