策略SDK下载地址：  

* C++ SDK
* [Python SDK](https://sourceforge.net/projects/powergate-sdk-python/files/latest/download)
* Java SDK
* C# SDK
* R SDK
* Matlab SDK
## 数据结构
###&emsp;Resolution  
行情周期

	TICK   = 0,                 
    SECOND = 1,                
    MINUTE = 60,                
    HOUR   = 60 * 60,          
    DAY    = 24 * 60 * 60,     
    WEEK   = 24 * 60 * 60 * 7
###&emsp;ExchangeCode  
交易所代码  
 
	EXCHG_UNKNOWN = 0x00,
    EXCHG_SSE     = 0x0001,
    EXCHG_SZE     = 0x0002,
    EXCHG_SHFE    = 0x0004,
    EXCHG_DCE     = 0x0008,
    EXCHG_CZCE    = 0x0010,
    EXCHG_CFFEX   = 0x0020,
    EXCHG_GOLD    = 0x0040
###&emsp;SecurityType  
证券类型

	UNKNOWN = 0,
    STOCK,
    FUTURE,
    FOREX,
    OPTION
###&emsp;MarketData
行情数据

	char      type;
    char      securityType;
    char      instrument[LEN_INSTRUMENT];
    char      exchange[LEN_EXCHANGE];
    int       date;     // YYYYMMDD
    int       time;     // hhmmss
    int       millis;
    int       resolution;
    int       interval;
    double    lastPrice;
    double    openPrice;
    double    highestPrice;
    double    lowestPrice;
    double    closePrice;
    double    volume;
    long long openInterest;
    double    turnover;
    double    upperLimitPrice;
    double    lowerLimitPrice;
    double    preSettlePrice;
    double    preClosePrice;
    double    settlePrice;
    int       preOpenInterest;
    double    averagePrice;
    int       depth;

    double    bidPrice1;
    int       bidVolume1;
    double    bidPrice2;
    int       bidVolume2;
    double    bidPrice3;
    int       bidVolume3;
    double    bidPrice4;
    int       bidVolume4;
    double    bidPrice5;
    int       bidVolume5;

    double    askPrice1;
    int       askVolume1;
    double    askPrice2;
    int       askVolume2;
    double    askPrice3;
    int       askVolume3;
    double    askPrice4;
    int       askVolume4;
    double    askPrice5;
    int       askVolume5;
###&emsp;TimeInforce
订单时效  

	DAY = 0,
    GTC,
    OPG,
    IOC,
    FOK,
    GTX,
    GTD,
###&emsp;Order
订单

	// Buy side's original client order ID, uniqueness must be guaranteed within a single trading day.
    char          clOrdId[LEN_ID];
    // Sell side's reference for this order.
    char          ordId[LEN_ID];
    char          instrument[LEN_INSTRUMENT];
    int           exchange;
    int           type;
    int           action;
    int           timeInforce;
    bool          allOrNone;
    int           status;
    double        quantity;
    double        price;
    double        stopPx;
    double        tradedQty;
    double        avgTradedPx;
    double        lastTradedQty;
    double        lastTradedPx;
    long          date;
    long          time;
    double        commissions;
    char          stateMsg[LEN_STATE_MSG];
    bool          closeAction;          // Distinguish three closing actions.
    int           compId;               // Component who submit this order.
    int           ownerId;              // Strategy who submit this order.
    int           srvId;
###&emsp;Execution
成交信息

	char          instrument[LEN_INSTRUMENT];
    int           type;
    int           action;
    int           date;       // YYYYMMDD
    int           time;       // hhmmss
    int           millis;
    double        quantity;
    double        price;
    bool          closeAction;

    char          clOrdId[LEN_ID];
    char          ordId[LEN_ID];
    char          execId[LEN_ID];
    int           srvId;
###&emsp;OrderAction
报单方向

	BUY          = 1,
    BUY_TO_COVER = 2,
    SELL         = 3,
    SELL_SHORT   = 4,
###&emsp;OrderState
订单状态

	UNKNOWN = 0,
    INITIAL,           // Initial state.
    PENDING_NEW,
    SUBMITTED,         // Order has been submitted.
    ACCEPTED,          // Order has been acknowledged by the broker.
    PENDING_CANCEL,
    CANCELED,          // Order has been canceled.
    PARTIALLY_FILLED,  // Order has been partially filled.
    FILLED,            // Order has been completely filled.
    REJECTED           // Order has been rejected.
###&emsp;OrderType
订单类型

	MARKET     = 1,
    LIMIT      = 2,
    STOP       = 3,
    STOP_LIMIT = 4,
###&emsp;AccountDetails
账户信息

	char   userCode[32];
    char   password[32];
    char   userName[64];
    char   currency[8];
    double preBalance;
    double preDeposit;
    double margin;
    double lastFund;
    double currMargin;
    double deposit;
    double withdraw;
    double equity;
    double availFunds;
    double buyFreeze;
    double sellFreeze;
    double buyBond;
    double sellBond;
    double realizedPnL;
    double unrealizedPnL;
    double totalBond;
    double totalExBond;
    double todayReleaseFund;
    double comFreeze;
    double commission;
    double otherFreeze;
    double totalFreeze;
    double riskLevel;
###&emsp;SecurityDefinition
合约定义

	char   instrument[LEN_INSTRUMENT];
    char   name[32];
    int    exchgCode;
    double upPrice;
    double lowPrice;
    double moneyRate;
    double longMarginRatio;
    double shortMarginRatio;
    double multiplier;
    char   mktdate1[20];
    char   mktdate2[20];
    double tickSize;
    double upDealNum;
    double lowDealNum;
    int    isTrading;
###&emsp;PositionDate
仓位日期
	
	POSITION_DATE_TODAY,
    POSITION_DATE_HISTORY,
    POSITION_DATE_ALL,
###&emsp;PositionSide
仓位方向

	POSITION_SIDE_LONG  = 'L',
    POSITION_SIDE_SHORT = 'S'
###&emsp;AccountPosition
账户持仓

	char   instrument[LEN_INSTRUMENT];
    char   side;
    char   buysell;
    char   dateMark;
    double cumQty;
    double todayQty;
    double histQty;
    double frozen;
    double preSettlmntPx;
    double cost;
    double avgPx;
    double unrealizedPnL;
    double realizedPnL;
    double margin;
    int    date;
    int    time;
    int    millis;
    double histHighestPx;
    double histLowestPx;
    char   accountId[LEN_ID];
###&emsp;StrategyPosition
策略持仓
	
	int    strategyId;
    char   instrument[LEN_INSTRUMENT];
    int    side;
    double quantity;
    double frozen;
    double unformed;
    double avgPx;
    double margin;
    double unrealizedPnL;
    double realizedPnL;
    int    date;
    int    time;
    int    millis;
    double highestPx;
    double lowestPx;
###&emsp;StrategyParamType
策略参数类型

	PARAM_TYPE_BOOL,
    PARAM_TYPE_INT,
    PARAM_TYPE_FLOAT,
    PARAM_TYPE_STRING,
##StrategyBase
###&emsp;行情API

	const char* getMainInstrument() const;
    BarSeries*  getTickSeries(const char* instrument = "");
    BarSeries*  getBarSeries(const char* instrument = "", int resolution = Resolution::MINUTE, int interval = 1);
	// 订阅行情
	bool   subscribe(const char* instrument, int resolution = Resolution::TICK, int interval = 1, int srvId = 0);
	// 取消订阅
	bool   unsubscribe(const char* instrument, int resolution = Resolution::TICK, int interval = 1, int srvId = 0);
	// 获取合约乘数
	double getMultiplier(const char* instrument = "");
	// 获取合约最小跳
	double getTickSize(const char* instrument = "");
	// 获取合约最新价
	double getLastPrice(const char* instrument = "");
	// 获取合约卖一价
	double getAskPrice(const char* instrument = "");
	// 获取合约买一价
	double getBidPrice(const char* instrument = "");
###&emsp;交易API
	
	bool   openLong(const char* instrument, double quantity, char* clOrdId);
    bool   closeLong(const char* instrument, char* clOrdId);
    bool   openShort(const char* instrument, double quantity, char* clOrdId);
    bool   closeShort(const char* instrument, char* clOrdId);

	bool   buy(const char* instrument, double quantity, double price, char* clOrdId, int srvId = 0);
    bool   sell(const char* instrument, double quantity, double price, char* clOrdId, int srvId = 0);
    bool   sellShort(const char* instrument, double quantity, double price, char* clOrdId, int srvId = 0);
    bool   buyToCover(const char* instrument, double quantity, double price, char* clOrdId, int srvId = 0);

    bool   submitOrder(Order& order);
    int    getOrderStatus(const char* _clOrdId);
    Order  getOrderSnapshot(const char* _clOrdId);
    int    getPendingOrders(OrderList& list, const char* instrument = "");
    bool   cancelOrder(const char* _clOrdId);
    bool   cancelOrder(const Order& order);
    bool   isOrderPending(const char* _clOrdId);


###&emsp;持仓API
	
	int    getAccountPositions(AccountPositionList& list, const char* instrument = "");
    int    getStrategyPositions(StrategyPositionList& list, const char* instrument = "");
    double getTotalPosSize(const char* instrument = "");

    double getLongPosSize(const char* instrument = "");
    void   getLongPosSize(double* closable, double* frozen, double* unformed);
    void   getLongPosSize(const char* instrument, double* closable, double* frozen, double* unformed);
    StrategyPosition getLongPos(const char* instrument = "");

    double getShortPosSize(const char* instrument = "");
    void   getShortPosSize(double* closable, double* frozen, double* unformed);
    void   getShortPosSize(const char* instrument, double* closable, double* frozen, double* unformed);
    StrategyPosition getShortPos(const char* instrument = "");

    double getClosableLongPosSize(const char* instrument = "");
    StrategyPosition getClosableLongPos(const char* instrument = "");

    double getClosableShortPosSize(const char* instrument = "");
    StrategyPosition getClosableShortPos(const char* instrument = "");

    double getAcctClosableLongPosSize(const char* instrument = "", int srvId = 0);

    double getAcctClosableShortPosSize(const char* instrument = "", int srvId = 0);

    double getAcctLongPosSize(const char* instrument = "", int srvId = 0);
    double getAcctHistLongPosSize(const char* instrument = "", int srvId = 0);
    double getAcctLongPos(const char* instrument, double* price, int* date, int* time, int srvId = 0);
    StrategyPosition getAcctLongPos(const char* instrument = "", int srvId = 0);

    double getAcctShortPosSize(const char* instrument = "", int srvId = 0);
    double getAcctHistShortPosSize(const char* instrument = "", int srvId = 0);
    double getAcctShortPos(const char* instrument, double* price, int* date, int* time, int srvId = 0);
    StrategyPosition getAcctShortPos(const char* instrument = "", int srvId = 0);

    bool assignLongPosition(const char* instrument, double size, double price, double frozen = 0,
                            int date = 0, int time = 0, int ms = 0, 
                            double highest = 0, double lowest = 0);
    bool assignShortPosition(const char* instrument, double size, double price, double frozen = 0,
                             int date = 0, int time = 0, int ms = 0,
                             double highest = 0, double lowest = 0);
###&emsp;其它API

	int         getId() const;
    int         getStatus() const;
    const char* getName() const;
	void   writeLogMsg(const char* msg);
    bool   isVerboseMsgEnabled() const;
    void   writeVerboseMsg(const char* msg);
    void   writeErrorMsg(const char* msg);
###&emsp;回调接口

	virtual void onCreate() {}
    virtual void onSetParameter(const char* name, int type, const char* value, bool isLast) {}
    virtual int  onBarSeriesFeed(const char* instrument, int resolution, int interval, int num, MarketData* buffer) { return 0; }
    virtual void onStart() {}
    virtual void onTick(const MarketData& data) {}
    virtual void onBar(const Bar& bar) {}
    virtual void onOrderSubmitted(const Order& order) {}
    virtual void onOrderUpdated(const Order& order) {}
    virtual void onExecutionReport(const Execution& exec) {}
    virtual void onOrderPartiallyFilled(const Order& order) {}
    virtual void onOrderFilled(const Order& order) {}
    virtual void onOrderRejected(const Order& order) {}
    virtual void onOrderCancelled(const Order& order) {}
    virtual void onOrderCancelRejected(const Order& order) {}
    virtual void onCommand(const char* command) {}
    virtual void onTimer(int timerId) {}
    virtual void onHistoricalDataRequestAck(const HistoricalDataRequest& request) {}
    virtual void onEnvVariable(const char* name, const char* value) {}
    virtual void onPause() {}
    virtual void onResume() {}
    virtual void onStop() {}
    virtual void onDestory() {}
###&emsp;运行接口
	
	#define DEFAULT_SRV_ADDR        ("127.0.0.1")
	#define DEFAULT_SRV_PORT        (5501)

	bool run(const StrategyConfig& config, const char* srvAddr = DEFAULT_SRV_ADDR, int srvPort = DEFAULT_SRV_PORT);
    void stop();

## StrategyConfig
###&emsp;设置接口
	
	void             setName(const char* name);
    const char*      getName() const;
    void             setDescription(const char* desc);
    const char*      getDescription() const;
    void             setAuthor(const char* author);
    const char*      getAuthor() const;
	void enableAlgoTrader();
    void disableAlgoTrader();
###&emsp;行情订阅

	void subscribe(const char* instrument, int resolution = Resolution::TICK, int interval = 0);
###&emsp;参数设置
    StrategyConfig& setUserParameter(const char* name, int value);
    StrategyConfig& setUserParameter(const char* name, double value);
    StrategyConfig& setUserParameter(const char* name, bool value);
    StrategyConfig& setUserParameter(const char* name, const char* value);