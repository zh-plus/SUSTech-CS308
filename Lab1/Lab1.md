# CV Lab1 Notes

TA: 郑浩 (RA in SUSTech CV Lab)

### Prerequisites

1. Server IP, username

2. Access to server using terminal

   ```shell
   ssh username@host -p 10022
   ```

3. Conda installation

   ```shell
   # Download Anaconda3 Installer
   wget http://mirrors.sustc.us/anaconda/archive/Anaconda3-2020.07-Linux-x86_64.sh
   
   # Give execution permission
   chmod 777 Anaconda3-2020.07-Linux-x86_64.sh
   
   # Install
   ./Anaconda3-2020.07-Linux-x86_64.sh
   
   # Activate environment variable
   source ~/.bashrc
   ```

4. Conda & pip mirror setting

   - Conda: 

     1. `vim ~/.condarc` 

     2. press `i` to enter insert mode

     3. copy and paste

        ```json
        channels:
          - defaults
        show_channel_urls: true
        channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
        default_channels:
          - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
          - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
          - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
          - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
          - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
        custom_channels:
          conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
          msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
          bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
          menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
          pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
          simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
        ```
     
     4. `ESC`, `:`, `wc` to save and exit
   
   - pip: 
   
     1. `vim ~/.pip/pip.conf`  (if `~/.pip` folder not exist, create it using `mkdir ~/.pip`)
   
     2. press `i` to enter insert mode
   
     3. copy and paste
   
        ```json
        [global]
        index-url = https://pypi.tuna.tsinghua.edu.cn/simple
        ```
   
     4. `ESC`, `:`, `wc` to save and exit
   
5. Conda environment

   ```shell
   # Create your conda environemnt with python version 3.8
   conda create -n [your env name] python=3.8
   
   # Activate your environment
   conda activate [your env name]
   ```



### Jupyter Lab

0. Activate your environment

   ```shell
   conda activate [your env name]
   ```

1. Install jupyter and required packages

   ```shell
   conda install jupyterlab numpy matplotlib
   
   # opencv-python can not be installed by conda
   pip install opencv-python
   ```

2. Run jupyter in **server terminal**

   ```shell
   jupyter lab --no-browser --port=PORT_NUM # 1024-65535
   ```

   $PORT\_NUM = 1024 + (SID \mod (65535-1024)) = 1024 + (SID \mod 64511)$

3. Run SSH port forwarding in **local terminal**

   ```powershell
ssh -N -f -L localhost:8888:localhost:PORT_NUM username@serverIP -p 10022
   ```
   
   *Check the explanation of command here:* https://explainshell.com/explain?cmd=ssh+-N+-f+-L+localhost%3A8888%3Alocalhost%3APORT_NUM+username%40serverIP+-p+10022#
   
4. Access jupyter lab by visit `localhost:8888`

5. Download course materials from github

   ```
   wget https://github.com/zh-plus/SUSTech-CS308/raw/master/Lab1/lab1.ipynb
   wget https://github.com/zh-plus/SUSTech-CS308/raw/master/Lab1/lenna.jpg
   ```

   
