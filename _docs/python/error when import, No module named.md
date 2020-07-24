---               
order: 15
title: (Python) error context must be a dict rather than set
category: Python
---

## Have to send data by using dic
```
data = db_search.get_user_info()
print(data)
    return render(request, "home.html", {'data':data})
```
