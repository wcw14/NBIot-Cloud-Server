# NBIot-Cloud-Server
NB-Iot project including a cloud server


    该项目分为两部分，第一部分是云平台，第二部分是硬件部分。
  目前硬件部分只支持Stm32f10x系列，如果适配其他的STM32系列只需要一直对应的NB驱动库即可，此驱动库借鉴了谷雨物联网的例子，如果需要移植到其他的系列，请参考textNB的子项目或者前往谷雨物联网参考他们家的例子。

  第一部分由前端后台和数据库构成，前端对应的是NBIot子项目，后台对应的是NBIotServer子项目。前端采用Vue.js开发，后端采用Node.js开发。具体技术可参考pdf文档。数据库采用MongoDB，具体的集合设计也可参考pdf文档。

  目前已实现UDP和CoAP协议的通信，本项目将保持更新，后续会支持MQTT、TCP等协议，并支持Adruino、树莓派、ARM9以上等硬件。

  前端后台部署需要先运行```cnpm i```安装所有依赖的模块。


目前测试硬件为stm32f103c8t6+bc95-b8(移动sim卡)。由于电信限制sim卡的对个人服务器的访问，电信的暂时不支持，如果您的服务器已经加入了电信白名单，那应该也是可以正常通信的。


----


# 关于如何部署该云平台

## 后端程序部署
后端采用node开发，有两种办法可以运行服务端程序。
首先，需要在服务端安装node环境，关于如何安装，请根据不同的操作系统自己寻找教程，之后进行下一步。
1. 第一种，进入NBIotServer文件夹，运行`cnpm i --save`命令，安装好依赖包。之后运行`node bin/www`命令即可，此时服务端已运行。
2. 第二种，使用pm2进行运维。首先安装pm2工具，之后运行`pm2 start 路径/NBIotServer/bin/www`，此时服务端已运行。

##### 注意
1. 服务端目前只能实现一次CoAP的通信流程，之后需要重新运行才可以重新通信，主要是端口变了没改回来，需要后续优化代码才可以。
2. 服务端需要用到MongoDB，所以需要自己安装MongoDB，并根据需要更改后端关于MongoDB的设置，即数据库，document和账号密码。


## 前端部署
前端采用vue开发，同样需要运行`cnpm i --save`命令安装所需的模块，前端可在本地部署或者服务器部署，已采用跨域处理。之后使用`cnpm run dev`命令即可运行前端。打开浏览器，输入http://ip  即可访问网站。


## 嵌入式代码
可随意使用stm32(arm m3内核)系列的硬件烧写该项目代码，由于需要发AT指令，所以需要stm32开发板需要有串口功能(一般会有)。由于本项目stm32发送何种指令受PC端控制，而PC端也是通过串口发送自定义命令(目前是采用发送1到9的数字)给stm32，stm32辨别后根据代码再发送相应的指令给bc95模块，因此stm32开发板还需要另外一个串口，一共两个串口。
本项目采用PA9、PA10做串口1用于发送AT指令给bc95，其中PA9为USART1 TX，PA10为USART1 RX；而PA2、PA3做串口2用于发送收发PC端指令，其中PA2为USART2 TX，PA3为USART2 RX。
##### 请根据实际硬件来修改IO口的定义。
