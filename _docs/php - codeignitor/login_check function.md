---
order: 1
title: login_check function
category: Php - codeignitor
---

function login_check($ecryp_pw)
    {

		$username = $this->security->xss_clean($this->input->post('username'));
		$password = $this->security->xss_clean($this->input->post('userpwd'));
		
		if(empty($username) || empty($password))
			return false;
		
		$this->db->where('id', $username);
		$this->db->where('pw', $ecryp_pw);		
		
		$query = $this->db->get('admin');

		if($query->num_rows == 1)
		{
			$row = $query->row();
			$data = array(
					'isadmin' => true,
					'admin_id' => $row->id,
					'admin_name' => $row->name,
					'admin_phone' => $row->phone,
					'admin_email' => $row->email,
					'admin_usertype' => $row->usertype
					);
			$this->session->set_userdata($data);
			return true;
		}
		return false;
    }


