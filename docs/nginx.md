# Nginx usage

## Self-Compule Nginx with RTMP Module
```
./auto/configure --add-module=../nginx-rtmp-module \
--with-cc-opt='-g -O2  -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' \
--with-ld-opt='-Wl,-z,relro -Wl,-z,now -fPIC'     --with-compat --with-debug --with-pcre-jit \
--with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module \
--with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module \
--with-http_gunzip_module --with-http_gzip_static_module --with-http_sub_module \
--with-stream=dynamic --with-http_geoip_module=dynamic --with-stream_geoip_module=dynamic --with-http_image_filter_module=dynamic \
--with-http_xslt_module=dynamic --with-mail=dynamic
```
There may be some compule error relate with *__DATE_TIME\_\_*, add CCFLAG option *-Wno-error=date-time* in objs/Makefile manually and try again.

## Nginx rtml/hls server config sample
```
rtmp { 
    server { 
        listen 1935; 
        application live { 
            live on; 
            interleave on;
 
            hls on;  
            hls_path /tmp/hls; 
            hls_fragment 15s; 
        } 
    } 
}

http {
    #some other http config
    server {
    #some other server config

	location /live { 
		types {
			application/vnd.apple.mpegurl m3u8;
			video/mp2t ts;
			text/html html;
		} 
		alias /tmp/hls; 
		add_header Cache-Control no-cache;
		add_header 'Access-Control-Allow-Origin' '*';
	    }
    }
    #some other server config
}
```
**hls_path** should match with **location /live** alias path in server config. The current user shoud have previlege to read/write the path.    
Stream play url:   
http://192.168.72.20:8080/live/bbb.m3u8  
rtmp://192.168.72.20/live/bbb