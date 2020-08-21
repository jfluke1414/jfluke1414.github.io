---                  
order: 11   
title: (Python) Python templating   
category: Python   
---   
   
### Only extends is available only one time in the same html.   
reusing is available by extending templte

   
  
   
<!DOCTYPE html>   
<html lang="en">   
   
<head>   
   
  <meta charset="utf-8">   
  <meta http-equiv="X-UA-Compatible" content="IE=edge">   
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">   
  <meta name="description" content="">   
  <meta name="author" content="">   
   
  <title>Admin 2 - Dashboard</title>   
   
</head>   
   
<body id="page-top">   
```   
   
### 2. home.html   
{% extends 'base.html' %}   
   
{% block main_content %}   
```   
<div class="modal fade" id="logoutModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">   
    <div class="modal-dialog" role="document">   
      <div class="modal-content">   
        <div class="modal-header">   
          <h5 class="modal-title" id="exampleModalLabel">Ready to Leave?</h5>   
          <button class="close" type="button" data-dismiss="modal" aria-label="Close">   
            <span aria-hidden="true">¡¿</span>   
          </button>   
        </div>   
        <div class="modal-body">Select "Logout" below if you are ready to end your current session.</div>   
        <div class="modal-footer">   
          <button class="btn btn-secondary" type="button" data-dismiss="modal">Cancel</button>   
          <a class="btn btn-primary" href="login.html">Logout</a>   
        </div>   
      </div>   
    </div>   
  </div>   
{% endblock %}   
```   
   
### 2. footer.html   
```   
{% load static %}   
<!-- Bootstrap core JavaScript-->   
  <script src="{% static 'vendor/jquery/jquery.min.js' %}"></script>   
<!--  vendor/jquery/-->   
  <script src="{% static 'vendor/bootstrap/js/bootstrap.bundle.min.js' %}"></script>   
   
  <!-- Core plugin JavaScript-->   
  <script src="{% static 'vendor/jquery-easing/jquery.easing.min.js' %}"></script>   
   
  <!-- Custom scripts for all pages-->   
  <script src="{% static 'js/sb-admin-2.min.js' %}"></script>   
   
  <!-- Page level plugins -->   
  <script src="{% static 'vendor/chart.js/Chart.min.js' %}"></script>   
   
  <!-- Page level custom scripts -->   
  <script src="{% static 'js/demo/chart-area-demo.js' %}"></script>   
  <script src="{% static 'js/demo/chart-pie-demo.js' %}"></script>   
   
</body>   
   
</html>   
```