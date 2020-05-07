---
order: 2
title: (PHP-codeig) _header()
category: Php - codeignitor
---

_header()
	$this->load->model('Menu');
	$parents = $this->Menu->GetData();
	$child = $this->Menu->GetParent();
	$data['parents'] = $parents;
	$data['child'] = $child;
