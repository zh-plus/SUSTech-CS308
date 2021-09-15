---
layout: page
title: Lab0: How to Develop on HUAWEI Cloud
---

# Lab0: How to Develop on a Remote Server

**Lecturer: 郑浩 (RA in SUSTech Zhengfeng Lab)**

### How to connect to remote server

0. Start your terminal
   - WIN+R & `cmd.exe`
   - Click the Launchpad in the Dock, type `Terminal` in the search field, then click Terminal.

1. SSH to server
   `ssh -p PORT username@host`: check [here](https://explainshell.com/explain?cmd=ssh+-p+PORT+username%40host) to explain the meaning of this command
   - For example: `ssh -p 10022 11610127@127.0.0.1`
   - Temporary server: (users would be deleted after this lab)
     - host: 10.16.36.240
     - PORT: 10022
     - username: \<your student ID\>
     - password: \<your student ID\>_cv
   
2. Privacy protection
   `chmod 700 /disk1/cv_home/<your student ID>`
   
   <img src="image\lab0\Snipaste_2021-09-07_20-30-38.png" style="zoom:50%;" />
   (Image from [https://chmodcommand.com/chmod-700/](https://chmodcommand.com/chmod-700/))
   
3. Recommended ssh management tools

   - XShell: [https://www.netsarang.com/en/free-for-home-school/](https://www.netsarang.com/en/free-for-home-school/)
   - Windows Terminal: [https://github.com/microsoft/terminal](https://github.com/microsoft/terminal)
     - You can install Terminal in [Windows store](https://aka.ms/terminal): 
     - Open terminal setting:

       <img src="image\lab0\Snipaste_2021-09-07_20-46-31.jpg" style="zoom:25%;" />
     - Config your command:

       <img src="image\lab0\Snipaste_2021-09-07_20-45-43.jpg" style="zoom:25%;" />
   - MobaXterm: [https://mobaxterm.mobatek.net/](https://mobaxterm.mobatek.net/)


### Anaconda

0. Download installer: `wget URL`

   - Official: [https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh](https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh)
     
     (The latest URL can be retrieved in https://www.anaconda.com/products/individual-d#linux)
   - SUSTech mirror (Recommended): 
     [https://mirrors.sustech.edu.cn/anaconda/archive/Anaconda3-2021.05-Linux-x86_64.sh](https://mirrors.sustech.edu.cn/anaconda/archive/Anaconda3-2021.05-Linux-x86_64.sh)
     
     (The latest URL can be retrieved in [https://mirrors.sustech.edu.cn/anaconda/archive/](https://mirrors.sustech.edu.cn/anaconda/archive/))

1. Set executable: `chmod 777 Anaconda3-2021.05-Linux-x86_64.sh`

2. `./Anaconda3-2021.05-Linux-x86_64.sh` and always Enter Enter Enter......

3.  Active the installed environment: `source ~/.bashrc`  [Command Explain](https://explainshell.com/explain?cmd=ssh+-p+PORT+username%40host) 

4. Set Conda mirror

   - use vim to edit `vim ~/.condarc`

   - press `i` to enter insert mode

   - Copy and Paste:

     ```
     channels:
       - defaults
     show_channel_urls: true
     default_channels:
       - https://mirrors.sustech.edu.cn/anaconda/pkgs/main
       - https://mirrors.sustech.edu.cn/anaconda/pkgs/free
       - https://mirrors.sustech.edu.cn/anaconda/pkgs/r
       - https://mirrors.sustech.edu.cn/anaconda/pkgs/pro
       - https://mirrors.sustech.edu.cn/anaconda/pkgs/msys2
     custom_channels:
       conda-forge: https://mirrors.sustech.edu.cn/anaconda/cloud
       msys2: https://mirrors.sustech.edu.cn/anaconda/cloud
       bioconda: https://mirrors.sustech.edu.cn/anaconda/cloud
       menpo: https://mirrors.sustech.edu.cn/anaconda/cloud
       pytorch: https://mirrors.sustech.edu.cn/anaconda/cloud
       simpleitk: https://mirrors.sustech.edu.cn/anaconda/cloud
     ```

     (The Configuration can be find in [https://mirrors.sustech.edu.cn/help/anaconda.html](https://mirrors.sustech.edu.cn/help/anaconda.html))

   - Exit vim:
     1. press `Esc`
     2. press `:`
     3. input `wq`
     4. press `Enter`
     
   - Show current used mirror: `conda config --show-sources`

     <img src="image\lab0\Snipaste_2021-09-07_21-18-39.png" style="zoom:43%;" />

5. Set pip mirror

   - create directory: `mkdir ~/.pip`

   - `vim ~/.pip/pip.conf`

   - press `i` to enter insert mode

   - Copy & Paste

     ```
     [global]
     index-url=http://mirrors.aliyun.com/pypi/simple/
     [install]
     trusted-host=mirrors.aliyun.com
     ```

6. Create and Switch environment using Conda

   - Create `conda create -n <your environment name> python=3.8`

     **Example**: `conda create -n pytorch_env python=3.8`

   - Switch `conda activate <your environment name>`

     **Example**: `conda activate pytorch_env`

   - You can switch back to `base` environment using `conda deactivate`

7. Install PyTorch

   `conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch`
   
   Official: [https://pytorch.org/](https://pytorch.org/)

   <img src="image\lab0\Snipaste_2021-09-07_21-21-39.png" style="zoom: 50%;" />

8. Check CUDA driver

   - Display detailed GPU info
     `nvidia-smi`

     <img src="image\lab0\Snipaste_2021-09-07_21-24-32.png" style="zoom:30%;" />

   - Display GPU info
     ```shell
     pip install gpustat
     gpustat
     ```

     <img src="image\lab0\Snipaste_2021-09-07_21-26-42.png" style="zoom:43%;"/>

   - Verification

     `python`

     ```python
     import pytorch
     torch.cuda.is_available() # Should output True
     ```


### Tools to code remotely

#### Jupyter Lab

0. Activate your environment

   ```shell
   conda activate <env name>
   ```

1. Install Jupyter and required packages

   ```shell
   conda install jupyterlab 
   ```

2. Run Jupyter in **server terminal**

   ```shell
   jupyter lab --no-browser --port=PORT_NUM # 1024-65535
   ```

   <!-- $PORT\_NUM = 1024 + (SID \; mod \; (65535 - 1024)) = 1024 + (SID \; mod \; 64511)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=PORT%5C_NUM%20%3D%201024%20%2B%20(SID%20%5C%3B%20mod%20%5C%3B%20(65535%20-%201024))%20%3D%201024%20%2B%20(SID%20%5C%3B%20mod%20%5C%3B%2064511)">

3. Run SSH port forwarding in **local terminal**

   - open a new terminal in **you machine (NOT Server!)**

   - ```shell
     ssh -N -f -L localhost:8888:localhost:PORT_NUM username@serverIP -p 10022
     ```

     [Explanation](https://explainshell.com/explain?cmd=ssh+-N+-f+-L+localhost%3A8888%3Alocalhost%3APORT_NUM+username%40serverIP+-p+10022#) 

   -   Access Jupyter Lab by visit `localhost:8888`



#### PyCharm Remote (Optional)

0. Download PyCharm: [https://www.jetbrains.com/pycharm/](https://www.jetbrains.com/pycharm/)
1. PyCharm Remote tutorial: [https://zhuanlan.zhihu.com/p/93236936](https://zhuanlan.zhihu.com/p/93236936)
   - Remember to set port to 10022 instead of 22



### Huawei Cloud

0. 申请华为云账号：https://www.huaweicloud.com/ 右上角注册
1. 登录后实名认证

   <img src="image\lab0\Snipaste_2021-09-07_21-57-04.png" style="zoom:33%;" />

   <img src="image\lab0\Snipaste_2021-09-07_22-06-19.png" style="zoom:33%;" />
2. 扫描二维码，登记账号信息

   <img src="image\lab0\unnamed.png" style="zoom: 50%;" />
3. 五个工作日内华为会发放500代金券，我们本学期将使用华为云进行实验课程，请大家暂时不要使用代金券开通任何实例。下节课程会指导使用华为云的按时计费型服务器。

