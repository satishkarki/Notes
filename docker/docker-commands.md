It works on my machine !!!

```sh
# installs docker engine and cli
sudo apt install docker.io
```
```sh
# check the status
systemctl status docker 
# or
service docker status

# Output
butcher@TF-250718105924:~/repo/Notes$ sudo service docker status
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-01-07 14:00:16 EST; 1h 58min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 3261 (dockerd)
      Tasks: 16
     Memory: 22.3M (peak: 23.6M)
        CPU: 2.662s
     CGroup: /system.slice/docker.service
             └─3261 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

```

Based on the above output, 