---
categories: software
tags: [devOps] 	
---

# process and sockect
![nginx_process](/assets/img/nginx_process.png)

# source code

main (core/nginx.c)
	ngx_init_cycle (core/ngx_cycle.c) : start a firing of nginx
	    ngx_conf_parse(core/ngx_conf.file.c): parse conf,
	    events|http|mail|imap   
	
	ngx_event_accept(event/ngx_event_accept.c):handle event with ngx_connection_t
		ngx_http_init_request : handle request with ngx_http_request_t
		   ngx_http_process_request_line
		   ngx_http_read_client_request_body: request body handled by proxy ,fastcgi,uwsgi 
		  