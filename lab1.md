# Lab1: How to Develop on HUAWEI Cloud

**Lecturer: 谢国洋**

### How to use HUAWEI Cloud

Check the video & Lab demo.



### How to connect to remote server

0. Start your terminal
   - WIN+R & `cmd.exe`
     - If `ssh` not installed in windows, check: [https://www.youtube.com/watch?v=xIfzZXHaCzQ](https://www.youtube.com/watch?v=xIfzZXHaCzQ)
   - Click the Launchpad in the Dock, type `Terminal` in the search field, then click Terminal.
   
1. SSH to server
   `ssh -p PORT username@host`: check [here](https://explainshell.com/explain?cmd=ssh+-p+PORT+username%40host) to explain the meaning of this command

   - HUAWEI Cloud server:
     - host:

       <img src="image\lab1\Snipaste_2021-09-15_14-02-16.png" style="zoom:43%;" />

       <img src="image\lab1\Snipaste_2021-09-15_14-07-22.png" style="zoom:43%;" />

     - PORT: 22
     - username: root
     - password: *password you set.*

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
     
   - Exit vim as above

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
     import torch
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
   jupyter lab --no-browser --port=3388 --ip=0.0.0.0 --allow-root
   ```

3. Access Jupyter Lab in browser: `http://<your host IP>:`

   <img src="image\lab1\Snipaste_2021-09-15_14-14-45.png" style="zoom:55%;" />

4. The browser should be:

   <img src="image\lab1\Snipaste_2021-09-15_14-20-22.png" style="zoom:43%;" />



#### PyCharm Remote (Optional)

0. Download PyCharm: [https://www.jetbrains.com/pycharm/](https://www.jetbrains.com/pycharm/)
1. PyCharm Remote tutorial: [https://zhuanlan.zhihu.com/p/93236936](https://zhuanlan.zhihu.com/p/93236936)

