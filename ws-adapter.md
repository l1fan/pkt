# Websocket Server
启动后，后端会有一个websocket连接到交易所，并保持一直连接，订阅okex,huobi,bitmex....所有数据。

## 流程

```
前端1   前端2   前端3  ...
 |       |      |     |
    Websocker Server 
        wsclient
          |
     OKEx, Bitmex
```

## API接口

### OKEx
文档接口 https://www.okex.me/docs/zh/#futures_ws-all

使用时调用 ws://ws.bicoin.com.cn/okex
支持订阅的频道 
- 交割/永续价格 `futures/ticker` , `swap/ticker`
- 交割/永续深度 `futures/depth5` , `swap/depth5`
- 交割/永续K线 `futures/candle60s` ... `futures/candle604800s` , `swap/candle60s` ... `swap/candle604800s`
- 交割/永续交易 `futures/trade` , `swap/trade`

### Bitmex
文档 https://www.bitmex.com/app/apiOverview

使用时调用 ws://ws.bicoin.com.cn/bitmex
支持订阅
- `instrument`
- 深度 `orderBook10`
- 交易 `trade`

### Huobi
文档 https://huobiapi.github.io/docs/spot/v1/cn/#websocket

使用时调用 ws://ws.bicoin.com.cn/huobi
支持订阅
- `market.$symbol.detail`
- 深度 `market.$symbol.depth.step1`
- K线 `market.$symbol$.kline.$period$`
- 交易 `market.$symbol.trade.detail`

### Binance
文档 https://github.com/binance-exchange/binance-official-api-docs/blob/master/web-socket-streams_CN.md

使用时调用 ws://ws.bicoin.com.cn/binance?streams=
支持订阅
- `<symbol>@miniTicker`
- `<symbol>@depth5`

### Bibox
文档 https://github.com/Biboxcom/API_Docs/wiki/WS_API_Reference

使用时调用 ws://ws.bicoin.com.cn/bibox
支持订阅
- 价格 `bibox_sub_spot_$pair_ticker`
- 深度 `bibox_sub_spot_$pair_depth`
- 交易 `bibox_sub_spot_$pair_deals`

### MXC



### IX
文档 https://github.com/sonsea/ix-API-Docs/blob/master/quotes_websocket_api.md

使用时调用 ws://ws.bicoin.com.cn/ix
订阅， 目前仅支持订阅永续合约 `FUTURE_BTCUSD`
- 价格 `/ticker/FUTURE_BTCUSD`    eg: `ws://ws.bicoin.com.cn/ix/ticker/FUTURE_BTCUSD`
- 深度 `/orderbook/FUTURE_BTCUSD`
- 交易 `/deal/FUTURE_BTCUSD`