FROM nginx:latest

MAINTAINER KeepWalking86

ADD ./default.conf /etc/nginx/conf.d/
RUN mkdir -p /var/www/example/
#ADD ./src /var/www/example/public/
RUN chown -R nginx:nginx /var/www/example

#Install net tools
RUN apt-get update
RUN apt-get install net-tools lsof -y

#Change nginx uid & gid
RUN usermod -u 1000 nginx && groupmod -g 1000 nginx

##Clearing the apt-get caches
RUN apt-get clean

## Expose ports
EXPOSE 80

server {
        listen 80;
	        listen [::]:80 ipv6only=on;

		    # Log files for Debugging
		            access_log /var/log/nginx/laravel-access.log;
			            error_log /var/log/nginx/laravel-error.log;

				        # Webroot Directory for Laravel project
					        root /var/www/example/public;
						        index index.php index.html index.htm;

							        # Your Domain Name
								        server_name example.local;
									        location ~* \.(jpg|jpeg|gif|css|png|js|ico|txt|srt|swf|zip|rar|html|htm|pdf)$ {
										                access_log        off;
												                log_not_found     off;
														                expires 30d; # caching, expire after 30 days
																        }

																	        location / {
																		                try_files $uri $uri/ /index.php?$query_string;
																				        }

																					    # PHP-FPM Configuration Nginx
																					            location ~ \.php$ {
																						                    try_files $uri =404;
																								                    fastcgi_split_path_info ^(.+\.php)(/.+)$;
																										                    #fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
																												                    fastcgi_index index.php;
																														                    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
																																                    include fastcgi_params;
																																		                    fastcgi_pass php-fpm:9000;
																																				            }
																																					    }
