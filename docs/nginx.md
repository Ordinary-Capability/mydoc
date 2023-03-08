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