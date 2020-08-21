---               
order: 10
title: (Python) Python rendering css, js - path
category: Python
---
### crypto is app home directory.

### 1. make a "static" folder
```
/home/django-apps/aaronapps/crypto/static
```

### 2. make css files and folder into the static folder

### 3. loading static in the html.(adding loading code)
```
{% load static %}
<link href="{% static 'vendor/fontawesome-free/css/all.min.css' %}" rel="stylesheet" type="text/css">
<script src="{% static 'js/demo/chart-area-demo.js' %}"></script>
```

### 2. adding in the setting.py
```
STATICFILES_DIRS =[
    "/home/django-apps/aaronapps/crypto/static",
]
```

