一个图片/视频换脸项目

# 安装
1. python 3.10 `pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/`
2. 下载ffmpeg，并将其`ffmpeg/bin`添加到系统环境变量
3. 使用 Visual Studio 安装C++扩展内容
4. 保持联网并开启VPN，因首次运行会自动从外网下载模型文件

***
# 运行
##### cpu基础用法（UI）
```
python run.py
```

##### gpu建议用法（UI）
使用 NVIDIA gpu 运行（需安装CUDA）
```
python run.py --execution-provider cuda --execution-threads=4
```

##### 命令行用法
```
python run.py -s F:\roop\media\input\kimball1.png -t F:\roop\media\input\alpha.mp4 -o F:\roop\media\output\alpha.mp4 --execution-provider cuda --execution-threads=4
```

##### 运行参数（详见 https://github.com/s0md3v/roop/wiki/）
* -h, --help                                               show this help message and exit
* -s SOURCE_PATH, --source SOURCE_PATH                     select an source image
* -t TARGET_PATH, --target TARGET_PATH                     select an target image or video
* -o OUTPUT_PATH, --output OUTPUT_PATH                     select output file or directory
* --frame-processor FRAME_PROCESSOR [FRAME_PROCESSOR ...]  frame processors (choices: face_swapper, face_enhancer, ...)
默认为 face_swapper 用于替换人脸。也可以用face_enhancer，通过GFPGAN增强修复模糊人脸。两者也可一起使用。
* --keep-fps：默认为 False，按 30 fps导出结果。
如为 True 则保持原视频 fps。
* --keep-audio：默认存在，保留原始音频
* --keep-frames：默认为 False，不保留原视频帧的中间临时文件
* --many-faces：默认为 False，只修改一帧画面中最靠左的脸
* --video-encoder：默认为 libx264，可选择 libx265, libvpx-vp9
* --video-quality：默认为18，可选择 1 ~ 51。数字越小质量越高
* --max-memory：最大允许使用的内存空间GB数，默认值由系统自动生成。
* --execution-provider：默认为cpu。根据本地拥有的 onnxruntime provider 自行选择：
cuda: for NVIDIA
rocm: for AMD (linux only)
dml: for windows
coreml: for mac
* --execution-threads：并行线程数，默认值由系统自动生成。
当出现`Non zero status code...` 或 `Cannot allocate memory...`报错即显存不足，可调小该值。


***
# 关闭NSFW屏蔽
NSFW内容检测位于 predicter.py 中的 predict_image, predict_video
注释掉 core.py 中相关的检测退出行为即可
