---
title: "# Installing NVIDIA drivers  (+ CUDA toolkits) in debian based systems (e.g., in my case Ubuntu 22.04.2 LTS)"
date: 2023-04-12T15:34:30-04:00
categories:
  - blog
tags:
  - linux NVIDIA drivers
  - Errors were encountered while processing
---

![](https://images.unsplash.com/photo-1555618254-84e2cf498b01?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1171&q=80)

Machine learning, especially deep learning requires a lot of computational power. Tensorflow an open-source software can greatly improve computation as it can utilise the GPU under the NVIDIA-CUDA enabled systems. If you are using a laptop, you might have an integrated graphics card (Intel) and a discrete graphics card (e.g., NVIDIA). Updating your system may require you to also update the new drivers for your GPUs. If you use cloud frameworks like AWS, you will have access to a range of powerful NVIDIA GPUs. However, AWS instances built from scratch will usually not have the NVIDIA drivers installed, and you have to do that yourself (which can be a bit of hassle). 

There are lots of tutorials on the web, here I will show you the way that worked for me. Maybe it will work for you too. 

First thing you do is check whether you have an NVIDIA graphics card in your laptop/instance You can do that by running the following commands in the terminal:

```
lspci | grep -e VGA 
```

lspci = "list pci devices" and grep -e VGA = "search for a pattern VGA". The lspci command will list all the PCI devices in your system. The second command will list all the PCI devices that have the word "VGA" in them. You can see your display adapter in the output. 

You can get more details about your graphics card by running the following command (I like this method). lshw = "list hardware" and -C video = "list only the video hardware".

```
sudo lshw -C video

```
My laptop has both Intel and NVIDIA cards so I get information about both of them like this: 

```
 *-display                 
       description: VGA compatible controller
       product: UHD Graphics 620
       vendor: Intel Corporation
       physical id: 2
       bus info: pci@0000:00:02.0
       logical name: /dev/fb0
       version: 07
       width: 64 bits
       clock: 33MHz
       capabilities: pciexpress msi pm vga_controller bus_master cap_list rom fb
       configuration: depth=32 driver=i915 latency=0 resolution=1920,1080
       resources: irq:130 memory:ed000000-edffffff memory:c0000000-cfffffff ioport:f000(size=64) memory:c0000-dffff
  *-display
       description: 3D controller
       product: GP108M [GeForce MX150]
       vendor: NVIDIA Corporation
       physical id: 0
       bus info: pci@0000:01:00.0
       version: a1
       width: 64 bits
       clock: 33MHz
       capabilities: pm msi pciexpress bus_master cap_list rom
       configuration: driver=nvidia latency=0
       resources: irq:132 memory:ee000000-eeffffff memory:d0000000-dfffffff memory:e0000000-e1ffffff ioport:e000(size=128) memory:ef000000-ef07ffff```
```
If you do not see your NVIDIA cards in the list, maybe you do not have one. You can also confirm that by booting in BIOS mode and checking the specifications of your laptop. 

Now that you have confirmed that you have an NVIDIA graphics card, you can proceed to install the drivers.


**Oh wait a minute ! First you need to clean any NVIDIA (or also CUDA) residues from
previous installation or from your previous attempt etc**

The following 3 scripts is a more aggressive method as it removes all packages that have "nvidia" or "cuda" in their name, along with NVIDIA related library packages (libnvidia). The ```--purge``` option removes the configuration files as well.

```
sudo apt-get remove --purge '^nvidia-.*' 
sudo apt-get remove --purge '^libnvidia-.*'
sudo apt-get remove --purge '^cuda-.*'
```
Sometimes you also install the NVIDIA drivers from the NVIDIA website. By downloading the ```.run``` file and running it. In that case you need to remove the NVIDIA drivers this way: 

```
sudo /usr/bin/nvidia-uninstall
```

Will these codes break my system ? No, they will most likely not. They will only remove the NVIDIA and CUDA packages. If you have any other packages that have "nvidia" or "cuda" in their name, they will be removed as well. But as always back up your system before you do anything.

Now that you have removed all the NVIDIA and CUDA packages, you can proceed to install the drivers. There are 2 ways to install the drivers; through the (i) terminal and (ii) GUI. I prefer the terminal method because it is faster and you can see the progress of the installation. 

**Terminal method**

Update package lists and upgrade packages
```
sudo apt update && sudo apt upgrade
```
Identify the graphics card and their recommended drivers

```
ubuntu-drivers devices
```

You can now proceed with the install, either specify the version you like to install, mine shows nvidia-driver-510 so I run the following command:
```
sudo apt install nvidia-driver-510
```
or install the recommended one (both are same)
```
sudo ubuntu-drivers autoinstall
```
However, I had issues with installing using the default Ubuntu APT repository, while installing the recommended driver which was nvidia-driver-510. More specifically, I got the error:  

<font color="red">Errors </font>

```
Errors were encountered while processing:
 nvidia-dkms-510
 nvidia-driver-510
E: Sub-process /usr/bin/dpkg returned an error code (1)
```
A lot of fiddling on the web, I found out that I had to add the following PPA to my system. It is because with updated linux kernels, the NVIDIA drivers available in the repository are not compatible. So you need to add the PPA to get the latest drivers from ```graphics-drivers/ppa``` repository. 

But first you will also need to remove - - purge the broken files from the previous installation attempt (see above)

Install the required dependencies
```
sudo apt install software-properties-common -y
```
Add the PPA and update package lists
```
sudo add-apt-repository ppa:graphics-drivers/ppa -y
```
See the drivers available in the PPA

```
sudo apt update
```

```
ubuntu-drivers devices
```

The output will show new drivers and update the recommendations

```
== /sys/devices/pci0000:00/0000:00:1c.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001D10sv00001043sd00001C20bc03sc02i00
vendor   : NVIDIA Corporation
model    : GP108M [GeForce MX150]
driver   : nvidia-driver-470 - third-party non-free
driver   : nvidia-driver-510 - third-party non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-510-server - distro non-free
driver   : nvidia-driver-525 - third-party non-free recommended
driver   : nvidia-driver-418-server - distro non-free
driver   : nvidia-driver-390 - third-party non-free
driver   : nvidia-driver-515 - third-party non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```

It shows that for my card GeForce MX150, the recommended driver is nvidia-driver-525. So I can install it using the following command: 

```
sudo ubuntu-drivers autoinstall

```

or 

```
sudo apt install nvidia-driver-525

```
You need to restart to apply the changes. 


```
reboot
```

Finally, you can check if the NVIDIA drivers are installed correctly by running the following command:

```
nvidia-smi
```

The output will show something like this: 

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.105.17   Driver Version: 525.105.17   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   52C    P8    N/A /  N/A |      4MiB /  2048MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1924      G   /usr/lib/xorg/Xorg                  4MiB |
+-----------------------------------------------------------------------------+
```

**Once you set up the NVIDIA drivers, you can install CUDA Toolkit**

You can visit the [official website  to download the CUDA Toolkit](https://developer.nvidia.com/cuda-downloads) 

I select OS as Linux, Architecture as x86_64, and Distribution as Ubuntu, and version 22.04. I use the Installer Type: deb(local) 

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda-repo-ubuntu2204-12-1-local_12.1.0-530.30.02-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-1-local_12.1.0-530.30.02-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-1-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```

You can check if the CUDA Toolkit is installed correctly by running the following command:

```
nvidia-smi
```
You can see that both the NVIDIA drivers (also it has updated the driver from 525 to 530) and CUDA Toolkit (v12.1) are installed correctly. 

```
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 530.30.02              Driver Version: 530.30.02    CUDA Version: 12.1     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                  Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf            Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce MX150            On | 00000000:01:00.0 Off |                  N/A |
| N/A   46C    P8               N/A /  N/A|      4MiB /  2048MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A      1917      G   /usr/lib/xorg/Xorg                            4MiB |
+---------------------------------------------------------------------------------------+
```

Bonus tip: did you know about this app called `nvtop`? It is a command-line utility that shows the GPU usage in real-time. It is very useful for monitoring the GPU usage. If not try it out

```
sudo apt install nvtop
```

Run it in your shell using the following command:

```
nvtop
```

![](https://lh3.googleusercontent.com/drive-viewer/AAOQEORxzzaoJFHFooCMPtncfMGkXeOEaeHyUImAsfUeQ5rOVDUJ0EDUJ4q1fl15WX8Bhs3fvowRQKToq-_jN-Nhz2rxDeaA=s1600)  

Congratulations, if both NVIDIA drivers and CUDA Toolkit are installed correctly, you can start using your GPU for deep learning. 

Sometimes you just have a bad day, and your installations are not working. And you are loosing that patience to try out some cool deep learning stuff to vent out all that frustation. Then go try the [Google Colab](https://colab.research.google.com/) . It is a free Jupyter notebook environment that requires no setup and runs entirely in the cloud (and try their free GPUs). It is a great tool for learning and prototyping deep learning models. 

I hope the blog is useful to you. If you have any questions, please feel free to ask. I will try to answer them as soon as possible.

