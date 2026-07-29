# Docker

> It works on my machine !!!

I am using Fedora so I am following [installtion on Linux](https://docs.docker.com/desktop/setup/install/linux/) guide for Docker Desktop.

Under general requirement, it says Docker desktop depends on KVM virtualization and QEMU. What does it mean?

Don't be confused. Docker itself doesn't normally depend on KVM or QEMU. Docker engine runs directly on Linux. Docker containers share the host’s Linux kernel. Docker uses Linux features called namespaces to keep containers separated and control groups, or cgroups, to limit CPU and memory use. It does not need to create a separate virtual computer for every container.

On the other hand, Docker Desktop creates a small Linux virtual machine. That VM uses:
* KVM to run efficiently on the real CPU.
* QEMU as part of the virtual-machine environment.
* Docker Engine inside the VM.
* Containers inside that Docker Engine.

Lets briefly tocuh on KVM and QEMU before diving into Docker Desktop installtion. 
QEMU as the name suggest- Quick Emulator creates virtual machine model- motherboard, firmware, disks, network cards, display, USB ect. It can even emulate the CPU. But the software emulated CPU can be slow- thats where the KVM comes in. Kernal-based Virtual Machine turns Linux kernel into a hardware assisted hypervisor.  It lets normal guest CPU instrcutions run directly on the host CPU. 

![KVM QEMU](/Notes/docker/image-resource/kvm-qemu.png)



## Installation

**Installing using rpm repository**

1. [Docker's package repository](https://docs.docker.com/engine/install/fedora/#set-up-the-repository)

   ```bash
   # Set up the repository
   sudo dnf config-manager addrepo --from-repofile https://download.docker.com/linux/fedora/docker-ce.repo
   ```
2. Download the latest [RPM package](https://desktop.docker.com/linux/main/amd64/docker-desktop-x86_64.rpm?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64). 

3. Install the pacakge with dnf
   ```bash
   sudo dnf install ./docker-desktop-x86_64.rpm
   ```
Unfortunately, the above process didn't work for me. I am using M3 mac, runing VMware hypervisor on it and running Fedora inside it, now I am tryring to install Decoker desktop (another VM) with in Fedora (another VM). 
```bash
M3 Mac
└── VMware Fusion VM
    └── Fedora
        └── Docker Desktop VM
            └── Containers
```


This is virtualization inside virtualization. Broadcom states that nested hypervisors are generally unsupported in Fusion and that Apple-silicon Fusion hosts do not currently provide nested virtualization.

Instead, lets roll with docker engine, who cares about the docker GUI, I am a command line hero, yeah- lets do it.  Only if I knew how to get out of VIM :). Here is how it will look now.

```bash
M3 Mac
└── VMware Fusion
    └── Fedora ARM64
        └── Docker Engine
            ├── Container A
            └── Container B
```

