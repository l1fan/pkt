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
项目相当于websocket的桥接，不做过多的数据处理，发送的订阅请求和返回数据也基本按照官网格式(有区别的会在下方具体标明)

### OKEx
官方文档接口 https://www.okex.me/docs/zh/#futures_ws-all

使用时调用 `ws://ws.bicoin.com.cn/okex`  
订阅格式与官方一致 eg:`{"op":"subscribe","args":["futures/ticker:BTC-USD-190927","swap/trade:BTC-USD-SWAP"]}`,取消订阅`op`为`unsubscribe`     
支持订阅的频道 
- 指数价格 `index/ticker`
- 标记价格 `futures/mark_price`
- 交割/永续价格 `futures/ticker` , `swap/ticker`
- 交割/永续深度 `futures/depth5` , `swap/depth5`
- 交割/永续K线 `futures/candle60s` ... `futures/candle604800s` , `swap/candle60s` ... `swap/candle604800s`
- 交割/永续交易 `futures/trade` , `swap/trade`

> 可以通过http调用 `http://ws.bicoin.com.cn/api/okex?table=futures/ticker:BTC-USD-190927` 获取最新一次数据


### Bitmex
官方文档 https://www.bitmex.com/app/apiOverview

使用时调用 `ws://ws.bicoin.com.cn/bitmex`  
订阅格式 eg: `{"op":"subscribe","args":["instrument:XBTUSD"]}`, 取消订阅`op`为`unsubscribe`    
支持订阅
- `instrument`
- 深度 `orderBook10`
- 交易 `trade`

> 可以通过http调用 `http://ws.bicoin.com.cn/api/bitmex?table=<订阅>` 获取最新一次数据  

### Huobi
官方文档 https://huobiapi.github.io/docs/spot/v1/cn/#websocket

使用时调用 `ws://ws.bicoin.com.cn/huobi`  
订阅格式 eg: `{"sub": "market.btccny.kline.1min","id": "id1"}` 取消订阅时key为`unsub`  
支持订阅
- `market.$symbol.detail`
- 深度 `market.$symbol.depth.step1`
- K线 `market.$symbol$.kline.$period$`
- 交易 `market.$symbol.trade.detail`

> 可以通过http调用 `http://ws.bicoin.com.cn/api/huobi?table=<订阅>` 获取最新一次数据

### Binance
官方文档 https://github.com/binance-exchange/binance-official-api-docs/blob/master/web-socket-streams_CN.md

使用时调用 `ws://ws.bicoin.com.cn/binance?streams=`  
支持订阅
- `<symbol>@miniTicker`
- `<symbol>@depth5`

### Bibox
官方文档 https://github.com/Biboxcom/API_Docs/wiki/WS_API_Reference

使用时调用 `ws://ws.bicoin.com.cn/bibox`  
支持订阅
- 价格 `bibox_sub_spot_$pair_ticker`
- 深度 `bibox_sub_spot_$pair_depth`
- 交易 `bibox_sub_spot_$pair_deals`

### MXC



### IX
官方文档 https://github.com/sonsea/ix-API-Docs/blob/master/quotes_websocket_api.md

使用时调用 `ws://ws.bicoin.com.cn/ix`  
目前仅支持订阅永续合约 `FUTURE_BTCUSD` ,`FUTURE_ETHUSD`, `FUTURE_EOSUSD`      
订阅方式与官网不同, 建立连接后发送订阅信息`{"op":"subscribe","args":["ticker:FUTURE_BTCUSD", ...]}` , 取消订阅时`op`为`unsubscribe`
- 价格 `ticker:FUTURE_BTCUSD`    
- K线 `history/{period}:FUTURE_BTCUSD`  period参照官网
- 深度 `orderbook:FUTURE_BTCUSD`
- 交易 `deal:FUTURE_BTCUSD`

> 可以通过http调用 `http://ws.bicoin.com.cn/api/ix?table=<订阅>` 获取最新一次数据

### BFX
官网 https://www.bfx.nu/h5/index.html#/   > 没有文档,可以用开发者工具查看接口  
合约交易symbol接口 `https://www.bfx.nu/commonApi/partitions.do`

使用时调用 `ws://ws.bicoin.com.cn/bfx`    
订阅，只支持合约
- 价格，深度，交易 `{"sub":"trade.contract.{symbol}"}`  eg: `{"sub":"trade.contract.btc"}`
  返回的数据里有价格，深度，交易数据。 取消订阅时将 `sub` 改为 `unsub`
- K线 `{"sub":"kline.contract.{symbol}.{period}"}`  K线有四个`period`可选 `5min`,`15min`,`1hour`,`4hour`,`1day`
