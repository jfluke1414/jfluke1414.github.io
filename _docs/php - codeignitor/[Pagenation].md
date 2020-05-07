---
order: 9
title: (PHP-codeig) [Pagenation]
category: Php - codeignitor
---

//controller
public function security_news()
	{
		$id = $this->input->get('list_id');
		$data['news_id'] = $id;
		$this->load->model('supports');

		$pagenum = $this->uri->segment(3, 1);	//페이지 번호
		$outcnt = '5';							//리스트 출력 갯수
		
		$params = array();
		$params['outcnt'] = $outcnt;
		$params['pagenum'] = $pagenum;
		$params['call'] = true;
		
		$result = $this->supports->news_list($params);
		$data['results'] = $result;
		
		$allcnt = $this->supports->news_count_all();
			
		$data['allcnt'] = $allcnt;
		$data['pagenum'] = $pagenum;
		$data['outcnt'] = $outcnt;
		
		$this->load->library('pagination');
		$config['base_url'] = base_url().'support/security_news';
		$config['total_rows'] = $allcnt;
		$config['per_page'] = $outcnt;
		$config['num_links'] = '5';
		$config['uri_segment'] = '3';
		$config['use_page_numbers'] = TRUE;
		
		$config['full_tag_open'] = '<div id="pagination">';
		$config['full_tag_close'] = '</div>';

		$config['prev_link'] = '<img src="/assets/img/icon_left.png" width="25" height="25" alt="" style="vertical-align: middle;">';
		$config['next_link'] = '<img src="/assets/img/icon_right.png" width="25" height="25" alt="" style="vertical-align: middle;">';

		$this->pagination->initialize($config);


		$this->load->view("security_news_view", $data);
		$this->_footer();
		
	}

//model
function faq_list($param)
    {
		$pagenum = $param['pagenum'];
		$outcnt = $param['outcnt'];
		
		$this->db->order_by("category", "desc");
    	$this->db->order_by("id", "desc");
		$this->db->limit($outcnt, ($pagenum-1)*$outcnt);
		$query = $this->db->get('faq');
		
        return $query->result();
    }
	
function faq_count_all() {
        return $this->db->count_all('faq');
    }

//view
<?
      echo $this->pagination->create_links();
?>
