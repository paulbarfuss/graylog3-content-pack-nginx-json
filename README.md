### Configuring nginx

You need to run at least nginx version 1.11.8, escaped JSON support.

**Add this to your nginx configuration file and restart the service:**

        log_format graylog2_json escape=json '{ "timestamp": "$time_iso8601", '
                         '"remote_addr": "$remote_addr", '
                         '"body_bytes_sent": $body_bytes_sent, '
                         '"request_time": $request_time, '
                         '"response_status": $status, '
                         '"request": "$request", '
                         '"request_method": "$request_method", '
                         '"host": "$host",'
                         '"upstream_cache_status": "$upstream_cache_status",'
                         '"upstream_addr": "$upstream_addr",'
                         '"http_x_forwarded_for": "$http_x_forwarded_for",'
                         '"http_referrer": "$http_referer", '
                         '"http_user_agent": "$http_user_agent" }';

    # replace the hostnames with the IP or hostname of your Graylog2 server
    access_log syslog:server=graylog.server.org:12301 graylog2_json;
    error_log syslog:server=graylog.server.org:12302;
