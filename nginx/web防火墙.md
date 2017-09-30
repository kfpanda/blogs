# web防火墙
    出于安全的考虑，最近刚好有时间研究一下网站安全方面方案，顺便写片文章记录一下。

常见的WEB网站攻击方式：引用 web攻击方式。

控制web网站安全方案主要有一下几块：<br>
1. 使用硬件设备来控制网络层面的攻击。
2. 第三方防御服务：
    一、高防：http://www.fangyuba.com
    二、
2. Nginx 模块 ModSecurity 、 http_guard 、 ngx_lua_waf <br>
  ModSecurity 应用层WAF，功能强大，能防御的攻击多，配置复杂
  ngx_lua_waf 基于 ngx_lua 的 web 应用防火墙，使用简单，高性能和轻量级
  http_guard 基于 openresty

[ModSecurity](https://www.modsecurity.org) 是Apache提供的一个Web安全WAF的项目。目前支持：Apache、nginx、IIS Web服务器。
且其[安全规则](https://www.modsecurity.org/crs/)在持续的更新和维护中。
https://www.52os.net/articles/nginx-use-modsecurity-module-as-waf.html

[http-guard](https://github.com/centos-bz/HttpGuard) 是基于openrest 做开发，项目在Git上已经多年未更新。<br>
使用参考：<br>
https://www.centos.bz/http-guard/
https://www.centos.bz/2011/03/20-steps-to-create-the-best-secure-nginx-web-server/

[ngx_lua_waf](https://github.com/loveshell/ngx_lua_waf) 是使用lua做的一个网络防火墙，程序逻辑比较简单，可以自行加工扩展。
项目在Git上已经多年未更新。<br>

一. 限制每秒请求数
ngx_http_limit_req_module
二.限制IP连接数
ngx_http_limit_conn_module 的配置方法和参数与 http_limit_req 模块很像

