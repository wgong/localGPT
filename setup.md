
# Setup LocalGPT

got error when running `python3 ingest.py`

```
RuntimeError: Found no NVIDIA driver on your system. Please check that you have an NVIDIA GPU and installed a driver from http://www.nvidia.com/Download/index.aspx
```

## How to check NVIDIA driver version on your Linux system
https://linuxconfig.org/how-to-check-nvidia-driver-version-on-your-linux-system

```
$ nvidia-smi

Mon May 29 14:10:09 2023       
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 530.41.03              Driver Version: 530.41.03    CUDA Version: 12.1     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                  Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf            Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce GTX 1080 Ti      Off| 00000000:01:00.0  On |                  N/A |
|  0%   48C    P8               18W / 280W|    519MiB / 11264MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
```


### How to install the NVIDIA drivers on Ubuntu 22.04
https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-22-04


```
# step 1
$ ubuntu-drivers devices

== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001B06sv00003842sd00006694bc03sc00i00
vendor   : NVIDIA Corporation
model    : GP102 [GeForce GTX 1080 Ti]
driver   : nvidia-driver-418-server - distro non-free
driver   : nvidia-driver-510 - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-525 - distro non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-390 - distro non-free
driver   : nvidia-driver-515 - distro non-free
driver   : nvidia-driver-470 - distro non-free
driver   : nvidia-driver-530 - distro non-free recommended
driver   : nvidia-driver-515-server - distro non-free
driver   : nvidia-driver-525-server - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin


# step 2
$ sudo apt install nvidia-driver-530

# step 3
$ sudo reboot
```

## Check Linux version
`uname -r`

5.19.0-35-generic

## Check Ubuntu version
`lsb_release -a`

No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.2 LTS
Release:	22.04
Codename:	jammy


## Ingest docs

```
$ python3 ingest.py


Loading documents from /home/wengong/projects/wgong/localGPT/SOURCE_DOCUMENTS
Loaded 1 documents from /home/wengong/projects/wgong/localGPT/SOURCE_DOCUMENTS
Split into 72 chunks of text
load INSTRUCTOR_Transformer
max_seq_length  512
Using embedded DuckDB with persistence: data will be stored in: /home/wengong/projects/wgong/localGPT
```

## Query Local GPT

```
$ python3 run_localGPT.py

load INSTRUCTOR_Transformer
max_seq_length  512
Using embedded DuckDB with persistence: data will be stored in: /home/wengong/projects/wgong/localGPT
Downloading tokenizer.model: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 500k/500k [00:00<00:00, 7.71MB/s]
Downloading (…)cial_tokens_map.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 411/411 [00:00<00:00, 2.97MB/s]
Downloading (…)okenizer_config.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 715/715 [00:00<00:00, 3.04MB/s]
Downloading (…)lve/main/config.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 582/582 [00:00<00:00, 3.67MB/s]
Downloading (…)model.bin.index.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████| 26.8k/26.8k [00:00<00:00, 54.4MB/s]
Downloading (…)l-00001-of-00002.bin: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████| 9.98G/9.98G [15:18<00:00, 10.9MB/s]
Downloading (…)l-00002-of-00002.bin: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3.50G/3.50G [05:07<00:00, 11.4MB/s]
Downloading shards: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2/2 [20:26<00:00, 613.03s/it]
Loading checkpoint shards: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 2/2 [01:09<00:00, 34.84s/it]
Downloading (…)neration_config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 137/137 [00:00<00:00, 187kB/s]
Xformers is not installed correctly. If you want to use memorry_efficient_attention to accelerate training use the following command to install Xformers
pip install xformers.

> Question:
What is the gang of four?

> Answer:
 The Gang of Four refers to four Supreme Court Justices who were known for their opposition to the Warren Court's expansive interpretation of civil liberties during the 1960s. They are Hugo Black, John Marshall Harlan II, Potter Stewart, and Byron White.


> Question:
what is basic idea behind the US constitution?

> Answer:
 The basic idea behind the U.S. Constitution is to create a more perfect union by establishing justice, providing for the common defense, promoting the general welfare, and securing the blessings of liberty to ourselves and future generations through a system of government with limited powers divided between the federal government and the states.

> Question:
what is Article 1 Section 10 about?

> Answer:
 It appears to be about congressional appropiation of money for the federal government.

Completed in 123.71 sec

```

*Note* my GPU model is GP102 [GeForce GTX 1080 Ti], it took over 2 mins to answer a question.