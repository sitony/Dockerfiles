# Docker Image for original OpenPose and Chainer OpenPose.

* Base docker image is nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
* Build command  
sudo docker build . -t saaa/openpose-gpu
* Run command   
sudo docker run --rm -it --runtime=nvidia --net=host -e DISPLAY --device=/dev/video0:/dev/video0 -v $HOME/.Xauthority:/root/.Xauthority -v /docker/notebooks:/notebooks saaa/openpose-gpu bash

* Sample command for OpenPose  
./build/examples/openpose/openpose.bin --video ./examples/media/video.avi --process_real_time  
./build/examples/openpose/openpose.bin  
./build/examples/openpose/openpose.bin --write_video output/result.avi --write_keypoint_json output/

* Sample command for Chainer OpenPose   
python3 pose_detector.py posenet models/coco_posenet.npz --img data/person.png --gpu 0
