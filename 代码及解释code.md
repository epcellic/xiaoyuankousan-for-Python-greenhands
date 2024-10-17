#没想到上传本地文件稍有麻烦，我就先放文本代码在这里了，稍后我会配置git和ssh后加入py文件，希望对你有帮助。
记得用代码格式看，不然可太乱了

import math
import sys
import keyboard  # 用于检测键盘按键
from PIL import ImageGrab  # 用于捕捉屏幕图像
import pyautogui  # 用于模拟鼠标和键盘操作
import cv2  # OpenCV库，用于图像处理
import pytesseract  # 用于OCR文字识别
    # 设置tesseract的路径，确保你的系统中安装了tesseract，并且路径正确
pytesseract.pytesseract.tesseract_cmd = r'D:\tesseract\tesseract.exe'
while True:
    # 检测是否按下了空格键，如果按下则退出程序
    if keyboard.is_pressed('space'):
        print('识别结束')
        sys.exit()
    # 使用ImageGrab捕捉屏幕的特定区域，bbox参数定义了捕捉区域的左上角和右下角的坐标   
    ImageGrab.grab(bbox=(209,472,650,574)).save('num.png')
    # 使用OpenCV读取刚才保存的图像文件
    img = cv2.imread('num.png')
    # 将图像转换为灰度图，这有助于后续的二值化处理
    img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    # 使用阈值处理将图像转换为二值图，150是阈值，100是最大值，THRESH_BINARY是阈值类型
    _, thresh = cv2.threshold(img, 150, 255, cv2.THRESH_BINARY)

    # 使用pytesseract进行OCR识别，config参数设置为'--psm 6'，这是页面分割模式的一种
    result = pytesseract.image_to_string(thresh, config='--psm 6').split('?')

    try:
        # 去除结果字符串两端的空白字符
        result[0] = result[0].strip()
        result[1] = result[1].strip()

        # 将识别到的字符串转换为浮点数，然后向下取整为整数
        num1 = math.floor(float(result[0]))
        num2 = math.floor(float(result[1]))

        # 移动鼠标到指定的坐标位置
        pyautogui.moveTo(x=277, y=700, duration=0.1)
        # 比较两个数字的大小，并根据比较结果执行不同的鼠标操作
        if num1 > num2:
            pyautogui.mouseDown()
            pyautogui.move(xOffset=100, yOffset=100, duration=0.1)
            pyautogui.move(-100, yOffset=100, duration=0.1)
            pyautogui.mouseUp()
            print(f'{num1}  >  {num2}')
        else:
            pyautogui.mouseDown()
            pyautogui.move(-100, yOffset=100, duration=0.1)
            pyautogui.move(xOffset=100, yOffset=100, duration=0.1)
            pyautogui.mouseUp()
            print(f'{num1}  <   {num2}')
    except IndexError:
        # 如果result列表中没有两个元素，则打印错误信息
        print('未捕获到内容，可能是OCR识别错误')
    except ValueError:
        # 如果转换数字失败，则打印错误信息
        print('未捕获到内容，可能是非数字字符')
