---   
order: 65   
title: (LINUX) date 명령어를 이용하여 날짜 format 추출하기   
category: Linux   
---   
   
 %%     a literal %   
       %a     locale's abbreviated weekday name (Sun..Sat)   
       %A     locale's full weekday name, variable length (Sunday..Saturday)   
       %b     locale's abbreviated month name (Jan..Dec)   
       %B     locale's full month name, variable length (January..December)   
       %c     locale's date and time (Sat Nov 04 12:02:33 EST 1989)   
       %C     century (year divided by 100 and truncated to an integer) [00-99]   
       %d     day of month (01..31)   
       %D     date (mm/dd/yy)   
       %e     day of month, blank padded ( 1..31)   
       %F     same as %Y-%m-%d   
       %g     the 2-digit year corresponding to the %V week number   
       %G     the 4-digit year corresponding to the %V week number   
       %h     same as %b   
       %H     hour (00..23)   
       %I     hour (01..12)   
       %j     day of year (001..366)   
       %w     day of week (0..6);  0 represents Sunday   
       %W     week number of year with Monday as first day of week (00..53)   
       %x     locale's date representation (mm/dd/yy)   
       %X     locale's time representation (%H:%M:%S)   
       %y     last two digits of year (00..99)   
       %Y     year (1970...)   
       %z     RFC-2822 style numeric timezone (-0500) (a nonstandard extension)   
       %Z     time zone (e.g., EDT), or nothing if no time zone is determinable   
       By default, date pads numeric fields with  zeroes.   GNU  date  recognizes  the  following  modifiers   
       between '%' and a numeric directive.   
              '-' (hyphen) do not pad the field '_' (underscore) pad the field with spaces   
### [sample]   
```
# date '+%Y %m %d'   
2009 03 13   
# date +'%H:%M:%S'   
10:33:09   
# date +'%F %X' -d tomorrow            
2009-03-14 10:39:42 AM   
# date +'%F %X' -d yesterday   
2009-03-12 10:40:02 AM   
# date +'%F %X' -d today       
2009-03-13 10:40:20 AM   
# date +'%F %X' -d '3 days ago'   
2009-03-10 10:41:36 AM   
# date +'%F %X' -d '+3 days'   
2009-03-16 10:42:38 AM   
# date +'%F %X' -d '-3 days'   
2009-03-10 10:42:42 AM   
```