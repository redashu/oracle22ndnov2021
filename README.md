# Training Plan 

<img src="plan.png">

## Revision 

<img src="rev.png">

### Container 

```
 docker network  create  ashubr1
afe37a90e1c7239abb246cab163a08ed9a5526e0b153a03acacefcb6a27a056b
[ashu@ip-172-31-80-220 appimages]$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
afe37a90e1c7   ashubr1   bridge    local
da65410a2c6d   bridge    bridge    local
f935aeaccb11   host      host      local
d825610a8d02   none      null      local
[ashu@ip-172-31-80-220 appimages]$ docker run -itd --name c3  --network  ashubr1    alpine 
d075f1ce6d2644e709ca72d5137b3452fb0aafe69d81b1ebf74d69ead38714af
[ashu@ip-172-31-80-220 appimages]$ docker run -itd --name c4  --network  ashubr1    alpine 
dfe1c34a68a41c64032fc3978a15b2541e3a2d36c52de26605a7c67e140b1539
[ashu@ip-172-31-80-220 appimages]$ 
[ashu@ip-172-31-80-220 appimages]$ docker exec -it  c3  sh 
/ # 
/ # ping  c4
PING c4 (172.18.0.3): 56 data bytes
64 bytes from 172.18.0.3: seq=0 ttl=64 time=0.082 ms
64 bytes from 172.18.0.3: seq=1 ttl=64 time=0.085 ms
^C
--- c4 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.082/0.083/0.085 ms
/ # exit

```

### network 

```
350   docker network  create  ashubr2 --subnet  192.168.1.0/24 
  351  docker run -itd --name c5  --network ashubr2  alpine 
  352  docker run -itd --name c6  --network ashubr2 --ip 192.168.1.100  alpine
  
```

### container to image 

```
363  docker run -it  --name ashuc11  centos bash 
  364  history 
[ashu@ip-172-31-80-220 appimages]$ docker  commit ashuc11  ashucimg:v007  
sha256:7bd19e44dd4f92dae7dbf31bde1f1db78f618cd3a88bf5504ef8e067c9ff544c
[ashu@ip-172-31-80-220 appimages]$ 
[ashu@ip-172-31-80-220 appimages]$ docker  tag  ashucimg:v007  dockerashu/orday3:v3 
[ashu@ip-172-31-80-220 appimages]$ 
[ashu@ip-172-31-80-220 appimages]$ docker login -u dockerashu
Password: 
WARNING! Your password will be stored unencrypted in /home/ashu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[ashu@ip-172-31-80-220 appimages]$ docker push  dockerashu/orday3:v3
The push refers to repository [docker.io/dockerashu/orday3]
338f4be3981d: Pushed 
74ddd0ec08fa: Mounted from varunssai/varundockerapps 
v3: digest: sha256:748b7e49b4e46aae552b576b1d375ea5bd2b9c7306316e93f1d2afea8be2fced size: 741

```

### Storage in Container 

<img src="st.png">

### creating volume in docker engine 

```
docker  volume  create  ashuvol1 
ashuvol1
[ashu@ip-172-31-80-220 appimages]$ docker  volume  ls
DRIVER    VOLUME NAME
local     ashuvol1
local     shared
[ashu@ip-172-31-80-220 appimages]$ docker  volume  inspect  ashuvol1 
[
    {
        "CreatedAt": "2021-11-24T05:11:37Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/ashuvol1/_data",
        "Name": "ashuvol1",
        "Options": {},
        "Scope": "local"
    }
]

```

### access storage in back ground 

<img src="st1.png">

### mounting external location from docker host to container 

```
docker  run -itd  --name ashupyc1  -v  /home/ashu/appimages/pythonapp/:/code111/    ashupython:v1   python3  /code111/oracle.py 

```

### mounting host data 

```
docker run -it --rm   -v  /etc:/myetc:ro  alpine sh 
/ # 
/ # 
/ # cd  /myetc/
/myetc # ls
DIR_COLORS               exports                  man_db.conf              rsyncd.conf
DIR_COLORS.256color      exports.d                mke2fs.conf              rsyslog.conf
DIR_COLORS.lightbgcolor  filesystems              modprobe.d               rsyslog.d
GREP_COLORS              fstab                    modules-load.d           rwtab
GeoIP.conf               gcrypt                   motd                     rwtab.d
GeoIP.conf.default       gnupg                    mtab                     sasl2
NetworkManager           groff                    m

```




