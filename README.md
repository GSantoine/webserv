# Webserv - A fully configurable HTTP/1.1 web server in C++, inspired by Nginx

### Notions explored
UNIX sockets, interaction with TCP, HTTP requests parsing, HTTP response building, requests polling, I/O buffers, even-driven and fault-tolerance design, CGI implementation.

|    Project Name    |                                                                       webserv                                                                      |
| :----------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------: |
|    Description     |       	A fully configurable home-made web server in C++ (following HTTP/1.1 RFC)                                       |
|    Technologies    |  <img alt="C++" src="https://custom-icon-badges.demolab.com/badge/C++-9C033A.svg?logo=cpp2&logoColor=white"> <img alt="PHP" src="https://img.shields.io/badge/PHP-777BB4.svg?logo=php&logoColor=white"> <img alt="HTML" src="https://img.shields.io/badge/HTML-E34F26.svg?logo=html5&logoColor=white"> |


## Usage

### Installation:
```bash
  git clone https://github.com/GSantoine/webserv.git
  cd webserv
  make
  ./webserv <CONFIG FILE> (you can use by default the example config file : config_files/default.conf)
```

You can now access it on your browser on the ip and port specified in the config file you launched the server with

### Server config file
You can configure you server by modifying the config file it runs with (config files structure and rules are very much inspired by Nginx)<br>
Here is an example of a config file :
```
server {
	listen: 127.0.0.1:8080
	server_name:example.com
	client_max_body_size : 1000000
	index: index.html
	error_page: 404 /error_pages/404.html
	root : html
	allowed_methods: GET POST

	location /assets/ {
		autoindex:on
	}

	location /error_pages/ {
		autoindex:on
		root:html_test_root
	}

	location /test {
		rewrite: 302 /
	}

	location /assets/uploaded_files/totoro.jpg {
		allowed_methods: DELETE
	}
}

server {
	listen: 127.0.0.1:8081
	server_name:agras.com
	root: html_test_root
	index:index.html
	
}

server {
	listen: 127.0.0.1:8081
	server_name:agras.com
	index:index.html
}


server {
	listen: 127.0.0.1:8082
	server_name:agras.com
	autoindex:on
}
```
