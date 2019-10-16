# modbusPlcSimulator
modbus服务器模拟程序

![screenshot.png](https://raw.githubusercontent.com/alongL/modbusPlcSimulator/master/imgs/screenshot.png "运行窗口")
![screenshot.png](https://raw.githubusercontent.com/alongL/modbusPlcSimulator/master/imgs/screenshot-register.png "寄存器窗口"

## 一、用途
+ 主要用来模拟modbus设备，通过配置文件，一次可以模拟多台设备，一键启机和停机。
+ 可以查看寄存器和modbus访问日志log。
+ 通过提供_data.csv文件，支持数据自动刷新。

## 二、使用方法
+ 编译后将config目录复制到可执行文件目录下，正确配置csv文件后，即可使用
+ 点击播放窗口的播放按钮后数据才会根据csv进行刷新，刷新时数据是从 _data.csv中选取一行进行刷新。
+ 不要关闭播放窗口，目前关闭播放窗口会结束数据刷新线程。
+ 可以在日志窗口查看modbus协议底层访问情况，modbus读写都有记录。


## 三、原理
+ plc对外提供的是modbus协议，可以通过提供modbus服务模拟。以前主要是用modsim进行模拟，这种方式一次只能模拟一台设备，且操作起来相对比较麻烦。此程序操作简单，使用方便，只需运行，即可以同时模拟一个风场的多台，方便进行采集软件调试。
+ 以前只能采用数据转发的方式，只能以现有数据为条件进行测试，并且不能测试数据采集和控制功能。现在可以在任何一台机器上搭建模拟的设备环境，进行数据采集和控制测试。
+ 以后还可以添加更多的功能，比如自动模拟设备运行等。

## 四、配置文件介绍 
+ app.cfg 指定程序启动时加载的设备配置文件，默认是default.csv，在config目录下。
+ default.csv配置一个风场中所有的类型和在本地模拟modbus所监听的端口。端口一般用1501，1502。。。。等等，避免与系统中其他程序所使用的端口相冲突。
+ PCS.csv 配置模拟一台PCS设备所用的modbus寄存器的类型和值。
+ PCS_data.csv 是每秒要刷新的数据。

## 五、注意事项
+ 1.地址
 modbus协议所用的地址比实际地址多1。 用modscan查看时显示的地址+1，建议在配置文件app.cfg中设置 offsetAddOne=1

+ 2.值类型
 目前INT型是作为16位1个寄存器处理。
 32位INT请用DWORD
 FLOAT当作32位处理。
 REAL作为32浮点数处理。


## 六、TODO
+ 1.寄存器察看器中显示浮点数的数值
+ 2.按位设置变量的值



