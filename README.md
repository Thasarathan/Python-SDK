# Python SDK for Stocknote API
Official Python SDK for accessing Stocknote API

The official Python library for communicating with the Stocknote APIs.

Stocknote API Python library provides a wrapper over the HTTPs APIs.

The HTTP calls have been converted to methods and JSON responses are wrapped into Python-compatible objects.

Websocket connections are handled automatically with the library

## Installation

This module is installed via pip:

```
pip install StocknotePythonSDK
```


### Prerequisites

Python 2.x or 3.x

Also, you need the following modules:

* `future`
* `requests`
* `websocket`
* `websocket_client`

The modules can also be installed using `pip`

## Getting started with API

### Overview
SDK stands for software development kit.A set of tools that can be used to create and develop applications.” In general, an SDK refers to a full-suite software module that includes everything you need for a specific module within an application.
There is a StocknoteAPIPythonBridge class in the library: create a object for StocknoteAPIPythonBridge with an instance and from this class you can create a Session token using Login function.The StockNote APIs allow the user authentication using the session token from Login API. A valid StockNote Trading Account and subscription to StockNote API Services is a pre-requisite for successful authentication.
 

### REST Documentation
The original REST API that this SDK is based on is available online.
   [Stocknote API REST documentation](https://developers.stocknote.com/api/?python#stocknote-api-documentation)

## Using the API

### Get an session token
1. Import StocknoteAPIPythonBridge
```
from snapi_py_client.snapi_bridge import StocknoteAPIPythonBridge
```

2. Create a StocknoteAPIPythonBridge object
```python
samco=StocknoteAPIPythonBridge()
```
3. Get the login function so you can login with your Stocknote APi by providing below parameters.

## Parameters:
```
userId*,password*,yob*
```
## Login Sample Request:
  ```python
  login=samco.login(body={"userId":'*****','password':'*****','yob':'****'})
  print("Login details",login)
  ##this will return a user details and generated session token
  ```
 ## Login Response:
 ```python
 {
  "serverTime": "16/06/20 12:36:52",
  "msgId": "580d405d-663e-49e4-9a5d-26d439bc8390",
  "status": "Success",
  "statusMessage": "Login session token generated successfully ",
  "sessionToken": "cbcc85c02d057187a4c6512ae0978946",
  "accountID": "client_id",
  "accountName": "client_name",
  "exchangeList": [
    "BSE",
    "NSE"
  ],
  "orderTypeList": [
    "L",
    "MKT",
    "SL"
  ],
  "productList": [
    "CNC",
    "CO",
    "MIS"
  ]
}
```
4. Get the session token form login response and set it to `set_session_token()` function.
```python
samco.set_session_token(sessionToken="cbcc85c02d057187a4c6512ae0978946")
## this function will help to reduce to pass session token for other apis. This will automate the session token for other apis
```
### Search Equity & Derivative:
To search equity, derivatives and commodity scrips based on user provided search symbol and exchange name. 
The search function name in python is `search_equity_derivative()`

#### Parameters:
```python
search_symbol_name*,exchange
```
#### Sample Search Request:
```python
samco.search_equity_derivative(search_symbol_name="BANKNIFTY20JUN",exchange=samco.EXCHANGE_NFO)
```
#### Sample Search Response:
```python
{
 "msgId": "a9080992-71f3-47a9-9b53-b6103f4eb6ba",
  "status": "Success",
  "statusMessage": "Equity Search details retrieved successfully",
  "equityDertivativeValues": [
       {
            "tradingSymbol": "BANKNIFTY20JUN21000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN22000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20500CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20000CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN19000PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN20000PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN21500CE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        },
        {
            "tradingSymbol": "BANKNIFTY20JUN19500PE",
            "instrument": "OPTIDX",
            "exchange": "NFO"
        }
    ]
}
```
### Quote:
Get market depth details for a specific equity scrip including but not limited to values like last trade price, previous close price, change value, change percentage, bids/asks, upper and lower circuit limits etc. This helps user with market picture of an equity scrip using which he will be able to place an order.
The Quote function name in python is `get_quote()`

#### Parameters:
```python
`symbol_name`,exchange
```
#### Sample Quote request:
```python
samco.get_quote(symbol_name='BANKNIFTY18JUN2017900PE',exchange=samco.EXCHANGE_NFO)
```
#### Sample Quote Response:
```python
{
    "serverTime": "16/06/20 14:06:12",
    "msgId": "b6322a42-1e3f-4706-af6d-6e88c32a5ee5",
    "status": "Success",
    "statusMessage": "Quote details retrieved successfully",
    "tradingSymbol": "BANKNIFTY18JUN2017900PE",
    "exchange": "NFO",
    "lastTradedTime": "16/06/2020 14:08:05",
    "lastTradedPrice": "54.25",
    "changeValue": "19.45",
    "changePercentage": "55.89",
    "lastTradedQuantity": "40",
    "lowerCircuitLimit": "0.05",
    "upperCircuitLimit": "138.95",
    "averagePrice": "37.63",
    "totalBuyQuantity": "85520",
    "totalSellQuantity": "17100",
    "totalTradedValue": "1.57858 (Crs)",
    "totalTradedVolume": "419500",
    "yearlyHighPrice": "0.00",
    "yearlyLowPrice": "0.00",
    "tickSize": "0.05",
    "openInterest": "16880",
    "bestBids": [
        {
            "number": "1",
            "quantity": "20",
            "price": "54.00"
        },
        {
            "number": "2",
            "quantity": "40",
            "price": "53.95"
        },
        {
            "number": "3",
            "quantity": "40",
            "price": "53.85"
        },
        {
            "number": "4",
            "quantity": "40",
            "price": "53.75"
        },
        {
            "number": "5",
            "quantity": "120",
            "price": "53.70"
        }
    ],
    "bestAsks": [
        {
            "number": "1",
            "quantity": "20",
            "price": "54.55"
        },
        {
            "number": "2",
            "quantity": "80",
            "price": "54.60"
        },
        {
            "number": "3",
            "quantity": "40",
            "price": "54.65"
        },
        {
            "number": "4",
            "quantity": "40",
            "price": "54.70"
        },
        {
            "number": "5",
            "quantity": "480",
            "price": "54.75"
        }
    ],
    "expiryDate": "18 Jun 20",
    "spotPrice": "19959.35",
    "instrument": "OPTIDX",
    "lotQuantity": "20",
    "listingId": "41870_NFO",
    "openInterestChange": "8800",
    "oIChangePer": "58.05"
}
```
### OptionChain:
To search OptionChain for equity, derivatives and commodity scrips based on user provided search symbol and exchange name.
The OptionChain function name in python is `get_option_chain()`

#### Parameters:
```python
search_symbol_name,exchange,expiry_date,strike_price,option_type
```
#### Sample OptionChain Request:
```python
samco.get_option_chain(search_symbol_name='Reliance',exchange=samco.EXCHANGE_NFO,expiry_date='2020-07-30',strike_price='1961.40',option_type='PE')
```
#### Sample OptionChain Response:
```python
{
  "serverTime": "16/06/20 14:48:53",
  "msgId": "9922deb8-dcdb-402f-a282-9f8df0b2fdee",
  "status": "Success",
  "statusMessage": "OptionChain details retrived successfully. ",
  "optionChainDetails": [
    {
      "tradingSymbol": "RELIANCE20JUL1961.4PE",
      "exchange": "NFO",
      "symbol": "38914_NFO",
      "strikePrice": "1961.40",
      "expiryDate": "2020-07-30",
      "instrument": "OPTSTK",
      "optionType": "PE",
      "underLyingSymbol": "RELIANCE",
      "spotPrice": "1613.45",
      "lastTradedPrice": "0.00",
      "openInterest": "0",
      "openInterestChange": "0",
      "oichangePer": "0",
      "volume": "0"
    }
  ]
}
```
### UserLimits:
Gets the user cash balances, available margin for trading in equity and commodity segments.
The UserLimits function name in python is `get_limits()`
#### Sample UserLimit Request:
```python
samco.get_limits()
```
#### Sample UserLimit Response:
```python
{
  "serverTime": "18/06/20 12:27:44",
  "msgId": "095bd777-34f3-40b8-81fd-6bf25d3f3c3c",
  "status": "Success",
  "statusMessage": "User Limit details retrieved successfully",
  "equityLimit": {
    "grossAvailableMargin": "50000000000",
    "payInToday": "0",
    "notionalCash": "0",
    "marginUsed": "0",
    "netAvailableMargin": "50000000000"
  },
  "commodityLimit": {
    "grossAvailableMargin": "0",
    "payInToday": "0",
    "notionalCash": "0",
    "marginUsed": "0",
    "netAvailableMargin": "0"
  }
}
```
### PlaceOrder:
To place an equity/derivative order to the exchange i.e the place order request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. To be precise, under normal scenarios, the whole flow of order execution starting with order placement, routing to OMS and transfer to the exchange, order execution, and confirmation from exchange happen real time. But due to various reasons like market hours, exchange related checks etc. This may not happen instantly. So when an order is successfully placed the PlaceOrder API returns an OrderNumber in response, and in scenarios as above the actual order status can be checked separately using the OrderStatus API call .This is for Placing CNC, MIS and NRML Orders.
The PlaceOrder function name in python is `place_order()`

#### Sample PlaceOrder Request:
```python
samco.place_order(body={
"symbolName":"RELIANCE",
"exchange":samco.EXCHANGE_NSE,
"transactionType":samco.TRANSACTION_TYPE_BUY,
"orderType":samco.ORDER_TYPE_LIMIT,
"price":"1282",
"quantity": "15",
"disclosedQuantity":"",
"orderValidity":samco.VALIDITY_DAY,
"productType":samco.PRODUCT_MIS,
"afterMarketOrderFlag":"NO"
})
```
#### sample PlaceOrder Response:
```python
{
  "serverTime": "16/06/20 18:03:48",
  "msgId": "0b9e75c7-c624-4c77-bfbf-6d4e53536948",
  "orderNumber": "200616000000350",
  "status": "Success",
  "statusMessage": "MIS Order request placed successfully",
  "exchangeOrderStatus": "PENDING",
  "orderDetails": {
    "pendingQuantity": "15",
    "avgExecutionPrice": "0.00",
    "orderPlacedBy": "--",
    "tradingSymbol": "RELIANCE-EQ",
    "triggerPrice": "0.00",
    "exchange": "NSE",
    "totalQuantity": "15",
    "transactionType": "BUY",
    "productType": "MIS",
    "orderType": "L",
    "quantity": "15",
    "filledQuantity": "0",
    "orderPrice": "1282.0",
    "filledPrice": "0.00",
    "exchangeOrderNo": "1100000000015551",
    "orderValidity": "DAY",
    "orderTime": "16/06/2020 18:03:47"
  }
}
```
### PlaceOrderBO:
To place an equity/derivative order to the exchange i.e the place order BO request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. To be precise, under normal scenarios, the whole flow of order execution starting with order placement, routing to OMS and transfer to the exchange, order execution, and confirmation from exchange happen real time. But due to various reasons like market hours, exchange related checks etc. This may not happen instantly. So when an order is successfully placed the placeOrderBO returns an orderNumber in response, and in scenarios as above the actual order status can be checked separately using the orderStatus API call. This is for Placing BO Orders.
The PlaceOrderBO function name in python is `place_order_bo()`
#### Sample PlaceOrderBO Request:
```python
samco.place_order_bo(body={
"symbolName":"TCS",
"exchange":"BSE",
"transactionType":samco.TRANSACTION_TYPE_BUY,
"orderType":samco.ORDER_TYPE_LIMIT,
"quantity": "10",
"disclosedQuantity":"1",
"price":"2021",
"priceType":"LTP",
"valueType":"Absolute",
"orderValidity":samco.VALIDITY_DAY,
"productType":samco.PRODUCT_BO,
"squareOffValue":"15.00",
"stopLossValue":"5.00",
"trailingStopLoss":"5"
})
```
#### Sample PlaceOrderBO Response:
```python
{
  "serverTime": "17/06/20 18:29:39",
  "msgId": "3dde806a-17b3-43ae-b1c1-58691f640a10",
  "orderNumber": "200617000000375",
  "status": "Success",
  "statusMessage": "Bracket Order request placed successfully",
  "exchangeOrderStatus": "EXECUTED",
  "orderDetails": {
    "pendingQuantity": "0",
    "avgExecutionPrice": "2014.95",
    "orderPlacedBy": "--",
    "tradingSymbol": "TCS",
    "triggerPrice": "0.00",
    "exchange": "BSE",
    "totalQuantity": "10",
    "transactionType": "BUY",
    "productType": "BO",
    "orderType": "L",
    "quantity": "10",
    "filledQuantity": "10",
    "orderPrice": "2021.0",
    "filledPrice": "2014.95",
    "exchangeOrderNo": "1592387449638000140",
    "orderValidity": "DAY",
    "orderTime": "17/06/2020 18:29:38"
  }
}
```
### PlaceOrderCO:
To place an equity/derivative order to the exchange i.e the place order CO request typically registers the order with OMS and when it happens successfully, a success response is returned. Successful placement of an order via the API does not imply its successful execution. To be precise, under normal scenarios, the whole flow of order execution starting with order placement, routing to OMS and transfer to the exchange, order execution, and confirmation from exchange happen real time. But due to various reasons like market hours, exchange related checks etc. This may not happen instantly. So when an order is successfully placed the placeOrderCO returns an orderNumber in response, and in scenarios as above the actual order status can be checked separately using the orderStatus API call. This is for Placing CO Orders.
The PlaceOrderCO function name in python is `place_order_co()`
#### Sample PlaceOrderCO Request:
```Python
samco.place_order_co(body={
"symbolName":"INFY",
"exchange":samco.EXCHANGE_NSE,
"transactionType":samco.TRANSACTION_TYPE_BUY,
"orderType":samco.ORDER_TYPE_LIMIT,
"price":"679",
"quantity": "15",
"disclosedQuantity":"",
"orderValidity":samco.VALIDITY_DAY,
"productType":samco.PRODUCT_CO,
"afterMarketOrderFlag":"NO",
"triggerPrice":"646"})
```
#### Sample PlaceOrderCO Response:
```Python
{
  "serverTime": "17/06/20 16:37:18",
  "msgId": "9bd0ab52-f6a0-4ec6-9813-aa707795aa87",
  "orderNumber": "200617000000181",
  "status": "Success",
  "statusMessage": "CO Order request placed successfully",
  "exchangeOrderStatus": "EXECUTED",
  "orderDetails": {
    "pendingQuantity": "0",
    "avgExecutionPrice": "679.00",
    "orderPlacedBy": "--",
    "tradingSymbol": "INFY-EQ",
    "triggerPrice": "646.00",
    "exchange": "NSE",
    "totalQuantity": "15",
    "transactionType": "BUY",
    "productType": "CO",
    "orderType": "L",
    "quantity": "15",
    "filledQuantity": "15",
    "orderPrice": "679.0",
    "filledPrice": "679.00",
    "exchangeOrderNo": "1100000000026975",
    "orderValidity": "DAY",
    "orderTime": "17/06/2020 16:37:17"
  }
}
```
### ModifyOrder:
User would be able to modify some attributes of an order as long as it is with open/pending status in system. For modification order identifier is mandatory. With order identifier you need to send the optional parameter(s) which needs to be modified. In case the optional parameters aren't sent, the default will be considered from the original order. Modifiable attributes include quantity, Order Type (L,MKT, SL,SL-M). This API cannot be used for modifying attributes of an executed/rejected/cancelled order. Only the attribute that needs to be modified should be sent in the request alongwith the Order Identifier.
The ModifyOrder function name in python is `modify_order()`

#### Sample ModifyOrder Request:
```python
samco.modify_order(order_number='200616000000350',body={"quantity": "50"})
```
#### Sample ModifyOrder Response:
```python
{
  "serverTime": "16/06/20 18:12:42",
  "msgId": "c681bb4b-37c1-4e50-b3f6-60f3c43b9bef",
  "orderNumber": "200616000000350",
  "status": "Success",
  "statusMessage": "Order 200616000000350 modified successfully",
  "exchangeOrderStatus": "PENDING",
  "orderDetails": {
    "pendingQuantity": "50",
    "avgExecutionPrice": "0.00",
    "orderPlacedBy": "Dv999",
    "tradingSymbol": "RELIANCE-EQ",
    "triggerPrice": "0.00",
    "exchange": "NSE",
    "totalQuantity": "50",
    "transactionType": "BUY",
    "productType": "MIS",
    "orderType": "L",
    "quantity": "50",
    "filledQuantity": "0",
    "orderPrice": "1282.0",
    "filledPrice": "0.00",
    "exchangeOrderNo": "1100000000015551",
    "orderValidity": "DAY",
    "orderTime": "16/06/2020 18:12:41"
  }
}
```
### OrderBook:
Orderbook retrieves and displays details of all orders placed by the user on a specific day. This API returns all states of the orders, namely, open, pending, rejected and executed ones.
The OrderBook function name in python is `get_order_book()`

#### Sample OrderBook Request:
```python
samco.get_order_book()
```
#### Sample OrderBook Response:
```Python
{
  "serverTime": "16/06/20 18:25:18",
  "msgId": "2e2d2926-1a15-4510-b98e-c86d1f87cb7e",
  "status": "Success",
  "statusMessage": "Order Book details retrieved successfully",
  "orderBookDetails": [
    {
      "orderNumber": "200616000000350",
      "exchange": "NSE",
      "tradingSymbol": "RELIANCE",
      "transactionType": "BUY",
      "productCode": "MIS",
      "orderType": "L",
      "orderPrice": "1282.00",
      "triggerPrice": "0.00",
      "orderValidity": "DAY",
      "orderStatus": "Open",
      "orderValue": "0.0",
      "orderTime": "16-Jun-2020 18:03:47",
      "userId": "DS37591",
      "filledQuantity": "0",
      "fillPrice": "0.00",
      "averagePrice": "0.00",
      "rejectionReason": "--",
      "exchangeConfirmationTime": "16-Jun-2020 18:12:41",
      "coverOrderPercentage": "0.0",
      "orderRemarks": "--",
      "exchangeOrderNumber": "1100000000015551",
      "symbol": "2885_NSE",
      "displayStrikePrice": "00.00",
      "displayNetQuantity": "50",
      "status": "Open",
      "exchangeStatus": "open",
      "expiry": "NA",
      "pendingQuantity": "50",
      "totalQuanity": "50",
      "optionType": "XX",
      "orderPlaceBy": "Dv999"
    }
  ]
}
```
### TriggerOrders:
To get the trigger order numbers in case of BO and CO orders so that their attribute values can be modified for BO orders, it will give the order identifiers. For Stop loss leg and target leg. Similarly for CO orders, it will return order identifier of stop loss leg only. Using the order identifier, the user would be able to modify the order attributes using the modifyOrder API. Refer modifyOrder API documentation for the parameters details.
The TriggerOrders function name in python is `get_trigger_order_numbers()`

#### Sample TriggerOrders Request:
```python
samco.get_trigger_order_numbers(order_number="200617000000378")
```
#### Sample TriggerOrders Response:
```python
{
    "serverTime": "17/06/20 18:40:00",
    "msgId": "ccff75e1-9d79-4b54-b4cb-bc48e080758f",
    "status": "Success",
    "statusMessage": "SubOrder details retrieved successfully.",
    "triggerOrders": [
        {
            "targetOrderNo": "200617000000380",
            "orderStatus": "Complete",
            "orderPrice": "2010.00",
            "triggerPrice": "0.00"         
        },
        {
            "targetOrderNo": "200617000000379",
            "orderStatus": "Cancelled",
            "orderPrice": "2029.95",
            "triggerPrice": "0.00"
        }
    ]
}
```
### OrderStatus:
Get status of an order placed previously. This API returns all states of the orders,but not limited to open, pending, and partially filled ones.
The OrderStatus function name in python is `get_order_status`
#### Sample OrderStatus Request:
```python
samco.get_order_status(order_number="200617000000378")
```
#### Sample OrderStatus Response:
```python
{
    "serverTime": "17/06/20 20:54:53",
    "msgId": "d45688d9-31c0-4195-90ba-5474e7f50873",
    "orderNumber": "200617000000378",
    "orderStatus": "EXECUTED",
    "orderDetails": {
        "pendingQuantity": "0",
        "avgExecutionPrice": "2014.95",
        "orderPlacedBy": "--",
        "tradingSymbol": "TCS",
        "triggerPrice": "0.00",
        "exchange": "BSE",
        "totalQuantity": "10",
        "transactionType": "BUY",
        "productType": "BO",
        "orderType": "L",
        "quantity": "10",
        "filledQuantity": "10",
        "orderPrice": "2021.0",
        "filledPrice": "2014.95",
        "exchangeOrderNo": "1592387449638000143",
        "orderValidity": "DAY",
        "orderTime": "17/06/2020 18:38:37"
    }
}
```
### CancelOrder:
An order which is open or pending in system can be cancelled. In other words, cancellation cannot be initiated for already Executed, Rejected orders.This is for CNC, MIS and NRML Orders.
The CancleOrder function name in python is `cancel_order()`
#### Sample CancelOrder Request:
```python
samco.cancel_order(order_number='200616000000350')
```
#### sample CancelOrder Response:
```python
{
  "serverTime" : "16/06/20 14:50:36",
  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
  "status" : "Success",
  "orderNumber" : "200616000000350",
  "statusMessage" : "Order cancelled successfully"
}
```
### CancelOrderCO:
For Cancellation/exit of CO orders pass main leg Order number. If main leg is in Open/Pending state that order will be cancelled.
If the main leg is executed and the sublegs are created and in open/Trigger pending state, the order will be exited.
If the main leg is executed and if Stop loss is hit, API will return error message "SubOrder is in Executed status. Cannot exit/cancel such orders.
The CancleOrder function name in python is `cancel_order_co()`
#### Sample CancelOrderCO Request:
```python
samco.cancel_order_co(order_number='200617000000181')
```
#### sample CancelOrderCO Response:
```python
{
  "serverTime" : "16/06/20 14:50:36",
  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
  "status" : "Success",
  "orderNumber" : "200617000000181",
  "statusMessage" : "Cover Order 200617000000181 exited successfully"
}
```
### CancelOrderBO:
For Cancellation/exit of BO orders pass main leg Order number. If main leg is in Open/Pending state that order will be cancelled.
If the main leg is executed and the sublegs are created and in open/Trigger pending state, the order will be exited.
If the main leg is executed and if either of Stop loss or target is hit, API will return error message "SubOrder is in Executed status. Cannot exit/cancel such orders."
The CancleOrder function name in python is `cancel_order_bo()`
#### Sample CancelOrderBO Request:
```python
samco.cancel_order_bo(order_number='200617000000375')
```
#### sample CancelOrderBO Response:
```python
{
  "serverTime" : "16/06/20 14:50:36",
  "msgId" : "25d6d99b-3224-4a77-b129-a5d0bd38349b",
  "status" : "Success",
  "orderNumber" : "200617000000375",
  "statusMessage" : "Bracket Order exited successfully"
}
```
### TradeBook:
Details of all successfully executed orders placed by the user.
The TradeBook function name in python is `get_trade_book()`
#### Sample TradeBook Request:
```python
samco.get_trade_book()
```
#### Sample TradeBook Response:
```python
{
    "serverTime": "17/06/20 21:01:25",
    "msgId": "c4b7ec88-32e5-4e1f-a56b-7186f6933d79",
    "status": "Success",
    "statusMessage": "Request Successfull",
    "tradeBookDetails": [
        {
            "orderNumber": "200617000000380",
            "exchange": "BSE",
            "tradingSymbol": "TCS",
            "transactionType": "SELL",
            "productCode": "BO",
            "orderType": "L",
            "orderPrice": "2010.00",
            "quantity": "10",
            "orderValidity": "DAY",
            "orderTime": "06:39:50 PM",
            "filledQuantity": "10",
            "exchangeOrderNumber": "1592387449638000145",
            "tradeNumber": "25400",
            "tradePrice": "2010.00",
            "tradeDate": "17JUN2020",
            "tradeTime": "06:39:49 PM",
            "strikePrice": "0.00",
            "optionType": "XX",
            "expiry": "NA"
        }
    ]
}
```
### Positions:
Get position details of the user (The details of equity, derivative, commodity, currency borrowed or owned by the user).
The Postions function name in python is `get_positions_data()`
#### Sample Positions Request:
```Python
samco.get_positions_data(position_type=samco.POSITION_TYPE_DAY)
```
#### Sample Positions Response:
```python
{
    "serverTime": "17/06/20 21:06:10",
    "msgId": "36a2cb48-2ce8-48e4-ac0a-90e68c6d26f1",
    "status": "Success",
    "statusMessage": "User Positions details retrieved successfully",
    "positionDetails": [
        {
            "averagePrice": "-4.95",
            "exchange": "BSE",
            "markToMarketPrice": "-99.00",
            "lastTradedPrice": "2,010.00",
            "previousClose": "2067.80",
            "productCode": "BO",
            "tradingSymbol": "TCS",
            "calculatedNetQuantity": "0.0",
            "averageBuyPrice": "2014.95",
            "averageSellPrice": "2010.00",
            "boardLotQuantity": "1",
            "boughtPrice": "40299.00",
            "buyQuantity": "20",
            "carryForwardQuantity": "0",
            "carryForwardValue": "0.00",
            "multiplier": "1",
            "netPositionValue": "-99.00",
            "netQuantity": "0",
            "netValue": "-99.00",
            "positionType": "DAY",
            "positionConversions": [
                "CNC",
                "NRML"
            ],
            "soldValue": "40200.00",
            "transactionType": "BUY",
            "realizedGainAndLoss": "-99.00",
            "unrealizedGainAndLoss": "0.00",
            "companyName": "TATA CONSULTANCY SERVICES LTD."
        }
    ]
}
```
### PositionConversion:
Convert an existing position of a margin product to a different margin product type. All or a subset of an existing position quantity can be converted to a different product type.The available margin product types are MARGIN_INTRADAY_SQUAREOFF(MIS), CASHNCARRY(CNC), NORMAL(NRML).
The PostionConversion function name in python is `convert_position()`
##### Sample PositionConverstion Request:
```python
samco.convert_position(body={ 
  "symbolName":"TSC",
  "exchange":"BSE",
  "transactionType":"BUY",
  "positionType":"DAY",
  "quantityToConvert": "2",
   "fromProductType":"MIS",
   "toProductType":"CNC",
   "netQuantity":"2"
})
```
#### Sample PostionConverstion Response:
```python
{
  "serverTime" : "17x/06/20 15:06:42",
  "msgId" : "ba32c75f-ee4b-4af6-a580-f17ad36fefd4",
  "status" : "Success",
  "statusMsg" : "Position Conversion from MIS to CNC successful"
}
```

### Holdings:
Get the details of the Stocks which client is holding. Here, you will be able to get the Client holdings which are bought under ‘CNC’ product type and are not sold yet.
The Holdings function name in python is `get_holding()`
#### Sample Holdings Request:
```python
samco.get_holding()
```
#### Sample Holdings Response:
```python
{
    "serverTime": "16/06/20 18:31:52",
    "msgId": "192d039e-6647-4e2f-8d97-5a91143d47a7",
    "status": "Success",
    "statusMessage": "User Holding details retrieved successfully",
    "holdingSummary": {
        "gainingTodayCount": "2",
        "losingTodayCount": "2",
        "totalGainAndLossAmount": "-242900000.00",
        "portfolioValue": "176205000.00"
    },
    "holdingDetails": [
        {
            "averagePrice": "51.10",
            "exchange": "BSE",
            "lastTradedPrice": "0.00",
            "previousClose": "51.10",
            "productCode": "CNC",
            "symbolDescription": "ASHOK LEYLAND LTD.",
            "tradingSymbol": "ASHOKLEY",
            "totalGainAndLoss": "-51100000.00",
            "holdingsQuantity": "1000000",
            "collateralQuantity": "0",
            "holdingsValue": "0.00",
            "sellableQuantity": "1000000"
        },
        {
            "averagePrice": "1610.60",
            "exchange": "NSE",
            "lastTradedPrice": "1760.30",
            "previousClose": "1610.60",
            "productCode": "CNC",
            "symbolDescription": "ASIAN PAINTS LIMITED",
            "tradingSymbol": "ASIANPAINT-EQ",
            "totalGainAndLoss": "14970000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "176030000.00",
            "sellableQuantity": "100000"
        },
        {
            "averagePrice": "1.65",
            "exchange": "NSE",
            "lastTradedPrice": "1.75",
            "previousClose": "1.65",
            "productCode": "CNC",
            "symbolDescription": "JAIPRAKASH ASSOCIATES LTD",
            "tradingSymbol": "JPASSOCIAT-EQ",
            "totalGainAndLoss": "10000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "175000.00",
            "sellableQuantity": "100000"
        },
        {
            "averagePrice": "2067.80",
            "exchange": "BSE",
            "lastTradedPrice": "0.00",
            "previousClose": "2067.80",
            "productCode": "CNC",
            "symbolDescription": "TATA CONSULTANCY SERVICES LTD.",
            "tradingSymbol": "TCS",
            "totalGainAndLoss": "-206780000.00",
            "holdingsQuantity": "100000",
            "collateralQuantity": "0",
            "holdingsValue": "0.00",
            "sellableQuantity": "100000"
        }
    ]
}
```
### IntraDayCandleData:
Gets the Intraday candle data such as Open, high, low, close and volume within specific time period per min for a specific symbol.
The IndexIntraDayCandleData function name in python is `get_intraday_candle_data()`
#### Sample IntraDayCandleData Request:
```Python
samco.get_intraday_candle_data(symbol_name='INFY',exchange=samco.EXCHANGE_NSE, from_date='2020-06-17 10:22:00',to_date='2020-06-17 10:28:00')
```
#### Sample IntraDayCandleData Response:
```python
{
  "serverTime": "17/06/20 10:50:31",
  "msgId": "c3a1ae34-8078-4f56-8a00-83f92bfa3a4b",
  "status": "Success",
  "statusMessage": "Intraday candle data retrieved successfully",
  "intradayCandleData": [
    {
      "dateTime": "2020-06-17 10:22:00.0",
      "open": "705.25",
      "high": "705.3",
      "low": "704.6",
      "close": "704.65",
      "volume": "7627"
    },
    {
      "dateTime": "2020-06-17 10:23:00.0",
      "open": "704.6",
      "high": "704.7",
      "low": "704.0",
      "close": "704.0",
      "volume": "16154"
    },
    {
      "dateTime": "2020-06-17 10:24:00.0",
      "open": "704.25",
      "high": "704.6",
      "low": "704.05",
      "close": "704.6",
      "volume": "13767"
    },
    {
      "dateTime": "2020-06-17 10:25:00.0",
      "open": "704.75",
      "high": "704.75",
      "low": "703.8",
      "close": "703.95",
      "volume": "13091"
    },
    {
      "dateTime": "2020-06-17 10:26:00.0",
      "open": "703.95",
      "high": "704.3",
      "low": "703.8",
      "close": "704.1",
      "volume": "7039"
    },
    {
      "dateTime": "2020-06-17 10:27:00.0",
      "open": "704.15",
      "high": "704.15",
      "low": "703.55",
      "close": "703.95",
      "volume": "17886"
    },
    {
      "dateTime": "2020-06-17 10:28:00.0",
      "open": "704.0",
      "high": "704.95",
      "low": "703.75",
      "close": "704.85",
      "volume": "17760"
    }
  ]
}
```
### IndexIntraDayCandleData:
Gets the Index intraday candle data such as Open, high, low, close and volume within specific time period per min for a specific index.
The IndexIntraDayCandleData function name in python is `get_index_intraday_candle_data()`
#### Sample IndexIntraDayCandleData Request:
```Python
samco.get_index_intraday_candle_data(index_name='sensex', from_date='2020-06-16 09:23:00',to_date='2020-06-16 9:28:00')
```
#### Sample IndexIntraDayCandleData Response:
```Python
{
  "serverTime": "16/06/20 19:09:13",
  "msgId": "42bc5657-2d2b-49f3-8ead-1bb07a157e2a",
  "status": "Success",
  "statusMessage": "Index IntraDay Candle data retrieved successfully ",
  "indexIntraDayCandleData": [
    {
      "dateTime": "2020-06-16 09:23:00.0",
      "open": "33896.83",
      "high": "33914.65",
      "low": "33874.05",
      "close": "33874.96",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:24:00.0",
      "open": "33878.08",
      "high": "33915.78",
      "low": "33874.27",
      "close": "33909.3",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:25:00.0",
      "open": "33905.3",
      "high": "33911.31",
      "low": "33884.92",
      "close": "33900.15",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:26:00.0",
      "open": "33899.02",
      "high": "33936.46",
      "low": "33899.02",
      "close": "33936.46",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:27:00.0",
      "open": "33936.5",
      "high": "33951.67",
      "low": "33924.21",
      "close": "33925.92",
      "volume": "0"
    },
    {
      "dateTime": "2020-06-16 09:28:00.0",
      "open": "33925.2",
      "high": "33928.91",
      "low": "33886.56",
      "close": "33890.5",
      "volume": "0"
    }
  ]
}
```
### HistoricalCandleData:
Gets the historical candle data such as Open, high, low, close, last traded price and volume within specific dates for a specific symbol. From date is mandatory. End date is optional and defaults to Today.
The HistoricalCandleData function name in python is `get_index_intraday_candle_data()`

#### Sample HistoricalCandleData Request:
```python
samco.get_historical_candle_data(symbol_name='BANKNIFTY18JUN2018500PE',exchange=samco.EXCHANGE_NFO, from_date='2020-06-14',to_date='2020-06-17')
```
#### Sample HistoricalCandleData respone:
```python
{
  "serverTime": "17/06/20 11:14:06",
  "msgId": "97cdca8f-81f9-4a88-8da6-99b471e82803",
  "status": "Success",
  "statusMessage": "Historical candle data retrieved successfully",
  "historicalCandleData": [
    {
      "date": "2020-06-15",
      "open": "60.0",
      "high": "136.45",
      "low": "56.2",
      "close": "78.5",
      "ltp": "78.5",
      "volume": "9302660"
    },
    {
      "date": "2020-06-16",
      "open": "38.75",
      "high": "206.85",
      "low": "13.0",
      "close": "38.5",
      "ltp": "38.5",
      "volume": "7792900"
    }
  ]
}
```
### IndexHistoricalCandleData:
Gets the Index historical candle data such as Open, high, low, close, last traded price and volume within specific dates for a specific index. From date is mandatory. End date is optional and defaults to Today.
The IndexHistoricalCandleData function name in python is `get_index_candle_data()`
#### Sample IndexHistoricalCandleData Request;
```python
samco.get_index_candle_data(index_name='NIFTY 200', from_date='2019-05-24',to_date='2019-05-29')
```
#### Sample IndexHistoricalCandleData Response:
```python
{
  "serverTime": "17/06/20 11:39:11",
  "msgId": "bb015c56-74e5-401b-bfe0-e2c9c415d088",
  "status": "Success",
  "statusMessage": "Index HistoricalCandle data retrieved successfully ",
  "indexCandleData": [
    {
      "date": "2019-05-24",
      "open": "6067.65",
      "high": "6134.4",
      "low": "6029.9",
      "close": "6129.8",
      "ltp": "6129.8",
      "volume": "0"
    },
    {
      "date": "2019-05-27",
      "open": "6134.35",
      "high": "6189.0",
      "low": "6114.5",
      "close": "6177.15",
      "ltp": "6177.15",
      "volume": "0"
    },
    {
      "date": "2019-05-28",
      "open": "6195.7",
      "high": "6195.7",
      "low": "6151.25",
      "close": "6181.35",
      "ltp": "6181.35",
      "volume": "0"
    },
    {
      "date": "2019-05-29",
      "open": "6172.55",
      "high": "6178.85",
      "low": "6132.0",
      "close": "6143.8",
      "ltp": "6143.8",
      "volume": "0"
    }
  ]
}
```
### StreamingData:
StockNote API platform provides the Broadcast API, as the most effective way to receive quote data for instruments across all exchanges during live market hours. The API provides continuous streaming data of quote based on user request, and primarily consists of fields such as last traded price, open, high, low, close, last traded quantity, last traded volume, last traded time etc.

The API uses WebSocket protocol to establish a dedicated TCP connection after an HTTP handshake to receive streaming quotes and thereby provides seamless streaming of quote data. You need to use a WebSocket client to connect to our broadcast API. If you have already subscribed to our StockNote API services, you will be able to access broadcast API too.

#### Sample Streaming Request:
```python
value=[{"symbol":"-53"},{"symbol":"1143_CDS"},{"symbol":"1270_NSE"},{"symbol":"10604_NSE"},{"symbol":"11195_NSE"}]
samco.set_streaming_data(value)
samco.start_streaming()
```
#### Sample Streaming Response:
```python
Message Arrived:{"response":{"data":{"aPr":"0.00","aSz":"0","avgPr":"0.00","bPr":"0.00","bSz":"0","c":"29.65","ch":"0.38","chPer":"1.28","h":"30.28","l":"27.24","lTrdT":"09 Jun 2020, 02:11:58 PM","ltp":"30.03","ltq":"0","ltt":"09 Jun 2020, 02:11:58 PM","lttUTC":"09 Jun 2020, 08:41:58 AM","o":"29.65",
"oI":"","oIChg":"","sym":"-53","tBQ":"0","tSQ":"0","ttv":"0.00","vol":"0","yH":"0.00","yL":"0.00"},"streaming_type":"quote"}}

Message Arrived:{"response":{"data":{"aPr":"0.00","aSz":"0","avgPr":"0.00","bPr":"0.00","bSz":"0","c":"29.65","ch":"0.37","chPer":"1.25","h":"30.28","l":"27.24","lTrdT":"09 Jun 2020, 02:11:59 PM","ltp":"30.02","ltq":"0","ltt":"09 Jun 2020, 02:11:59 PM","lttUTC":"09 Jun 2020, 08:41:59 AM","o":"29.65",
"oI":"","oIChg":"","sym":"-53","tBQ":"0","tSQ":"0","ttv":"0.00","vol":"0","yH":"0.00","yL":"0.00"},"streaming_type":"quote"}}
```

### Logout:
Logging out user from the application.
The Logout function name in python is `logout()`

#### Sample Logout Request:
```python
samco.logout()
```
#### Sample Logout Response:
```python
{
  "serverTime" : "17/06/20 12:27:52",
  "msgId" : "41627994-5c96-411c-b15c-dbda00029269",
  "status" : "Success",
  "statusMessage" : "User has successfully logged out"
}
```
