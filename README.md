# jetson-trt-pose-training
How to training the pose new mode
### Step 1 - Install pc system for unbuntu18.04 LTS
1.You need a good pc hardware to prepare training.I use gpu is RTX3070,cpu is AMD64.
2.PCos is unbuntu18.04 LTS (64-bit PC (AMD64) desktop image)[this guide](http://old-releases.ubuntu.com/releases/18.04.4/)
### Step 2 - Install GPU device
1.you should download the nvidia device [connect](https://www.nvidia.cn/Download/index.aspx?lang=cn),according your GPU model,my device is NVIDIA-Linux-x86_64-460.27.04
2.remove old device
    ```python
    sudo apt-get remove --purge nvidia-* 
    sudo apt-get remove --purge "*nvidia*" 
    
    ```
3.


    
