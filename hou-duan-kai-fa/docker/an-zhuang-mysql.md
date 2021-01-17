# 安装MySql

#### 查看可用版本

```bash
docker search mysql
```

```text
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   10317     [OK]
mariadb                           MariaDB is a community-developed fork of MyS…   3822      [OK]
mysql/mysql-server                Optimized MySQL Server Docker images. Create…   754                  [OK]
percona                           Percona Server is a fork of the MySQL relati…   517       [OK]
centos/mysql-57-centos7           MySQL 5.7 SQL database server                   86
mysql/mysql-cluster               Experimental MySQL Cluster Docker images. Cr…   79
centurylink/mysql                 Image containing mysql. Optimized to be link…   60                   [OK]
bitnami/mysql                     Bitnami MySQL Docker Image                      47                   [OK]
deitch/mysql-backup               REPLACED! Please use http://hub.docker.com/r…   41                   [OK]
tutum/mysql                       Base docker image to run a MySQL database se…   35
databack/mysql-backup             Back up mysql databases to... anywhere!         34
prom/mysqld-exporter                                                              33                   [OK]
schickling/mysql-backup-s3        Backup MySQL to S3 (supports periodic backup…   29                   [OK]
linuxserver/mysql                 A Mysql container, brought to you by LinuxSe…   27
centos/mysql-56-centos7           MySQL 5.6 SQL database server                   20
circleci/mysql                    MySQL is a widely used, open-source relation…   19
mysql/mysql-router                MySQL Router provides transparent routing be…   17
arey/mysql-client                 Run a MySQL client from a docker container      16                   [OK]
fradelg/mysql-cron-backup         MySQL/MariaDB database backup using cron tas…   10                   [OK]
yloeffler/mysql-backup            This image runs mysqldump to backup data usi…   7                    [OK]
openshift/mysql-55-centos7        DEPRECATED: A Centos7 based MySQL v5.5 image…   6
devilbox/mysql                    Retagged MySQL, MariaDB and PerconaDB offici…   3
ansibleplaybookbundle/mysql-apb   An APB which deploys RHSCL MySQL                2                    [OK]
jelastic/mysql                    An image of the MySQL database server mainta…   1
widdpim/mysql-client              Dockerized MySQL Client (5.7) including Curl…   1                    [OK]
```

#### 拉取MySql镜像

```text
docker pull mysql:latest
```

```text
latest: Pulling from library/mysql
6ec7b7d162b2: Pull complete
fedd960d3481: Pull complete
7ab947313861: Pull complete
64f92f19e638: Pull complete
3e80b17bff96: Pull complete
014e976799f9: Pull complete
59ae84fee1b3: Pull complete
ffe10de703ea: Pull complete
657af6d90c83: Pull complete
98bfb480322c: Pull complete
6aa3859c4789: Pull complete
1ed875d851ef: Pull complete
Digest: sha256:78800e6d3f1b230e35275145e657b82c3fb02a27b2d8e76aac2f5e90c1c30873
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest
```

#### 查看本地镜像

```text
docker images
```

![](../../.gitbook/assets/image%20%282%29.png)

#### 运行容器

```text
docker run -itd --name mysql-db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=12345678 mysql
```

#### 查看是否安装成功

```text
docker ps
```

![](../../.gitbook/assets/image%20%289%29.png)

