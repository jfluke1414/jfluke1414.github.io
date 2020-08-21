---                  
order: 11   
title: (Python) Python templating   
category: Python   
---   
   
### Only extends is available only one time in the same html.   
템플릿 확장을 통해 재활용이 가능하다   
   
### 1. base.html   
```   
{% include 'head.html' %}   
   
{% block main_content %}   
{% endblock %}   
   
{% include 'footer.html' %}   
```   
   
