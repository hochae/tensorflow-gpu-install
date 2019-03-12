# tensorflow-gpu-install
summary of tensorflow-gpu install


# TensorFlow-gpu
  - ## Install Anaconda
    - Download Anaconda from [hear](https://www.anaconda.com/distribution/#download-section)
      - install anaconda(version: 4.5.12): setup environment manually
        - select 'no' for auto setup environment by installer
      ```
      # run install script
      bash Anaconda3-5.1.0-Linux-x86_64.sh
      
      # add path into .bashrc : export PATH="/home/dbk/anaconda3/bin:$PATH"
      sudo vi ~/.bashrc
      
      # set path with runing .bashrc
      source ~/.basherc
      ```      
      - create conda virtual environment
      ```
      conda create --name tf-gpu
      ```
      - tensorflow tools versions from conda install
        - python-3.6.8
        - pip-19.0.3
        - tensorflow-1.12.0
        - tensorflow-gpu-1.12.
        - cudnn-7.3.1
        - cudatoolkit-9.2
        
      - install tensorflow-gpu
      ```
      # activate ven
      source activate tf-gpu
      
      # install tensorflow-gpu
      conda install tensorflow-gpu
      ```
      ```
      # captured printout
      Downloading and Extracting Packages
      protobuf-3.6.1       | 616 KB    | ##################################### | 100% 
      markdown-3.0.1       | 107 KB    | ##################################### | 100% 
      tensorflow-1.12.0    | 3 KB      | ##################################### | 100% 
      python-3.6.8         | 34.4 MB   | ##################################### | 100% 
      numpy-1.16.2         | 49 KB     | ##################################### | 100% 
      libedit-3.1.20181209 | 188 KB    | ##################################### | 100% 
      cupti-9.2.148        | 1.7 MB    | ##################################### | 100% 
      ca-certificates-2019 | 126 KB    | ##################################### | 100% 
      werkzeug-0.14.1      | 423 KB    | ##################################### | 100% 
      mkl_random-1.0.2     | 407 KB    | ##################################### | 100% 
      c-ares-1.15.0        | 98 KB     | ##################################### | 100% 
      tensorflow-gpu-1.12. | 2 KB      | ##################################### | 100% 
      hdf5-1.10.4          | 5.3 MB    | ##################################### | 100% 
      keras-preprocessing- | 52 KB     | ##################################### | 100% 
      grpcio-1.16.1        | 1.1 MB    | ##################################### | 100% 
      numpy-base-1.16.2    | 4.4 MB    | ##################################### | 100% 
      cudnn-7.3.1          | 334.6 MB  | ##################################### | 100% 
      wheel-0.33.1         | 39 KB     | ##################################### | 100% 
      astor-0.7.1          | 43 KB     | ##################################### | 100% 
      mkl_fft-1.0.10       | 170 KB    | ##################################### | 100% 
      scipy-1.2.1          | 17.7 MB   | ##################################### | 100% 
      openssl-1.1.1b       | 4.0 MB    | ##################################### | 100% 
      absl-py-0.7.0        | 156 KB    | ##################################### | 100% 
      tensorflow-base-1.12 | 216.9 MB  | ##################################### | 100% 
      certifi-2018.11.29   | 146 KB    | ##################################### | 100% 
      six-1.12.0           | 22 KB     | ##################################### | 100% 
      keras-applications-1 | 49 KB     | ##################################### | 100% 
      gast-0.2.2           | 138 KB    | ##################################### | 100% 
      tensorboard-1.12.2   | 3.1 MB    | ##################################### | 100% 
      setuptools-40.8.0    | 647 KB    | ##################################### | 100% 
      libprotobuf-3.6.1    | 4.1 MB    | ##################################### | 100% 
      _tflow_select-2.1.0  | 2 KB      | ##################################### | 100% 
      termcolor-1.1.0      | 7 KB      | ##################################### | 100% 
      pip-19.0.3           | 1.9 MB    | ##################################### | 100% 
      h5py-2.9.0           | 1.2 MB    | ##################################### | 100% 
      cudatoolkit-9.2      | 351.0 MB  | ##################################### | 100% 
      Preparing transaction: done
      Verifying transaction: done
      Executing transaction: done
      ```
      - Jupyter notebook kernel for tensorflow
      ```
      # take following steps in ven
      # install ipykernel
      conda install ipykernel
      
      # create jupyter kernel
      python -m ipykernel install --user --name tf-gpu --display-name "TensorFlow-GPU"
      
      # start jupyter notebook in vnc
      jypyter notebook
      
      # enjoy tensorflow... ;)
      ```
      - python versions
        - bfore anaconda install 
          - 16.04: python: 2.7.12, pip: not installed / python3: 3.5.2
        - after anaconda install
          - 16.04: python: 3.7.1 pip: 18.x
    - Ref
      - [Tensorflow easy install with conda](https://www.pugetsystems.com/labs/hpc/Install-TensorFlow-with-GPU-Support-the-Easy-Way-on-Ubuntu-18-04-without-installing-CUDA-1170/)
      - [conda-forge](https://stackoverflow.com/questions/33646541/tensorflow-and-anaconda-on-ubuntu)

# NVIDIA(GTX-1060) driver install on ubuntu 16.04
  - NVIDIA last version driver is support CUDA 10.1 but tensorflow-gpu is looking for 10.0
    - need to update the older version: decided to use 410.xx version: download [hear](https://www.nvidia.com/download/driverResults.aspx/142569/en-us)
    - To install this version we have to turn off nouveau first
    - And then install the driver after turning off X and lightdm
    ```
    # turn off nouveau
    sudo bash -c "echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
    sudo bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
    sudo update-initramfs -u
    sudo reboot
    
    # get into terminal mode: ctrl + alt + F1
    # and then turn off lightdm/gdm3
    sudo service lightdm stop
    
    #enter runlevel 3
    #sudo init 3  # rmoved and confirmed @2019.3.11
    
    # install driver
    chmod +x ./your-nvidia-file.run
    sudo ./your-nvidia-file.run
    
    # reboot 
    sudo reboot now
    ```
    - Ref
      - [Installing the NVIDIA Driver](http://us.download.nvidia.com/XFree86/Linux-x86_64/410.104/README/installdriver.html)
      - [turn off nouveau]()
      - [turn off lightdm]()
      - [init level](https://www.geeksforgeeks.org/run-levels-linux/)

## VNC connection
  - vnc connection with vino
    - enable desktop sharing
    - take following procedure
    ```
    # disable encryption
    gsettings set org.gnome.Vino require-encryption false
    
    # start vino server
    /usr/lib/vino/vino-server &
    ```
      - Ref
        - enable desktop sharing: [16.04](https://www.howtoforge.com/configure-remote-access-to-your-ubuntu-desktop), [18.04](https://websiteforstudents.com/access-ubuntu-18-04-lts-beta-desktop-via-vnc-from-windows-machines/)
        - [disable encryption](https://wiki.archlinux.org/index.php/Vino)
    
