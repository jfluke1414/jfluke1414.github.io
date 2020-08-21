---                  
order: 11   
title: (Python) Python templating   
category: Python   
---   
   
### Only extends is available only one time in the same html.   
reusing is available by extending templte

   
### 1. base.html   
```   
{% include 'head.html' %}   
   
{% block main_content %}   
{% endblock %}   
   
{% include 'footer.html' %}   
```   
   
