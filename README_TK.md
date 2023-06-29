一个图片/视频换脸项目

# 安装
1. pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/
2. 下载ffmpeg，并将其`ffmpeg/bin`添加到系统环境变量
3. 开启VPN，因首次运行会自动从外网下载模型文件


# 运行
##### 使用cpu运行
python run.py
##### 使用gpu运行
其中 --execution-threads=4 默认为8，显存较小的电脑可能无法支持
python run.py --execution-provider cuda --execution-threads=4


# 关闭NSFW屏蔽
NSFW内容检测位于 predicter.py 中的 predict_image, predict_video
注释掉 core.py 中相关的检测退出行为即可
