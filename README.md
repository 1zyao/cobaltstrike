## [CobaltStrike Update](https://cobaltstrike.vercel.app/)

![version](https://img.shields.io/badge/Version-4.5-da282a) [![Docker Automated Build](https://img.shields.io/docker/automated/xrsec/cobaltstrike?label=Build&logo=docker&style=flat-square)](https://hub.docker.com/r/xrsec/cobaltstrike) [![CobaltStrike Docker Build](https://github.com/XRSec/CobaltStrike-Docker/actions/workflows/CobaltStrike_Docker_Build.yml/badge.svg)](https://github.com/XRSec/CobaltStrike-Docker/actions/workflows/CobaltStrike_Docker_Build.yml)

![image-20211015083754121](https://dogefs.s3.ladydaily.com/ZYGG/storage/image-20211015083754121.png?fmt=webp&q=48)

## Introduce

> Cobatstrike is a platform wide multi-party cooperative post penetration attack framework based on Java. Cobaltstrike integrates the functions of port forwarding, port scanning, socket proxy, lifting rights, fishing, remote control Trojan horse and so on. The tool covers almost all the technical links needed in the apt attack chain.
> Use cloud functions to avoid traceability
> Using docker container is fast and convenient
> Use the python script I wrote to avoid privacy disclosure and malicious attacks

## Quickly create

### Server

> If you want to use cloud functions, you must use port 443 inside the container

```bash
docker run -it \
   --name cs \
   -e "passwd=e9PrFYtrPFD2U" \
   -e "server_ip=1.1.1.1" \
   -e "server_port=33009" \
   -e "aliasname=Bing Wallpaper" \
   -e "dname=CN=www.microsoft.com,  OU=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=WA, C=US" \
   -p 443:443 \
   -p 443:443/udp \
   -p 80:80 \
   -p 33009:33009 \
   -p 33009:33009/udp \
   --restart=always \
   xrsec/cobaltstrike:latest

# "tips server_ip=192.168.0.1" | "tips server_ip=86.66.66.66"
# -p 80:80 : http
# -p 443:443 : https
# -p 33009:33009 : admin
# -e "passwd=e9PrFYtrPFD2U" : your password
```

### Clinet

```bash
mkdir CobaltStrike && cd CobaltStrike
docker cp cs:/cobaltstrike/cobaltstrike.jar .
docker cp cs:/cobaltstrike/CSAgent.jar .
wget https://raw.githubusercontent.com/XRSec/CobaltStrike-Update/main/cobaltstrikecn.jar

APPDIR="/home/hello/cobaltstrike"
java -javaagent:$APPDIR/cobaltstrikecn.jar -javaagent:$APPDIR/CSAgent.jar=f38eb3d1a335b252b58bc2acde81b542 -Dfile.encoding=UTF-8 -XX:ParallelGCThreads=4  -XX:+AggressiveHeap -XX:+UseParallelGC -Xms512M -Xmx1024M -jar $APPDIR/cobaltstrike.jar
# macOS `-Xdock:icon=$APPDIR/cobaltstrike.icns`
```

### Preview

![image-20210903211149434](https://dogefs.s3.ladydaily.com/ZYGG/storage/20210903213218094679.png?fmt=webp&q=48)

![image-20210903211214909](https://dogefs.s3.ladydaily.com/ZYGG/storage/20210903213224154378.png?fmt=webp&q=48)

## Thanks

[@doocs](https://www.upload.ee/files/13456591/Cobalt_Strike_4.4__August_04__2021_.7z.html) [JUICY00000](https://github.com/JUICY00000/Cobalt4.4) [anonymous](https://www.123pan.com/s/l1eA-iqdD3)

> Note: if you think that there are some backdoors in this crack patch or those who reprint or delete the copyright, please do not use it!
> Any direct or indirect consequences and losses caused by the dissemination and use of the information provided in this article shall be borne by the user himself, and the author of the article shall not bear any responsibility for this.
> Xrsec has the right to modify and interpret this article. If you want to reprint or disseminate this article, you must ensure the integrity of this article, including all contents such as copyright notice. Without the permission of the author, the content of this article shall not be modified or increased or decreased arbitrarily, and it shall not be used for commercial purposes in any way
