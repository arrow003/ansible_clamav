## ansible install ClamAV
本脚本支持在CentOS7/8、RedHat7/8、Rocky Linux 8、Alma Linux 8

1.在ansible服务器侧添加准备安装ClamAV杀毒软件的服务器的hosts


$ cat /etc/ansible/hosts 
```
[ClamAV_centos8]
172.26.37.141 ansible_ssh_user=root ansible_ssh_pass='123456'
[ClamAV_centos7]
172.26.37.204 ansible_ssh_user=root ansible_ssh_pass='123456'
```
2.下载ansible安装的playbook等文件

$ git clone git@github.com:arrow003/ansible_clamav.git

$ cd ansible_clamav

$ git checkout ansible_clamav_resource

3.执行playbook

$ ansible-playbook ansible_clamav_centos7.yaml

说明：CentOS7、RedHat7都可以

$ ansible-playbook ansible_clamav_centos8.yaml

说明：CentOS8、RedHat8、Rocky Linux 8、Alma Linux 8都可以


## 更新ClamAV病毒库

$ ansible-playbook ansible_clamav_fedora.yaml --tags update_clamav_dat

## 测试ClamAV运行

$ /usr/sbin/clamd &

稍等1-2分钟，待clamscan启动完成

$ ps -ef|grep clam
```
clamscan   38558       1 40 23:25 ?        00:00:44 /usr/sbin/clamd
```
如果存在两个进程，说明还在启动过程中

$ /usr/bin/clamdscan  -i  /var/log

## 更新ClamAV版本

$ ansible-playbook ansible_clamav_fedora.yaml --tags install_and_update
