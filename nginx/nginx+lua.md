# nginx Lua 环境搭建

1. 准备Openresty依赖：<br>
apt-get install libreadline-dev libncurses5-dev libpcre3-dev libssl-dev perl<br>
make build-essential<br>
或者<br>
yum install readline-devel pcre-devel openssl-devel gcc<br>
2. 安装Openresty：<br>
cd /opt/nginx/ # 安装文件所在目录 <br>
wget https://openresty.org/download/openresty-1.11.2.4.tar.gz<br>
tar -xzf openresty-1.11.2.4.tar.gz /opt/nginx/<br>
3. 配置:<br>
#指定目录为/opt/openresty, 默认在/usr/local。 -- 这个目录可以随意指定，但必须和下面的对应<br>
./configure --prefix=/opt/openresty \<br>
--with-luajit \ <br>
--without-http_redis2_module \<br>
--with-http_iconv_module <br>
make <br>
make install <br>

#下载lua-resty-kafka: 
wget https://github.com/doujiang24/lua-resty-kafka/archive/master.zip 
unzip master.zip -d /opt/nginx/ 
#拷贝lua-resty-kafka到openresty 
mkdir /opt/openresty/lualib/kafka 
cp -rf /opt/nginx/lua-resty-kafka-master/lib/resty /opt/openresty/lualib/kafka/ 

### 引用：
* https://openresty.org

修改 nginx.conf


nginx.conf :

#user nobody;
worker_processes 1;

#error_log logs/error.log;
#error_log logs/error.log notice;
#error_log logs/error.log info;

#pid logs/nginx.pid;


events {
use epoll;
worker_connections 1024;
}


http {

include mime.types;
default_type application/octet-stream; 

keepalive_timeout 0; 
gzip on; 
gzip_min_length 1k; 
gzip_buffers 4 8k; 
gzip_http_version 1.1; 
gzip_types text/plain application/x-JavaScript text/css application/xml application/X-JSON; 
charset UTF-8; 
#配置后端代理服务
#upstream rc{ 
#server 192.168.20.41 weight=4 max_fails=3;
#最大长连数
#keepalive 32;
#} 
#lua模块路径，多个之间”;”分隔，其中”;;”表示默认搜索路径，默认/kfpanda/nginx-lua-kafka下找 
lua_package_path "/kfpanda/nginx-lua-kafka/example/lualib/kafka/?.lua;;"; #lua 模块 
lua_package_cpath "/kfpanda/nginx-lua-kafka/example/lualib/?.s;;"; #c模块 

#include /kfpanda/nginx-lua-kafka/example/example.conf; 
#log_format main '$remote_addr - $remote_user [$time_local] "$request" '
#'$status $body_bytes_sent "$http_referer" '
#'"$http_user_agent" "$http_x_forwarded_for"';

#access_log logs/access.log main;

sendfile on;
#tcp_nopush on;


#keepalive_timeout 65;



server {
listen 801;
server_name localhost;

#charset koi8-r;

#access_log logs/host.access.log main;

location / {
root html;
index index.html index.htm;
}
location /s/1 { 
default_type 'text/html';
content_by_lua 'ngx.say(ngx.var.args)'; 
proxy_connect_timeout 8; 
proxy_send_timeout 8; 
proxy_read_timeout 8; 
proxy_buffer_size 4k; 
proxy_buffers 512 8k; 
proxy_busy_buffers_size 8k; 
proxy_temp_file_write_size 64k; 
proxy_next_upstream http_500 http_502 http_503 http_504 error timeout invalid_header; 
root html; 
index index.html index.htm; 
#proxy_pass http://www.baidu.com;
proxy_http_version 1.1; 
proxy_set_header Connection ""; 
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
#使用log_by_lua 包含lua代码,因为log_by_lua指令运行在请求最后且不影响proxy_pass机制
log_by_lua ' 
-- 引入lua所有api 
local cjson = require "cjson" 
local producer = require "resty.kafka.producer" 
-- 定义kafka broker地址，ip需要和kafka的host.name配置一致 
local broker_list = {
{ host = "192.168.21.228", port = 9092 },
{ host = "192.168.21.220", port = 9092 },
{ host = "192.168.21.180", port = 9092 }
} 

-- 定义json便于日志数据整理收集 
args = ngx.var.args;
args = string.gsub(args, "%%(%x%x)", function(h) return string.char(tonumber(h, 16)) end) ; 
function trim(s) return (string.gsub(s, "%s*(.-)%s*", "%1"))end ;
--args=trim(args)
-- 校验 
--参数不能为空
array={[["p":]],[["t":]],[["k":]],[["d":]]};
_array={[["p" :]],[["t" :]],[["k" :]],[["d" :]]};
local flag=true;
local kong=false;
for i,v in ipairs(array) do
local n,m=string.find(args,v);
if(not n)
then 
local n,m=string.find(args,_array[i]);
if(not n) 
then
flag=false;
else
kong=true;
end
end
end
if(kong)
then
array=_array
end
if(flag) then
local pm=string.sub(args,4,-1); 
local i,j = string.find(pm,"} ");
pm = string.sub(pm,0,j); 
pm=string.gsub(pm,array[1],[["project":]],1);
pm=string.gsub(pm,array[2],[["type":]],1);
pm=string.gsub(pm,array[3],[["key":]],1);
pm=string.gsub(pm,array[4],[["data":]],1); 
--local message = cjson.encode(pm); 
-- 转换json为字符串 
-- 定义kafka异步生产者 
local bp = producer:new(broker_list, { producer_type = "async" }) 
-- 发送日志消息,send第二个参数key,用于kafka路由控制: 
-- key为nill(空)时，一段时间向同一partition写入数据 
-- 指定key，按照key的hash写入到对应的partition 
local ok, err = bp:send("topic_bigdata_test", nil,pm) 

if not ok then 
ngx.log(ngx.ERR, "kafka send err:", err) 
return 
end 
else 
ngx.log(ngx.ERR, "para missing:", args)
return 
end;
'; 

return 200 '{"r":1}';
}

}


