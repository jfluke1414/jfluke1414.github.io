---   
order: 5   
title: (LINUX) Kill -9   
category: Linux   
---   
   
kill -9 `ps -ef | grep -v grep | grep BatchInference | awk '{print $2}'`   
nohup $JAVA_HOME/bin/java $JAVA_OPT $MAIN_CLASS "117"  20101101 20101228 > ../logs/1.log &   
nohup $JAVA_HOME/bin/java $JAVA_OPT $MAIN_CLASS "116"  20101101 20101228 > ../logs/2.log &   
   
