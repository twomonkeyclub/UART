
UART验证
===============
验证相当于重新设计一个UART，但是实现方式灵活，怎么方便怎么来，不用考虑可综合性。在大部分IC设计公司设计和验证人员是分开的，避免设计人员对自己设计的模块进行验证，出现思维陷阱。

## 文件结构

* UART_top.v                    -----------------------testbench top层
	* UART_baud.v             ----------------波特率产生模型
	* uart_rx_model.v         -------------数据接收模型
	* check_int.v                -------------------数据对比
		* reg_op.v                ----------------寄存器操作 
	* tc_01_00.v                 -------------------testcase1
	* tc_02_00.v                 -------------------testcase2
	* tc_03_00.v                 -------------------testcase3
	* uart_tx_model.v         -------------数据发送模型


## 仿真流程

* 例行化顶层
	* 目的是模拟外围使用场景。
	* 仿真模型中的RX对应到设计中的TX，仿真模型中的TX对应设计中的RX。
* 仿真通用流程
	* 进行信号的初始化，通过调用不同的testcase验证不同的功能。
	* testcase中调用reg_op中的读写寄存器任务，模拟APB时序，进行不同的寄存器配置。
	* 配置完成后调用数据发送模型向uart模块发送数据，设计中接收该数据，通过中断上报状态，数据对比模型通过读取数据寄存器，与发出的数据进行对比。
* 其他功能验证
	* 仿真数据通路正常后，通过对中断功能、中断触发深度、数据发送间隔等可配置功能进行配置验证，确保其功能正常。
