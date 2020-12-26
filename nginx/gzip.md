### 为静态文件加速

#### 浏览器要加载很多文件，速度很慢，可以使用gip 压缩技术
`操作如下`

```
gzip on;
gzip_min_length 1k;
gzip_comp_level 1;
gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/bmp application/x-bmp image/x-ms-bmp application/vnd.ms-fontobject font/ttf font/opentype font/x-woff;
gzip_vary on;
gzip_disable "MSIE [1-6]\.";
gzip_buffers 32 4k;
gzip_http_version 1.0;

```
