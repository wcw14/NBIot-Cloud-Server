# NBIot-Cloud-Server
NB-Iot project including a cloud server


    该项目分为两部分，第一部分是云平台，第二部分是硬件部分。
  目前硬件部分只支持Stm32f10x系列，如果适配其他的STM32系列只需要一直对应的NB驱动库即可，此驱动库借鉴了谷雨物联网的例子，如果需要移植到其他的系列，请参考textNB的子项目或者前往谷雨物联网参考他们家的例子。

  第一部分由前端后台和数据库构成，前端对应的是NBIot子项目，后台对应的是NBIotServer子项目。前端采用Vue.js开发，后端采用Node.js开发。具体技术可参考pdf文档。数据库采用MongoDB，具体的集合设计也可参考pdf文档。

  目前以实现UDP和CoAP协议的通信，本项目将保持更新，后续会支持MQTT、TCP等协议，并支持Adruino、树莓派、ARM9以上等硬件。

  前端后台部署需要先运行```cnpm i```安装所有依赖的模块。


目前测试硬件为stm32f103c8t6+bc95-b8(移动sim卡)。由于电信限制sim卡的对个人服务器的访问，电信的暂时不支持，如果您的服务器已经加入了电信白名单，那应该也是可以正常通信的。





# 关于如何部署该云平台

后端采用node开发，有两种办法可以运行服务端程序。
首先，需要在服务端安装node环境，关于如何安装，请根据不同的操作系统自己寻找教程，之后进行下一步。
1. 第一种，进入NBIotServer文件夹，运行`cnpm i --save`，安装好依赖包。之后运行`node bin/www`命令即可，此时服务端已运行。
2. 第二种，使用pm2进行运维。首先安装pm2工具，之后运行`pm2 start 路径/NBIotServer/bin/www`，此时服务端已运行。
