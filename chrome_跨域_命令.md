#### Chrome 跨域 命令

open -a "Google Chrome" --args -disable-web-security --user-data-dir=


##### 替换
.replace(/^(.{3})(?:\d+)(.{2})$/,'$1**********$2')

15937136388.replace(/^(.{3})(?:\d+)(.{2})$/,'$1**********$2')==159******88
除去前三位后两位，剩余的都用*代替。



#####  shift : q         后enter 退出

#####   O 编辑   esc键退出编辑    ：wq 退出



##### scrollIntoView() 处理input被键盘挡住的情况   在移动设备上有效

##### React     http://www.react-cn.com/


##### Mac os 下面用

/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --disable-web-security

或者

open -a "Google Chrome" --args --disable-web-security


##### Ubuntu?Linux:

chromium-browser --disable-web-security

##### windows
chrome.exe --disable-web-security

##### 用命令行打开 Apple Safafi 方法是：

Mac OS 下：

open -a '/Applications/Safari.app' --args --disable-web-security

Windows：
C:\Program Files\Safari\Safari.exe --disable-web-security


##### React map循环 渲染 内容是html  使用

`dangerouslySetInnerHTML`={{__html: '从后台拿到字符串类型的标签'}}

