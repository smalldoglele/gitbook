* 配置多个负载均衡节点，使用模块名称来区分
* 调整access\_log日志配置信息，最新版的需要在server中指定配置日志的自定义格式才能生效；
* 配置文件中，在ubuntu中nginx设置，如顶层设置
  ```
  ##########################################################
  #  负载均衡服务器
  ###########################################################
  upstream report-server {
    server 192.168.1.254:8181 weight=1;
    server 192.168.1.88:8181 weight=1;
  }
  upstream  yunwei-server {
    server 192.168.1.254:8200 weight=1;
    server 192.168.1.88:8200 weight=1;
  }
  upstream kefu-server{
    server 192.168.1.254:8210 weight=1;
    server 192.168.1.88:8210 weight=1;
  }
  upstream  dianjia-server  {
    server 192.168.1.254:8220 weight=1;
    server 192.168.1.88:8220 weight=1;
  }
  upstream  app-server {
    server 192.168.1.254:8100 weight=1;
    server 192.168.1.88:8100 weight=1;
  }
  upstream  common-server{
    server 192.168.1.254:8110 weight=1;
    server 192.168.1.88:8110 weight=1;
  }
  upstream  community-server {
    server 192.168.1.254:8120 weight=1;
    server 192.168.1.88:8120 weight=1;
  }
  upstream  contacts-server  {
    server 192.168.1.254:8130 weight=1;
    server 192.168.1.88:8130 weight=1;
  }
  ```
* server节点中指定server\_name
  ```
  server_name report-server yunwei-server kefu-server dianjia-server app-server common-server community-server contacts-server;
  ```
* 反向代理配置，修改如下
  ```
  location /study- {
    proxy_pass   http://app-server/handler/study-;
    proxy_redirect default ;
  }
  ```
* 配置日志格式，需要在http模块中配置如下：
  ```
  log_format  access_log_format  '$remote_addr - $remote_user [$time_local] "$request" '
                               '$status $body_bytes_sent "$http_referer" '
                               '"$http_user_agent" $http_x_forwarded_for '
                               '"$upstream_addr" "$upstream_status" "$upstream_response_time" "$request_time"';
  ```
* 如果要使用自定义的日志格式需要在server中声明如下：
  ```shell
  access_log /var/log/nginx/access.log access_log_format;
  ```



