## YOLOv5部署

实现YOLOv5使用tensorrt加速，yolov5为[ultralytics/yolov5](https://github.com/ultralytics/yolov5)的[yolov5 releasev3.1](https://github.com/ultralytics/yolov5/releases/tag/v3.1)pytorch版本。

其他版本，请参考[tensorrtx](https://github.com/wang-xinyu/tensorrtx/tree/master/yolov5)的版本。

运行前，请确保已经正确配置好所需环境。

### 配置

- 在`yolov5.cpp`中第13行的NET定义中选择模型的大小s/m/l/x，同时也可以设置BATCH_SIZE，CONF_THRESH等

- `yolov5.cpp`中定义使用FP16/FP32，GPU id

- 在`yololayer.h`中设置类别CLASS_NUM，高INPUT_H和宽INPUT_W

- `yololayer.cu`中第272-274行设置类别，高和宽

### 运行
```
1. 设置`gen_wts.py`中的第8行为需要转为tensorrt模型权重文件，复制gen_wts.py到yolov5的项目根目录下

python gen_wts.py
// 生成wts文件并将其移到该目录的根目录下

2. build并运行

//确保已经完成参数配置

mkdir build
cd build
cmake ..
make
sudo ./yolov5 -s             // 序列化模型并将其保存为'yolov5s.engine'


3. 推理
sudo ./yolov5 -d  ../samples // 使用c语言运行推理samples目录下的文件

python yolov5_trt.py //使用python运行推理samples目录下的文件
```
