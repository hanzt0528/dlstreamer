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
1) dowload dlstreamer https://github.com/dlstreamer/dlstreamer tag:v1.6
2) build
      # cmake
      mkdir ~/intel/dlstreamer_gst/build
      cd ~/intel/dlstreamer_gst/build
      cmake -DCMAKE_INSTALL_PREFIX=/opt/intel_test/dlstreamer_build  ..

      # make
      make -j
      sudo make install
      
4)config
export GST_PLUGIN_PATH=/opt/intel_test/dlstreamer_build/lib:$GST_PLUGIN_PATH
export LD_LIBRARY_PATH=/opt/intel_test/dlstreamer_build/lib:$LD_LIBRARY_PATH

5)test

export DETECTION_MODEL=${MODELS_PATH}/intel/person-vehicle-bike-detection-2004/FP32/person-vehicle-bike-detection-2004.xml
export DETECTION_MODEL_PROC=/opt/intel/dlstreamer/samples/model_proc/intel/person-vehicle-bike-detection-2004.json
export VEHICLE_CLASSIFICATION_MODEL=${MODELS_PATH}/intel/vehicle-attributes-recognition-barrier-0039/FP32/vehicle-attributes-recognition-barrier-0039.xml
export VEHICLE_CLASSIFICATION_MODEL_PROC=/opt/intel/dlstreamer/samples/model_proc/intel/vehicle-attributes-recognition-barrier-0039.json

export VIDEO_EXAMPLE=person-bicycle-car-detection.mp4
gst-launch-1.0 \
filesrc location=${VIDEO_EXAMPLE} ! decodebin ! \
gvadetect model=${DETECTION_MODEL} model_proc=${DETECTION_MODEL_PROC} device=CPU ! queue ! \
gvawatermark ! videoconvert ! avenc_mpeg4 ! mp4mux ! filesink location= ./out_pipeline1.mp4 sync=false

      
      
