
UART设计与验证
===============
实现一个在ARM中通过APB总线连接的UART模块（Universal Asynchronous Receiver/Transmitter）模块，包括设计与验证两部分。

## 项目需求

> * 系统时钟最大工作频率满足100MHz，功能时钟满足26MHz
> * 具有系统和功能时钟域的复位功能
> * 配置接口满足AMBA2.0-APB总线接口时序，总线位宽16bit
> * 数据传输满足通用串口时序，奇偶校验功能可配置
> * 波特率满足115200，或可配置
> * 接收和发送FIFO复位单独可控，触发深度可配置
> * 数据收发中断功能可配置
> * 数据发送间隔可控
> * 具有状态指示功能
> * 具有FIFO数据量指示功能

## 设计
* **波特率产生模块**
	* 根据功能时钟和配置，产生收发波特率时钟。
* **数据接收**
	* 根据RX波特率时钟接收数据，进行奇偶校验，存放数据到RX FIFO，再由CUP经过APB总线读取数据。内含接收数据状态机。
* **数据发送**
	* CUP通过APB总线将需要发送的数据放到TX FIFO，根据TX波特率时钟进行数据发送。内含发送数据状态机。
* **寄存器配置**
	* 实现APB读写寄存器功能，中断操作，功能选择，模块状态指示等。


## 验证

* **波特率产生**
	* 产生仿真环境使用的波特率时钟。
* **数据接收**
	* 仿真环境的接收数据模型。
* **数据发送**
	* 仿真环境的发送数据模型。
* **APB总线**
	* 仿真环境的APB总线模型，模拟cpu响应中断和实现各种功能。
* **数据对比**
	* 根据对比发送和接收的数据和时序，产生不同的对比结果，便于仿真时对结果的观察。
* **Testcase产生**
	* 通过不同的激励或配置产生不同的case，验证时序和功能是否符合。


框架
-------------
<div align=center><img src="https://github.com/twomonkeyclub/UART/blob/master/utils/frame.png" height="200"/> </div>


更多资料
------------
请关注公众号 **“两猿圈”**.
> * **带你丰富IC相关项目经验，轻松应对校招！！！**
> * **项目模块详细讲解，在公众号内持续更新！！！**

<div align=center><img src="https://github.com/twomonkeyclub/TinyWebServer/blob/master/root/test1.jpg" height="258"/> </div>
