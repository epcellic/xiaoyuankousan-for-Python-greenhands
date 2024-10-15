小猿搜题的目前算法主要有三种
1.机器视觉识别与模拟操作（速度最慢）
2.抓包加模拟操作（速度稍稍快）
3.改包加模拟操作（速度稍快）
4.直接提交值（速度最快）
其中抓包会出现断网的情况，需要自行进行证书验证，逆向提交值有点困难，目前貌似有不完整的逆向笔记。

我将会具体介绍一下第一种入门的算法

首先做好准备

安装屏幕ocr工具
打开网址
[tesseract图片识别软件](https://github.com/UB-Mannheim/tesseract/wiki)
安装程序
tesseract-ocr-w64-setup-5.4.0.20240606.exe （64 位）
安装后记住你的程序放置路径，稍后会用
设置——系统——高级系统设置——环境变量——（在“系统变量”栏找到变量：path，然后编辑新建一个——添加含有tesseract程序的路径即可）
[环境变量是干啥的？](https://www.bilibili.com/video/BV1w741147G9/?share_source=copy_web&vd_source=071f818f573a671f858e22c968842a24)

然后你还得知道你的设备屏幕的坐标，方便后续截屏定位
这个咋办？下面网站直接解决
[屏幕坐标定位器网页](https://zhangweixi.cc/static/windows-xy.html)

然后打开你的终端安装一下第三方库，
keyboard（监听键盘操作，这个用来终止程序的，如果方便其他方式终止，可以把这个库及其代码去掉）
pillow（图像处理库，会用它的ImageGrab来截图）（即调用时导入的PIL）
pyautogui(自动化键鼠操作)
OpenCV(计算机视觉与机器学习，会用到其中的cv2)
pytesseract（ocr识别）
比如这样pip install keyboard
安装完成后开始编写我们的程序
python文件含具体注释已放于目录，我们另行教学


