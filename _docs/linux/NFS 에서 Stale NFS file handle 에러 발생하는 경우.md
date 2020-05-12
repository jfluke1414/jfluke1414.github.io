---
order: 57
title: (LINUX) NFS 에서 Stale NFS file handle 에러 발생하는 경우
category: Linux
---

NFS 를 사용하다 Stale File Handle 에러가 발생하는 경우가 있다면, NFS 의 연결 상태를 의심해 보아야 한다.
예를 들어, NFS 연결되어 있는 디스크 연결이 끊어져 버린 경우의 상태라면 아래와 같은 에러를 접할 때가 있다.
$ ls
.: Stale File Handle
df: `/data': Stale NFS file handle
언마운트를 하고 마운트를 다시 하려고 해도 같은 메시지가 반복된다.
# mount /data
mount.nfs: Stale NFS file handle
이런 경우 간단한 해결방법은, NFS 마운트 포인트를 끊고, 다시 연결해 주면 된다. 하지만 umount 하려고
해도 제대로 연결이 끊어지지 않는다. umount 를 사용할 때 '-f' 옵션을 사용하면 말끔히 해결된다.
아래와 같이 -f 로 언마운트를 하고 다시 마운트를 해 주면 된다.
# umount -f /data
NFS 사용자들이 가끔 겪을 수 있는 문제 같아 살짝 기록해 놓아 본다.
