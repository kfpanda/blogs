installing-logstash:
https://www.elastic.co/guide/en/logstash/5.2/installing-logstash.html
<<<<<<< HEAD
Rest-Assured



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
