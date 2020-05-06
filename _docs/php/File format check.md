---
order: 8
title: (PHP) File format check
category: Php
---

//add, ext_check
//		$point = strrpos($fileName, '.');
//		$format_a = substr($fileName, $point);
//		$file_ext = substr($format_a, 1);
//		
//		$env = $this->EnvTbl->getData();
//		
//		$ext_Array = explode(",", $env['file_ext']);
//		
//		if (!in_array($file_ext, $ext_Array)){
//			$this->error('Disk quota limit exceeded.');
//			$result['success'] = false;
//			$result['all'] = "Failed to save uploaded file.";
//			$result['name'] = $fileName;
//			$result['size'] = $file_size;
//			$result['sizeText'] = $this->DiskFile->convertFileSize($file_size);
//			$this->set('result', $result);
//			return;
//		}
