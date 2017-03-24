installing-logstash:
https://www.elastic.co/guide/en/logstash/5.2/installing-logstash.html
<<<<<<< HEAD
Rest-Assured

辞旧迎新，随想贷一大波版本来了，我的小伙伴，2017属于我们。

随想贷V1.3版本需求评审会议
会议地址：大会议室
会议时间：本周五 2017-2-10 14：00 - 15：30
会议内容：车主信用贷需求评审。
会议主要内容安排： 
20分钟 APP需求介绍。
20分钟 后端需求介绍。
20分钟 提问。
其它
参会成员：
本群相关成员
如不能参加会议，请提前说明。谢谢！


1、随想贷
刘化罗、李瑞、姜缘、孙显龙、李浩博、见冰冰
潘俊霖、李亚军、林徳鹏
测试：丰涛、张涛

2、人审系统
刘化罗、姜缘、李浩博
潘俊霖
测试：丰涛、张涛

3、规则系统二期
刘化罗、李永杰、薛永峰、唐佳妹、单黄勇、杨闯、龙昊、潘俊霖
测试：董月倩

4、消息系统四期
刘化罗、李瑞、李浩博
测试：丰涛

5、大数据抓爬服务
姜缘、王学智
测试：牛晓静

6、数据服务系统
刘化罗、李瑞、孙显龙
测试：未安排

7、微贷助手
孙显龙

8、催收系统
未安排

9、预警系统
未安排





1、随想贷
2、人审系统
3、规则系统二期
4、消息系统四期
5、大数据抓爬服务
6、数据服务系统
7、微贷助手
8、催收系统
9、预警系统


1、傅总确认问题：
由原无源。
ocr 每次是否都需要。

法大大是否人 电子签章 的条件。


数据堂 合同。

=======

YUMedit
Download and install the public signing key:

rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
Add the following in your /etc/yum.repos.d/ directory in a file with a .repo suffix, for example logstash.repo

[logstash-5.x]
name=Elastic repository for 5.x packages
baseurl=https://artifacts.elastic.co/packages/5.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
And your repository is ready for use. You can install it with:

sudo yum install logstash
>>>>>>> 7e5c56edee9cfec33fc7b21608e3b0505e4fd8fe
