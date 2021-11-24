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



