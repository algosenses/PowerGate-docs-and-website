## 运行模式
PowerGate支持以两种模式运行交易策略：  
一是策略以动态链接库（.dll或.so）形式存在，PowerGate网关直接将其加载到进程内部。 
	
				+--------------------------+
				|              +--------+  |
				|              |Strategy|  |
				|              +--------+  |
				|              +--------+  |
				| PowerGate    |Strategy|  |
				|              +--------+  |
				|              +--------+  |
				|              |Strategy|  |
				|              +--------+  |
				+--------------------------+

二是策略以独立进程存在，PowerGate网关通过网络为策略提供运行环境，也就是典型的Client/Server模式。  

				+------------+
				|            |          +--------+
				|            |<-------->|Strategy|
				|            |          +--------+
				|            |          +--------+
				| PowerGate  |<-------->|Strategy|
				|            |          +--------+
				|            |          +--------+
				|            |<-------->|Strategy|
				|            |          +--------+
				+------------+

PowerGate默认以第二种模式运行。网关程序的默认监听端口为5501，用户可以通过登录界面的“设置”按钮修改监听端口。
## 事件驱动
策略以“事件驱动”的方式运行。用户继承SDK提供的策略父类之后，根据需要实现相应的事件接口，当对应的事件发生时，策略的事件接口会被调用。  
例如用户对Tick行情数据感兴趣，只要实现onTick()接口，当有Tick数据到来时，onTick()就会被调用。  
用户可以在PowerGate的界面上控制策略的运行与停止，当策略启动或停止时，对应的回调函数也会被调用。  
在事件驱动的模式下，一个交易策略的典型生命周期如下：  

		+-------+         +-----------+                                    +-----------+
		| User  |         | PowerGate |                                    | Strategy  |
		+-------+         +-----------+                                    +-----------+
		    |                   |                                                |
		    | 加载策略           |                                                |
		    |----------------->>|                                                |
		    |                   |                                                |
		    |                   |                                    onCreate()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    | 启动策略           |                                                |
		    |----------------->>|                                                |
		    |                   |                                                |
		    |                   |                              onSetParameter()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |                                     onStart()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |                                      onTick()  |  # 如果策略订阅了Tick
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |                                       onBar()  |  # 如果策略订阅了Bar
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |  buy()/sell()/sellShort()/cover()              |  # 策略发送报单
		    |                   |<<----------------------------------------------|
		    |                   |                                                |
		    |                   |                            onOrderSubmitted()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |            onOrderUpdated()/onOrderRejected()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |                           onExecutionReport()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |      onOrderPartiallyFilled()/onOrderFilled()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    | 停止策略           |                                                |
		    |----------------->>|                                                |
		    |                   |                                                |
		    |                   |                                      onStop()  |
		    |                   |---------------------------------------------->>|
		    |                   |                                                |
		    |                   |                                    onDestory() |
		    |                   |----------------------------------------------->|
		    |                   |                                                |

## 数据序列
PowerGate为用户提供了一个有用的抽象：数据时间序列（DataSeries）。  
例如，用户需要订阅某合约的一分钟数据，只要在策略配置中写：  

	config.subscribe("ABC", Resolution.MINUTE, 1)
系统会为策略自动生成一个周期为1分钟的"ABC"合约的时间序列，这个序列会被自动填充。当有分钟数据生成时，序列的第0个数据就是最新数据。  
这个时间序列能被用于各种运算，如：判断相互穿越，用于传递给技术指标如MA、EMA等。  
例如，我们可以在一个数据序列上计算周期为10的SMA指标：  

	from PowerGate import SMA
	sma = SMA()
	sma.init(series, 10)  
当有新数据被填充进序列时，数据序列会自动触发指标进行计算。用户在初始化完指标之后，指标会自动接收数据计算最新值。
## 策略持仓
PowerGate支持同时运行多个策略，不同于账户持仓，每个策略都有属于自己的持仓。  
当策略开仓时，所开的仓位会被分配给这个策略。PowerGate网关记录每个策略的持仓数量，策略默认只能平掉属于自己的持仓。  
用户可以在网关界面上或者在策略内部为策略分配持仓。
