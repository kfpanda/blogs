installing-logstash:
https://www.elastic.co/guide/en/logstash/5.2/installing-logstash.html
<<<<<<< HEAD
Rest-Assured

�Ǿ�ӭ�£������һ�󲨰汾���ˣ��ҵ�С��飬2017�������ǡ�

�����V1.3�汾�����������
�����ַ���������
����ʱ�䣺������ 2017-2-10 14��00 - 15��30
�������ݣ��������ô���������
������Ҫ���ݰ��ţ� 
20���� APP������ܡ�
20���� ���������ܡ�
20���� ���ʡ�
����
�λ��Ա��
��Ⱥ��س�Ա
�粻�ܲμӻ��飬����ǰ˵����лл��


1�������
�����ޡ����𡢽�Ե������������Ʋ���������
�˿��ء����Ǿ����֏���
���ԣ����Ρ�����

2������ϵͳ
�����ޡ���Ե����Ʋ�
�˿���
���ԣ����Ρ�����

3������ϵͳ����
�����ޡ������ܡ�Ѧ���塢�Ƽ��á������¡������껡��˿���
���ԣ�����ٻ

4����Ϣϵͳ����
�����ޡ�������Ʋ�
���ԣ�����

5��������ץ������
��Ե����ѧ��
���ԣ�ţ����

6�����ݷ���ϵͳ
�����ޡ�����������
���ԣ�δ����

7��΢������
������

8������ϵͳ
δ����

9��Ԥ��ϵͳ
δ����





1�������
2������ϵͳ
3������ϵͳ����
4����Ϣϵͳ����
5��������ץ������
6�����ݷ���ϵͳ
7��΢������
8������ϵͳ
9��Ԥ��ϵͳ


1������ȷ�����⣺
��ԭ��Դ��
ocr ÿ���Ƿ���Ҫ��

������Ƿ��� ����ǩ�� ��������


������ ��ͬ��

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
