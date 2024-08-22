
# Most of the endpoints can be used in the testnet platform.
# The REST baseurl for testnet is "https://testnet.binancefuture.com"
# The Websocket baseurl for testnet is "wss://stream.binancefuture.com"
#SDK and Code Demonstration
Disclaimer:

# The following SDKs are provided by partners and users, and are not officially produced. They are only used to help users become familiar with the API endpoint. Please use it with caution and expand R&D according to your own situation.
# Binance does not make any commitment to the safety and performance of the SDKs, nor will be liable for the risks or even losses caused by using the SDKs.
# Python3
# SDK: To get the provided SDK for Binance Futures Connector,
# please visit https://github.com/binance/binance-futures-connector-python,
or use the command below:
# pip install binance-futures-connector

-Java
# To get the provided -SDK for Binance -Futures,
# please visit --https://github.com/bin-ance/binance-futures--connector-java,
# or use the command below:
# git clone https://github.com/binance/binance-futures-connector-java.git

# General API Information
# Some endpoints will require an API Key. Please refer to this page
# The base endpoint is: https://fapi.binance.com
# All endpoints return either a JSON object or array.
# Data is returned in ascending order. Oldest first, newest last.
# All time and timestamp related fields are in milliseconds.
# All data types adopt definition in JAVA.

# ./General Information on Endpoints
# ./For GET endpoints, parameters must be sent as a query string.
# ./For POST, PUT, and DELETE endpoints, the parameters may be sent as a query string or in the request body with content type application/x-www-form-urlencoded. You may mix parameters between both the query string and request body if you wish to do so.
# ./Parameters may be sent in any order.
# ./If a parameter sent in both the query string and request body, the query string parameter will be used.
# ./LIMITS
# ./The /fapi/v1/exchangeInfo rateLimits array contains objects related to the exchange's RAW_REQUEST, REQUEST_WEIGHT, and ORDER rate limits. These are further defined in the ENUM definitions section under Rate limiters (rateLimitType).
# ./A 429 will be returned when either rate limit is violated.
# ./Binance has the right to further tighten the rate limits on users with intent to attack.
-IP Limits
# ./Every request will contain X-MBX-USED-WEIGHT-(intervalNum)(intervalLetter) in the response headers which has the current used weight for the IP for all request rate limiters defined.
# ./Each route has a weight which determines for the number of requests each endpoint counts for. Heavier endpoints and endpoints that do operations on multiple symbols will have a heavier weight.
# ./When a 429 is received, it's your obligation as an API to back off and not spam the API.
# ./Repeatedly violating rate limits and/or failing to back off after receiving 429s will result in an automated IP ban (HTTP status 418).
# ./IP bans are tracked and scale in duration for repeat offenders, from 2 minutes to 3 days.
The limits on the API are based on the IPs, not the API keys.
It is strongly recommended to use websocket stream for getting data as much as possible, which can not only ensure the timeliness of the message, but also reduce the access restriction pressure caused by the request.
Order Rate Limits
Every order response will contain a X-MBX-ORDER-COUNT-(intervalNum)(intervalLetter) header which has the current order count for the account for all order rate limiters defined.
Rejected/unsuccessful orders are not guaranteed to have X-MBX-ORDER-COUNT-** headers in the response.
The order rate limit is counted against each account.
Endpoint Security Type
Each endpoint has a security type that determines the how you will interact with it.
API-keys are passed into the Rest API via the X-MBX-APIKEY header.
API-keys and secret-keys are case sensitive.
API-keys can be configured to only access certain types of secure endpoints. For example, one API-key could be used for TRADE only, while another API-key can access everything except for TRADE routes.
By default, API-keys can access all secure routes.
Security Type	Description
NONE	Endpoint can be accessed freely.
TRADE	Endpoint requires sending a valid API-Key and signature.
USER_DATA	Endpoint requires sending a valid API-Key and signature.
USER_STREAM	Endpoint requires sending a valid API-Key.
MARKET_DATA	Endpoint requires sending a valid API-Key.
TRADE and USER_DATA endpoints are SIGNED endpoints.
SIGNED (TRADE and USER_DATA) Endpoint Security
SIGNED endpoints require an additional parameter, signature, to be sent in the query string or request body.
Endpoints use HMAC SHA256 signatures. The HMAC SHA256 signature is a keyed HMAC SHA256 operation. Use your secretKey as the key and totalParams as the value for the HMAC operation.
The signature is not case sensitive.
Please make sure the signature is the end part of your query string or request body.
totalParams is defined as the query string concatenated with the request body.
Timing Security
A SIGNED endpoint also requires a parameter, timestamp, to be sent which should be the millisecond timestamp of when the request was created and sent.
An additional parameter, recvWindow, may be sent to specify the number of milliseconds after timestamp the request is valid for. If recvWindow is not sent, it defaults to 5000.
The logic is as follows:

if (timestamp < serverTime + 1000 && serverTime - timestamp <= recvWindow) {
  // process request
} else {
  // reject request
}


Serious trading is about timing. Networks can be unstable and unreliable, which can lead to requests taking varying amounts of time to reach the servers. With recvWindow, you can specify that the request must be processed within a certain number of milliseconds or be rejected by the server.

It is recommended to use a small recvWindow of 5000 or less!
SIGNED Endpoint Examples for POST /fapi/v1/order - HMAC Keys
Here is a step-by-step example of how to send a vaild signed payload from the Linux command line using echo, openssl, and curl.

Key	Value
apiKey	dbefbc809e3e83c283a984c3a1459732ea7db1360ca80c5c2c8867408d28cc83
secretKey	2b5eb11e18796d12d88f13dc27dbbd02c2cc51ff7059765ed9821957d82bb4d9
Parameter	Value
symbol	BTCUSDT
side	BUY
type	LIMIT
timeInForce	GTC
quantity	1
price	9000
recvWindow	5000
timestamp	1591702613943
Example 1: As a query string
Example 1

HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=9000&timeInForce=GTC&recvWindow=5000&timestamp=1591702613943" | openssl dgst -sha256 -hmac "2b5eb11e18796d12d88f13dc27dbbd02c2cc51ff7059765ed9821957d82bb4d9"
    (stdin)= 3c661234138461fcc7a7d8746c6558c9842d4e10870d2ecbedf7777cad694af9


curl command:

    (HMAC SHA256)
    $ curl -H "X-MBX-APIKEY: dbefbc809e3e83c283a984c3a1459732ea7db1360ca80c5c2c8867408d28cc83" -X POST 'https://fapi/binance.com/fapi/v1/order?symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=9000&timeInForce=GTC&recvWindow=5000&timestamp=1591702613943&signature= 3c661234138461fcc7a7d8746c6558c9842d4e10870d2ecbedf7777cad694af9'


queryString:

symbol=BTCUSDT
&side=BUY
&type=LIMIT
&timeInForce=GTC
&quantity=1
&price=9000
&recvWindow=5000
&timestamp=1591702613943

Example 2: As a request body
Example 2

HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=9000&timeInForce=GTC&recvWindow=5000&timestamp=1591702613943" | openssl dgst -sha256 -hmac "2b5eb11e18796d12d88f13dc27dbbd02c2cc51ff7059765ed9821957d82bb4d9"
    (stdin)= 3c661234138461fcc7a7d8746c6558c9842d4e10870d2ecbedf7777cad694af9


curl command:

    (HMAC SHA256)
    $ curl -H "X-MBX-APIKEY: dbefbc809e3e83c283a984c3a1459732ea7db1360ca80c5c2c8867408d28cc83" -X POST 'https://fapi/binance.com/fapi/v1/order' -d 'symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=9000&timeInForce=GTC&recvWindow=5000&timestamp=1591702613943&signature= 3c661234138461fcc7a7d8746c6558c9842d4e10870d2ecbedf7777cad694af9'


requestBody:

symbol=BTCUSDT
&side=BUY
&type=LIMIT
&timeInForce=GTC
&quantity=1
&price=9000
&recvWindow=5000
&timestamp=1591702613943

Example 3: Mixed query string and request body
Example 3

HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&timeInForce=GTCquantity=1&price=9000&recvWindow=5000&timestamp= 1591702613943" | openssl dgst -sha256 -hmac "2b5eb11e18796d12d88f13dc27dbbd02c2cc51ff7059765ed9821957d82bb4d9"
    (stdin)= f9d0ae5e813ef6ccf15c2b5a434047a0181cb5a342b903b367ca6d27a66e36f2


curl command:

    (HMAC SHA256)
    $ curl -H "X-MBX-APIKEY: dbefbc809e3e83c283a984c3a1459732ea7db1360ca80c5c2c8867408d28cc83" -X POST 'https://fapi.binance.com/fapi/v1/order?symbol=BTCUSDT&side=BUY&type=LIMIT&timeInForce=GTC' -d 'quantity=1&price=9000&recvWindow=5000&timestamp=1591702613943&signature=f9d0ae5e813ef6ccf15c2b5a434047a0181cb5a342b903b367ca6d27a66e36f2'


queryString: symbol=BTCUSDT&side=BUY&type=LIMIT&timeInForce=GTC
requestBody: quantity=1&price=9000&recvWindow=5000&timestamp= 1591702613943
Note that the signature is different in example 3.
There is no & between "GTC" and "quantity=1".

SIGNED Endpoint Examples for POST /fapi/v1/order - RSA Keys
This will be a step by step process how to create the signature payload to send a valid signed payload.
We support PKCS#8 currently.
To get your API key, you need to upload your RSA Public Key to your account and a corresponding API key will be provided for you.
For this example, the private key will be referenced as test-prv-key.pem

Key	Value
apiKey	vE3BDAL1gP1UaexugRLtteaAHg3UO8Nza20uexEuW1Kh3tVwQfFHdAiyjjY428o2
Parameter	Value
symbol	BTCUSDT
side	SELL
type	MARKET
quantity	1.23
recvWindow	9999999
timestamp	1671090801999
Signature payload (with the listed parameters):

timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23


Step 1: Construct the payload

Arrange the list of parameters into a string. Separate each parameter with a &.

Step 2: Compute the signature:

2.1 - Encode signature payload as ASCII data.

Step 2.2

 $ echo -n 'timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23' | openssl dgst -keyform PEM -sha256 -sign ./test-prv-key.pem


2.2 - Sign payload using RSASSA-PKCS1-v1_5 algorithm with SHA-256 hash function.

Step 2.3

$ echo -n 'timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23' | openssl dgst -keyform PEM -sha256 -sign ./test-prv-key.pem | openssl enc -base64
aap36wD5loVXizxvvPI3wz9Cjqwmb3KVbxoym0XeWG1jZq8umqrnSk8H8dkLQeySjgVY91Ufs%2BBGCW%2B4sZjQEpgAfjM76riNxjlD3coGGEsPsT2lG39R%2F1q72zpDs8pYcQ4A692NgHO1zXcgScTGgdkjp%2Brp2bcddKjyz5XBrBM%3D


2.3 - Encode output as base64 string.

Step 2.4

$  echo -n 'timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23' | openssl dgst -keyform PEM -sha256 -sign ./test-prv-key.pem | openssl enc -base64 | tr -d '\n'
aap36wD5loVXizxvvPI3wz9Cjqwmb3KVbxoym0XeWG1jZq8umqrnSk8H8dkLQeySjgVY91Ufs%2BBGCW%2B4sZjQEpgAfjM76riNxjlD3coGGEsPsT2lG39R%2F1q72zpDs8pYcQ4A692NgHO1zXcgScTGgdkjp%2Brp2bcddKjyz5XBrBM%3D


2.4 - Delete any newlines in the signature.

Step 2.5

aap36wD5loVXizxvvPI3wz9Cjqwmb3KVbxoym0XeWG1jZq8umqrnSk8H8dkLQeySjgVY91Ufs%2BBGCW%2B4sZjQEpgAfjM76riNxjlD3coGGEsPsT2lG39R%2F1q72zpDs8pYcQ4A692NgHO1zXcgScTGgdkjp%2Brp2bcddKjyz5XBrBM%3D


2.5 - Since the signature may contain / and =, this could cause issues with sending the request. So the signature has to be URL encoded.

Step 2.6

 curl -H "X-MBX-APIKEY: vE3BDAL1gP1UaexugRLtteaAHg3UO8Nza20uexEuW1Kh3tVwQfFHdAiyjjY428o2" -X POST 'https://fapi.binance.com/fapi/v1/order?timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23&signature=aap36wD5loVXizxvvPI3wz9Cjqwmb3KVbxoym0XeWG1jZq8umqrnSk8H8dkLQeySjgVY91Ufs%2BBGCW%2B4sZjQEpgAfjM76riNxjlD3coGGEsPsT2lG39R%2F1q72zpDs8pYcQ4A692NgHO1zXcgScTGgdkjp%2Brp2bcddKjyz5XBrBM%3D'


2.6 - curl command

Bash script

#!/usr/bin/env bash

# Set up authentication:
# ./apiKey="vE3BDAL1gP1UaexugRLtteaAHg3UO8Nza20uexEuW1Kh3tVwQfFHdAiyjjY428o2"   ### REPLACE THIS WITH YOUR API KEY

# Set up the request:
apiMethod="POST"
apiCall="v1/order"
apiParams="timestamp=1671090801999&recvWindow=9999999&symbol=BTCUSDT&side=SELL&type=MARKET&quantity=1.23"
function rawurlencode {
    local value="$1"
    local len=${#value}
    local encoded=""
    local pos c o
    for (( pos=0 ; pos<len ; pos++ ))
    do
        c=${value:$pos:1}
        case "$c" in
            [-_.~a-zA-Z0-9] ) o="${c}" ;;
            * )   printf -v o '%%%02x' "'$c"
        esac
        encoded+="$o"
    done
    echo "$encoded"
}
ts=$(date +%s000)
paramsWithTs="$apiParams&timestamp=$ts"
rawSignature=$(echo -n "$paramsWithTs" \
               | openssl dgst -keyform PEM -sha256 -sign ./test-prv-key.pem \  ### THIS IS YOUR PRIVATE KEY. DO NOT SHARE THIS FILE WITH ANYONE.
               | openssl enc -base64 \
               | tr -d '\n')
signature=$(rawurlencode "$rawSignature")
curl -H "X-MBX-APIKEY: $apiKey" -X $apiMethod \
    "https://fapi.binance.com/fapi/$apiCall?$paramsWithTs&signature=$signature"


# ./A sample Bash script containing similar steps is available in the right side.

 # ./Postman Collections
# ./There is now a Postman collection containing the API endpoints for quick and easy use.

# ./For more information please refer to this page: Binance API Postman

Previous
Quick Start
Next
Websocket API General Info
Copyright © 2024 Binance.
