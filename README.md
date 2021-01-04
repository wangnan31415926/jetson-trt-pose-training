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
5. 最后，重启电脑。若再在终端输入 ```lsmod | grep nouveau```命令无输出，则表示禁用成功.
6. 安装依赖 ```sudo apt-get install build-essential gcc-multilib dkms```
7. 关闭图形界面 
  ```
  sudo systemctl set-default multi-user.target
  sudo reboot
  ```
8. 进入驱动下载的目录下
  ```
  cd Downloads
  sudo chmod a+x NVIDIA-Linux-x86_64-460.27.04.run     # 给驱动run文件赋予执行权限，驱动版本号自行修改
  sudo ./NVIDIA-Linux-x86_64-384.130.run -no-x-check -no-nouveau-check -no-opengl-files #开始安装驱动
  ```
  注意: -no-x-check：安装驱动时关闭X服务
       -no-nouveau-check：安装驱动时禁用nouveau
       -no-opengl-files：只安装驱动文件，不安装OpenGL文件
9. 重启电脑
  ```
  sudo systemctl set-default graphical.target
  sudo reboot
  ```
10. 验证安装驱动是否OK
  ```
      nvidia-smi
      nvidia-settings
  ```
### Step 3  Install Cuda Cudnn
 1.cuda(https://www.jianshu.com/p/4e8a4a07cc57?utm_campaign=haruki),()
   ```
   wget https://developer.download.nvidia.com/compute/cuda/11.1.0/local_installers/cuda_11.1.0_455.23.05_linux.run
   sudo sh cuda_11.1.0_455.23.05_linux.run
   ```
 3.cudnn(https://blog.csdn.net/public669/article/details/98470857?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control)
 
 ### Step 4  Install pytorch,torchvision 
  1.(https://pytorch.org/get-started/locally/)
 ### Step 5  Install tensorrt 
 (https://blog.csdn.net/shwan_ma/article/details/103637739/)
 ### Step 6  Install torch2trt
  ```
  git clone https://github.com/NVIDIA-AI-IOT/torch2trt
  cd torch2trt
  sudo python3 setup.py install --plugins
  ```
### Step 7 Install other miscellaneous packages
   ```
   sudo pip3 install tqdm cython pycocotools
   sudo apt-get install python3-matplotlib
   ```
### Step 8 Install trt_pose
   ```
   git clone https://github.com/NVIDIA-AI-IOT/trt_pose
   cd trt_pose
   sudo python3 setup.py install
   ```
### Step 9   Download coco
```
cd tasks/human_pose
source download_coco.sh
unzip train2017.zip
unzip val2017.zip
unzip annotations_trainval2017.zip
```   
### Step 10 Pre-process the coco annotations. This adds the "Neck" keypoint (midpoint of shoulders).
```
python3 preprocess_coco_person.py annotations/person_keypoints_train2017.json annotations/person_keypoints_train2017_modified.json

```
### Step 11 Create a model / training configuration. Easiest to start from an existing one. (https://github.com/NVIDIA-AI-IOT/trt_pose/issues/59)
```
cp experiments/resnet18_baseline_att_224x224_A.json experiments/my_model.json
python3 train.py ../tasks/human_pose/experiments/my_model.json 
```

  
  
  
  
