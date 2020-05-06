---
order: 14
title: (PHP) Array sort 정렬(Date, size)
category: Php
---

function array_sort($array, $on, $order=SORT_ASC)
	{
	    $new_array = array();
	    $sortable_array = array();

	    foreach ($array as $k => $v) {
			if (is_array($v)) {
				foreach ($v as $k2 => $v2) {
					if ($k2 == $on) {						      
		      	    $sortable_array[$k] = $v2;
		       		}
				}
			} else {
				$sortable_array[$k] = $v;
			}		  
	    }
	    switch ($order) {
	        case SORT_ASC:
	            asort($sortable_array);                   
	        break;
	        case SORT_DESC:
	            arsort($sortable_array);
	        break;
	    }
	    foreach ($sortable_array as $k => $v) {
	        $new_array[$k] = $array[$k];
	    }
	    return $new_array;
	}
	
	다른 function에서 호출해서 사용 something like it
	if( $this->sort == '-name' ){				
		rsort($dirs);
		rsort($files);
	} else if( $this->sort == '+datetime' ){
		$files = $this->array_sort($content['files'], 'datetime');
	} else if( $this->sort == '-datetime' ){				
		$files = $this->array_sort($content['files'], 'datetime', SORT_DESC);
	} else if( $this->sort == '+size' ){
		$files = $this->array_sort($content['files'], 'size');
	} else if( $this->sort == '-size' ){				
		$files = $this->array_sort($content['files'], 'size', SORT_DESC);
	} else {
		sort($dirs);
		sort($files);
	}
