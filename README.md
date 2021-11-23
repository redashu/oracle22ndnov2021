# Training Plan 

<img src="plan.png">

## Revision 

<img src="rev.png">

### docker arch 

<img src="darch.png">


## few more operations in docker 

### checking resources consumption 

```
docker  stats  nikhil 
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O           BLOCK I/O     PIDS
0a6b29904136   nikhil    0.01%     380KiB / 7.761GiB   0.00%     12.2kB / 11.1kB   1.14MB / 0B   1

```

### kill all the running container 

```
[ashu@ip-172-31-80-220 ~]$ docker kill  $(docker  ps  -q)
aaf063e8b5f7
f11f045c8eba
0a6b29904136
5ce9c1b6329e
da17712f979b
13c7c64a67d8
5fd777103a6e
8ef121f58e2a
2b7794f11403
39cf96a655fe
ca367ec62397
30b851ded07e
[ashu@ip-172-31-80-220 ~]$ docker  ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

### removing all containers 

```
 docker  rm $(docker  ps  -aq)
aaf063e8b5f7
f11f045c8eba
0a6b29904136
5ce9c1b6329e
da17712f979b

```

### creating container 

```
docker run -it   centos   bash 
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
a1d0c7532777: Pull complete 
Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
Status: Downloaded newer image for centos:latest
[root@ed213b5917c0 /]# 
[root@ed213b5917c0 /]# 
[root@ed213b5917c0 /]# cat  /etc/os-release 
NAME="CentOS Linux"
VERSION="8"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="8"
PLATFORM_ID="platform:el8"
PRETTY_NAME="CentOS Linux 8"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:8"
HOME_URL="https://centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"
CENTOS_MANTISBT_PROJECT="CentOS-8"
CENTOS_MANTISBT_PROJECT_VERSION="8"
[root@ed213b5917c0 /]# exit
exit
[ashu@ip-172-31-80-220 ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[ashu@ip-172-31-80-220 ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                     PORTS     NAMES
ed213b5917c0   centos    "bash"    31 seconds ago   Exited (0) 9 seconds ago             objective_tereshkova

```

### login into existing container 

```
ashu@ip-172-31-80-220 ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS        PORTS     NAMES
ed213b5917c0   centos    "bash"    2 minutes ago   Up 1 second             objective_tereshkova
[ashu@ip-172-31-80-220 ~]$ docker  exec  -it  ed213b5917c0  bash
[root@ed213b5917c0 /]# 
[root@ed213b5917c0 /]# 
[root@ed213b5917c0 /]# exit
exit
[ashu@ip-172-31-80-220 ~]$ docker run -d --name x1  alpine ping fb.com 
6886cbb39515ee3328316f6257a8817b29d039992b8df5e817200d0d2d46c424
[ashu@ip-172-31-80-220 ~]$ docker  ps
CONTAINER ID   IMAGE     COMMAND         CREATED         STATUS          PORTS     NAMES
6886cbb39515   alpine    "ping fb.com"   2 seconds ago   Up 1 second               x1
ed213b5917c0   centos    "bash"          2 minutes ago   Up 39 seconds             objective_tereshkova
[ashu@ip-172-31-80-220 ~]$ 
[ashu@ip-172-31-80-220 ~]$ 
[ashu@ip-172-31-80-220 ~]$ docker  exec -it x1  sh 
/ # 
/ # 
/ # cat /etc/os-release 
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.14.3
PRETTY_NAME="Alpine Linux v3.14"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://bugs.alpinelinux.org/"
/ # exit

```

## app containerization 

<img src="app1.png">

### image buildng process

<img src="build.png">

### PYthon code containerization 

<img src="pycode.png">

### building first image 

### Dockerfile 

```
FROM oraclelinux:8.5 
# image will be pulled from Docker HUB 
LABEL name=ashutoshh
LABEL email=ashutoshh@linux.com 
# image designer details but optional field
RUN yum install python3 -y 
# during image build time RUN will give
# shell access to write any cmd / script
RUN mkdir  /code 
COPY oracle.py  /code/oracle.py 
# from Dockerfile location to image during build time
CMD ["python3","/code/oracle.py"]
#  to set default process for this docker image 
# docker run -it -d --name x1 image   


```

```
$ ls
Dockerfile  oracle.py
[ashu@ip-172-31-80-220 pythonapp]$ docker build  -t   ashupython:v1  . 
Sending build context to Docker daemon  3.072kB
Step 1/7 : FROM oraclelinux:8.5
 ---> fa4253e97227
Step 2/7 : LABEL name=ashutoshh
 ---> Running in 8686d165f3d9
Removing intermediate container 8686d165f3d9
 ---> d3b9be373c72
Step 3/7 : LABEL email=ashutoshh@linux.com
 ---> Running in 86b07e3c005e
Removing intermediate container 86b07e3c005e
 ---> 3cfe437b046a
Step 4/7 : RUN yum install python3 -y
 ---> Running in fe939bae532b
Oracle Linux 8 BaseOS Latest (x86_64)            49 MB/s |  40 MB     00:00    

```

### checking images 

```
[ashu@ip-172-31-80-220 pythonapp]$ docker  images
REPOSITORY               TAG       IMAGE ID       CREATED          SIZE
madhuri1                 1         26f79fa6e57e   5 seconds ago    399MB
shyampy                  v1        784e614ebb18   12 seconds ago   399MB
ash_python               v1        556adf4c7864   13 seconds ago   399MB
ashupython               v1        df5d1b3b0693   13 seconds ago   399MB

```


