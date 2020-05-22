---      
order: 3      
title: (Python) try & except
category: Python      
---      
      
```    
try:
    age = int(input('Age : '))
    print(age)
except ZeroValueError:
    print('Age cannot be 0')
except ValueError:
    print('invalid value')
```   
   
