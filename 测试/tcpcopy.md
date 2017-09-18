# TCPCOPY 导入线上流量进行功能和压力测试
    每次项目发布的时候，开发和测试都由衷的一种恐惧感，唯恐系统出现问题影响个人业绩。
    所以如何做好uat环境的测试很重要，TCPCOPY正好是解决这方面测试的一种不错的方案。

#### 测试环境的搭建：
1、TCPCopy安装：<br>
git clone http://github.com/session-replay-tools/tcpcopy<br>
./configure （默认raw socket方式抓包）<br>
或者<br>
./configure --pcap-capture  （pcap方式抓包，在某些场景下，丢包率会高于raw socket方式抓包，这时候需要类似pf_ring的支持）<br>

2、Intercept安装：<br>
代码下载地址：<br>
git clone http://github.com/session-replay-tools/intercept<br>
configure方式： <br>
./configure <br>
> http://blog.csdn.net/wangbin579/article/details/8950282<br>

### 引用：
* https://github.com/wangbin579/tcpcopy
* http://blog.gaoyuan.xyz/2014/01/08/use-tcpcopy-test-online/
* http://www.searchtb.com/2012/05/using-tcpcopy-to-simulate-traffic.html
* http://hi.baidu.com/yacker/item/e6bd5b287fe5a3f150fd8731
* http://blog.yam.com/hn12303158/article/35207136
* http://www.cnblogs.com/zhengyun_ustc/p/tcpcopy.html
* http://www.cnblogs.com/tommyli/p/4239570.html