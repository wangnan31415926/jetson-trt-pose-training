# jetson-trt-pose-training
How to training the pose new mode
### Step 1 - Install pc system for unbuntu18.04 LTS
1.You need a good pc hardware to prepare training.I use gpu is RTX3070,cpu is AMD64.
2.PCos is unbuntu18.04 LTS (64-bit PC (AMD64) desktop image)[this guide](http://old-releases.ubuntu.com/releases/18.04.4/)
### Step 2 - Install GPU device
1. 最新驱动并下载 [connect](https://www.nvidia.cn/Download/index.aspx?lang=cn),according your GPU model,my device is NVIDIA-Linux-x86_64-460.27.04
2. 若已经安装了相关版本的版本，使用以下命令进行删除

    ```python
    sudo apt-get remove --purge nvidia-* 
    sudo apt-get remove --purge "*nvidia*" 
    ```    
3. 禁用Nouveau
    ```python
    sudo vim /etc/modprobe.d/blacklist.conf 
    ``` 
   在文件末尾输入：blacklist nouveauoptions nouveau modeset=0,接着，保存文件并退回终端
4. 执行以下命令进行更新：
   ```python
   sudo update-initramfs -u
   ```   
5.最后，重启电脑。若再在终端输入 ```lsmod | grep nouveau```命令无输出，则表示禁用成功.
6.安装依赖 ```sudo apt-get install build-essential gcc-multilib dkms```
7.关闭图形界面 
  ```
  sudo systemctl set-default multi-user.target
  sudo reboot
  ```
8.进入驱动下载的目录下
  ```
  cd Downloads
  sudo chmod a+x NVIDIA-Linux-x86_64-460.27.04.run     # 给驱动run文件赋予执行权限，驱动版本号自行修改
  sudo ./NVIDIA-Linux-x86_64-384.130.run -no-x-check -no-nouveau-check -no-opengl-files #开始安装驱动
  ```
  注意: -no-x-check：安装驱动时关闭X服务
       -no-nouveau-check：安装驱动时禁用nouveau
       -no-opengl-files：只安装驱动文件，不安装OpenGL文件
9.重启电脑
  ```
  sudo systemctl set-default graphical.target
  sudo reboot
  ```
10.验证安装驱动是否OK
  ```
      nvidia-smi
      nvidia-settings
  ```
  
  
  
  
  
  
  
  
  
  
  
