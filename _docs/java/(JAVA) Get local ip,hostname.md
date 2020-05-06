---
order: 9
title: Get local ip,hostname
category: Java
---

public class Print{
  public static void main(String[] args){
    try{
      System.out.println( InetAddress.getLocalHost().getHostName() );
      System.out.println( InetAddress.getLocalHost().getHostAddress() );
    }
    catch( UnknownHostException e ){
      e.printStackTrace();
    }
  }
}
