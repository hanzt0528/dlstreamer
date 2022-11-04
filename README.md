# dlstreamer
1Donload dlstreamer docker:

推荐方式 启用ubuntu20.04docker环境
运行docker （https://hub.docker.com/r/intel/dlstreamer/tags ）并挂载代码目录。 [2022.1.0-ubuntu20-devel]测试可用


2Download the models from Open Model Zoo

python3 -m pip install --upgrade pip
python3 -m pip install openvino-dev[onnx]
/opt/intel/dlstreamer/samples/download_models.sh

models location:/home/dlstreamer/intel/dl_streamer/models/

3build:
1 dowload dlstreamer https://github.com/dlstreamer/dlstreamer tag:v1.6
2 build
      # cmake
      mkdir ~/intel/dlstreamer_gst/build
      cd ~/intel/dlstreamer_gst/build
      cmake -DCMAKE_INSTALL_PREFIX=~/intel/dlstreamer_build  ..

      # make
      make -j
      sudo make install
      
      
      
