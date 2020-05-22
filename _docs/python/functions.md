---   
order: 1   
title: (Python) Functions   
category: Python   
---   
   
```
def greet_user();   
    print('Hi there')   
    print('Welcome abroad');   
   
   
print('Start')   
greet_user();   
print('Finish')   
   
***   
   
def greet_user(first_name, last_name):   
    print(f'Hi {first_name}, {last_name}!')   
    print('welcome abroad')   
   
greet_user("smith", "John");   
greet_user(last_name="John", first_name="smith");   
greet_user("smith", first_name="John ")   
   
priority   
do not use keyword argument first and position argument second like it below   
greet_user(last_name="John", "smith");   
   
***   
   
def square(number):   
    result = number * number   
    return result   

```