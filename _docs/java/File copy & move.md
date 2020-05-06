---
order: 13
title: File copy & move
category: Java
---

자바에서 파일을 복사 하기 위해서는 Spring 프레임워크의 StringUtil을 이용하면 간단하다
import org.springframework.util.FileCopyUtils;
    
     in = new File(tempPath, fileName);
    dir = new File(realPath+contentsSeq);
    dir.mkdirs();
    out = new File(realPath+contentsSeq, fileName);
    FileCopyUtils.copy(in, out);

자바에서 파일을 이동하기 위해서는 자바에서의 renameTo를 이용하는 파일 이름을 변경 뿐만 아니라 이동도 가능하다.
import java.io.*; 
    
     in = new File(tempPath, fileName);
    dir = new File(realPath+contentsSeq);
    dir.mkdirs();
    out = new File(realPath+contentsSeq, fileName);
    in.renameTo(out);

