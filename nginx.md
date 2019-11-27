### log formating for nginx X

log_format combined_plus_rt '$remote_addr - $remote_user [$time_local]'
                                 '"$request" $status $body_bytes_sent '
                                 '"$http_referer""$http_user_agent" $request_time' ;


                                 