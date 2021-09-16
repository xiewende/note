##### 1、打开虚拟机

- 账号：root
- 密码：xiaoxie

##### 2、打开fastDFS

- 启动tracker服务
  - /usr/bin/fdfs_trackerd /etc/fdfs/tracker.conf （restart）
- 启动Storage服务
  - /usr/bin/fdfs_storaged /etc/fdfs/storage.conf （restart）

- 启动 nginx
  - 进入 /usr/local/nginx/sbin 目录 ==》./nginx
  - 查看开启的进程：ps aux | grep nginx

##### 3、开启redis服务

- 进入到/usr/local/redis/bin目录 ==》./redis-server &
- 查看开启的进程：ps aux | grep redis

##### 4、防火墙

- 1）查看防火状态：

  - systemctl status firewalld

  - service  iptables status

- 2）暂时关闭防火墙：
  - systemctl stop firewalld
  - service  iptables stop

- 3）永久关闭防火墙
  - systemctl disable firewalld
  - chkconfig iptables off

- 4）重启防火墙
  - systemctl enable firewalld
  - service iptables restart