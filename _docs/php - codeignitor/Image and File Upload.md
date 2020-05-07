---
order: 4
title: (PHP-codeig) Image and File Upload
category: Php - codeignitor
---

Tutorial Scripts in detail
Below are the details of the code used in this tutorial with proper explanation.
View file for viewing complete form : file_view.php

<html>
<head>
<title>Upload Form</title>
</head>
<body>
<?php echo $error;?> <!-- Error Message will show up here -->
<?php echo form_open_multipart('upload_controller/do_upload');?>
<?php echo "<input type='file' name='userfile' size='20' />"; ?>
<?php echo "<input type='submit' name='submit' value='upload' /> ";?>
<?php echo "</form>"?>
</body>
</html>
 
Controller file : upload_controller.php
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Upload_Controller extends CI_Controller {
public function __construct() {
parent::__construct();
}
public function file_view(){
$this->load->view('file_view', array('error' => ' ' ));
}
public function do_upload(){
$config = array(
'upload_path' => "./uploads/",
'allowed_types' => "gif|jpg|png|jpeg|pdf",
'overwrite' => TRUE,
'max_size' => "2048000", // Can be set to particular file size , here it is 2 MB(2048 Kb)
'max_height' => "768",
'max_width' => "1024"
);
$this->load->library('upload', $config);
if($this->upload->do_upload())
{
$data = array('upload_data' => $this->upload->data());
$this->load->view('upload_success',$data);
}
else
{
$error = array('error' => $this->upload->display_errors());
$this->load->view('file_view', $error);
}
}
}
?>
Note : You can change preferences depending upon the file you wish to upload.
'allowed_types' => "gif|jpg|jpeg|png|iso|dmg|zip|rar|doc|docx|xls|xlsx|ppt|pptx|csv|ods|odt|odp|pdf|rtf|sxc|sxi|txt|exe|avi|mpeg|mp3|mp4|3gp",
 
View file to display success message : upload_success.php
<html>
<head>
<title>Upload File Specification</title>
</head>
<body>
<h3>Your file was successfully uploaded!</h3>
<!-- Uploaded file specification will show up here -->
<ul>
<?php foreach ($upload_data as $item => $value):?>
<li><?php echo $item;?>: <?php echo $value;?></li>
<?php endforeach; ?>
</ul>
<p><?php echo anchor('upload_controller/file_view', 'Upload Another File!'); ?></p>
</body>
</html>

