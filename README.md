# This is a lightweight library that works as a connector to the Binance Futures API

• Supported APIs:
• /fapi/*
• /dapi/*
• /futures/*
• USD-M Futures Websocket Market Stream
• COIN-M Futures Websocket Market Stream
• USD-M Futures User Data Stream
• COIN-M Futures User Data Stream
• Test cases and examples

# Replace LATEST_VERSION with the latest version number and paste the snippet below in pom.xml

<dependency>
    <groupId>io.github.binance</groupId>
    <artifactId>binance-futures-connector-java</artifactId>
    <version>LATEST_VERSION</version>
</dependency>

# "Run mvn install where pom.xml is located to install the dependency.

• Run Example
• The examples are located under src/test/java/examples. Before running the • examples, set up your API_KEY and SECRET_KEY in PrivateConfig.java. This • configuration file is only used for examples, you should reconfigure the • API_KEY and SECRET_KEY when using the library.

# RESTful APIs
* The endpoints are categorized according to the following API documentations:

# Binance USDⓈ-M Futures
# Binance COIN-M Futures
• Each object corresponds to its category which will be used to call its • • respective endpoints.

# Category	Object
* Account/Trades	account
* Market Data	market
* User Data	userData
* Portfolio Margin	portfolioMargin

# Market Endpoint: Exchange Information"
* https://github.com/binance/binance-futures-connector-* * * # java#:~:text=Run%20mvn%20install,Endpoint%3A%20Exchange%20Information

# Market Endpoint: Exchange Information

// UM-Futures
UMFuturesClientImpl client = new UMFuturesClientImpl();
String result = client.market().exchangeInfo();

// CM-Futures
CMFuturesClientImpl client = new CMFuturesClientImpl();
String result = client.market().exchangeInfo();

# Trade Endpoint: Testing a new order

LinkedHashMap<String,Object> parameters = new LinkedHashMap<String,Object>();

UMFuturesClientImpl client = new UMFuturesClientImpl(PrivateConfig.API_KEY, PrivateConfig.SECRET_KEY);

parameters.put("symbol","BTCUSDT");
parameters.put("side", "SELL");
parameters.put("type", "LIMIT");
parameters.put("timeInForce", "GTC");
parameters.put("quantity", 0.01);
parameters.put("price", 9500);

String result = client.trade().testNewOrder(parameters);

# Testnet
/fapi/* and /dapi/* endpoints can be tested in Futures Testnet. You can use it by changing the base URL:

# LinkedHashMap<String,Object> parameters = new LinkedHashMap<>();

UMFuturesClientImpl client = new UMFuturesClientImpl(PrivateConfig.TESTNET_API_KEY, PrivateConfig.TESTNET_SECRET_KEY);
String result = client.market().time();

# Base URL
It's recommended to pass in the baseUrl parameter. If not provided, the default baseUrl for USD-M Futures is https://fapi.binance.com
If not provided, the default baseUrl for COIN-M Futures is https://dapi.binance.com

# Optional parameters
All parameters are read from a LinkedHashMap<String,Object> object where String is the name of the parameter and Object is the value of the parameter. The parameters should follow their exact naming as in the API documentation.

LinkedHashMap<String,Object> parameters = new LinkedHashMap<String,Object>();

• parameters.put("symbol","BTCUSDT");
• parameters.put("side", "SELL");
• parameters.put("type", "LIMIT");
• parameters.put("timeInForce", "GTC");
• parameters.put("quantity", 0.01);
• parameters.put("price", 9500);

# 
Navigation Menu
binance
/
# binance-futures-connector-java

Code
Issues
14
Pull requests
3
Actions
Projects
Security
Insights
We are having a problem billing your account. Please update your payment method or call your payment provider for details on why the transaction failed.
You can contact support with any questions.
Owner avatar
binance-futures-connector-java
Public
binance/binance-futures-connector-java
Folders and files
Name		
Latest commit
aisling-2
aisling-2
v3.0.4
1018ec8
 · 
7 ay önce
History
.github/workflows
v3.0.4 (#25)
7 ay önce
src
v3.0.4
7 ay önce
CHANGELOG.md
v3.0.4 (#25)
7 ay önce
LICENSE.md
first commit
2 yıl önce
README.md
Release 3.0.0
geçen yıl
pom.xml
v3.0.4
7 ay önce
Repository files navigation
README
MIT license
Binance Futures Public API connector Java
License: MIT Code Style

# This is a lightweight library that works as a connector to the Binance Futures API

Supported APIs:
/fapi/*
/dapi/*
/futures/*
USD-M Futures Websocket Market Stream
COIN-M Futures Websocket Market Stream
USD-M Futures User Data Stream
COIN-M Futures User Data Stream
Test cases and examples
Installation
# Replace LATEST_VERSION with the latest version number and paste the snippet below in pom.xml

<dependency>
    <groupId>io.github.binance</groupId>
    <artifactId>binance-futures-connector-java</artifactId>
    <version>LATEST_VERSION</version>
</dependency>
# Run mvn install where pom.xml is located to install the dependency.

Run Example
# The examples are located under src/test/java/examples. Before running the examples, set up your API_KEY and SECRET_KEY in PrivateConfig.java. This configuration file is only used for examples, you should reconfigure the API_KEY and SECRET_KEY when using the library.

# RESTful APIs
The endpoints are categorized according to the following API documentations:

# Binance USDⓈ-M Futures
# Binance COIN-M Futures
# Each object corresponds to its category which will be used to call its respective endpoints.

Category	Object
Account/Trades	account
Market Data	market
User Data	userData
Portfolio Margin	portfolioMargin

# Market Endpoint: Exchange Information
// UM-Futures
UMFuturesClientImpl client = new UMFuturesClientImpl();
String result = client.market().exchangeInfo();

// CM-Futures
CMFuturesClientImpl client = new CMFuturesClientImpl();
String result = client.market().exchangeInfo();
Trade Endpoint: Testing a new order
LinkedHashMap<String,Object> parameters = new LinkedHashMap<String,Object>();

UMFuturesClientImpl client = new UMFuturesClientImpl(PrivateConfig.API_KEY, PrivateConfig.SECRET_KEY);

parameters.put("symbol","BTCUSDT");
parameters.put("side", "SELL");
parameters.put("type", "LIMIT");
parameters.put("timeInForce", "GTC");
parameters.put("quantity", 0.01);
parameters.put("price", 9500);

# String result = client.trade().testNewOrder(parameters);
Testnet
/fapi/* and /dapi/* endpoints can be tested in Futures Testnet. You can use it by changing the base URL:

LinkedHashMap<String,Object> parameters = new LinkedHashMap<>();

UMFuturesClientImpl client = new UMFuturesClientImpl(PrivateConfig.TESTNET_API_KEY, PrivateConfig.TESTNET_SECRET_KEY);
String result = client.market().time();
# Base URL
It's recommended to pass in the baseUrl parameter. If not provided, the default baseUrl for USD-M Futures is https://fapi.binance.com
If not provided, the default baseUrl for COIN-M Futures is https://dapi.binance.com

# Optional parameters
All parameters are read from a LinkedHashMap<String,Object> object where String is the name of the parameter and Object is the value of the parameter. The parameters should follow their exact naming as in the API documentation.

LinkedHashMap<String,Object> parameters = new LinkedHashMap<String,Object>();

parameters.put("symbol","BTCUSDT");
parameters.put("side", "SELL");
parameters.put("type", "LIMIT");
parameters.put("timeInForce", "GTC");
parameters.put("quantity", 0.01);
parameters.put("price", 9500);
Response MetaData
# The Binance API server provides weight usages in the headers of each response. This value can be return by calling setShowLimitUsage and setting it to true.

UMFuturesClientImpl client = new UMFuturesClientImpl();
client.setShowLimitUsage(true);
String result = client.market().time();
logger.info(result);
output:

INFO: {"data":"{"serverTime":1633434339494}","x-mbx-used-weight":"1","x-mbx-used-weight-1m":"1"}
Proxy
HTTP Proxy is supported.

# To set it up, call setProxy() with ProxyAuth and before submitting requests to binance:

CMFuturesClientImpl client = new CMFuturesClientImpl();
Proxy proxyConn = new Proxy(Proxy.Type.HTTP, new InetSocketAddress("127.0.0.1", 8080));
ProxyAuth proxy = new ProxyAuth(proxyConn, null);

client.setProxy(proxy);
logger.info(client.market().time());
For authenticated Proxy, define ProxyAuth with Authenticator from okhttp3:

CMFuturesClientImpl client = new CMFuturesClientImpl();
Proxy proxyConn = new Proxy(Proxy.Type.HTTP, new InetSocketAddress("127.0.0.1", 8080));
    Authenticator auth = new Authenticator() {
    public Request authenticate(Route route, Response response) throws IOException {
        if (response.request().header("Proxy-Authorization") != null) {
            return null; // Give up, we've already failed to authenticate.
          }
      
        String credential = Credentials.basic("username", "password");
        return response.request().newBuilder().header("Proxy-Authorization", credential).build();
        
    }
};
ProxyAuth proxy = new ProxyAuth(proxyConn, auth);

client.setProxy(proxy);
logger.info(client.market().time());
To undo Proxy, use unsetProxy() before submitting requests to binance:

client.unsetProxy();
logger.info(client.market().time());
Complete examples are available to the following folders:

test/java/examples/cm_futures/proxy
test/java/examples/um_futures/proxy
Logging
ch.qos.logback is used for logging in this connector. The configuration xml file can be found under src/main/resources.

Error
There are 3 types of error which may be thrown by this library.

# BinanceConnectorException
This is thrown when there is a validation error for parameters.For instance, mandatory parameter not sent. This error will be thrown before the request is sent to the server.
BinanceClientException
# This is thrown when server returns 4XX, it's an issue from client side.
The error consists of these 3 objects which will help in debugging the error:
httpStatusCode - HTTP status code
errorCode - API Server's error code, e.g. -1102
errMsg - API Server's error message, e.g. Unknown order sent.
# BinanceServerException
This is thrown when server returns 5XX, it's an issue from server side.
try {
      String result = client.trade().newOrder(parameters);
      logger.info(result);
    } catch (BinanceConnectorException e) {
      logger.error("fullErrMessage: {}", e.getMessage(), e);
    } catch (BinanceClientException e) {
      logger.error("fullErrMessage: {} \nerrMessage: {} \nerrCode: {} \nHTTPStatusCode: {}",
      e.getMessage(), e.getErrMsg(), e.getErrorCode(), e.getHttpStatusCode(), e);
    }
# Websocket
UMWebsocketClientImpl client = new UMWebsocketClientImpl(); // defaults to production websocket URL unless stated
int streamID1 = client.aggTradeStream("btcusdt",((event) -> {
    System.out.println(event);
}));

//Combining Streams
ArrayList<String> streams = new ArrayList<>();
streams.add("btcusdt@trade");
streams.add("bnbusdt@trade");

int streamID2 = client.combineStreams(streams, ((event) -> {
    System.out.println(event);
}));

//Listening to User Data Stream
int streamID3 = client.listenUserStream(listenKey, ((event) -> {
  System.out.println(event);
}));

//Closing a single stream
client.closeConnection(streamID1); //closes aggTradeStream-btcusdt

//Closing all streams
client.closeAllConnections();
More websocket examples are available in the test/examples folder

# Test
mvn clean test

# Contributing
Contributions are welcome.
If you've found a bug within this project, please open an issue to discuss what you would like to change.
If it's an issue with the API, please open a topic at Binance Developer Community
