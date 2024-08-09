From 8c13ec52d11e57804adce4c76ef1e2779a318b65 Mon Sep 17 00:00:00 2001
From: Recep <148443421+zxramozx@users.noreply.github.com>
Date: Fri, 9 Aug 2024 10:15:06 +0300
Subject: [PATCH] Update README.md
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit

# Binance-api-doc

* mkdocs is required
* view https://binanceapitest.github.io/Binance-api-doc/
* https://binanceapitest.github.io/Binance-api-doc/
```Html
POST /binancepay/openapi/wallet/transfer ```

## Request Parameters
Attributes	Type	Required	Limitation	Description
requestId	string	Y	maximum length 32	Represents the unique ID of each transfer request.Generated by the merchant
currency	string	Y	Valid currency, must be in uppercase	transfer currency, e.g. "USDT"
amount	string	Y	Amount Range: 0.00000001 - 999999999999999.99999999, each currency amount has a precision, see the info from api refer to	the transfer amount
transferType	string	Y	Only "TO_MAIN" OR "TO_PAY"	The transfer direction specified by the merchant. TO_MAIN means to spot wallet, TO_PAY means to funding wallet

## Sample Request Body#

{
  "requestId": "100002021071407140001",
  "currency": "BNB",
  "amount": "0.01",
  "transferType": "TO_MAIN"
}


** Binance Logo
Merchant Acquiring (C2B)API SpecificationTransfer fundTransfer Fund
On this page
Transfer Fund
Fund transfer API used for merchant/partner to initiate Fund transfer between wallets.

EndPoint
** POST /binancepay/openapi/wallet/transfer

## Request Parameters
Attributes	Type	Required	Limitation	Description
requestId	string	Y	maximum length 32	Represents the unique ID of each transfer request.Generated by the merchant
currency	string	Y	Valid currency, must be in uppercase	transfer currency, e.g. "USDT"
amount	string	Y	Amount Range: 0.00000001 - 999999999999999.99999999, each currency amount has a precision, see the info from api refer to	the transfer amount
transferType	string	Y	Only "TO_MAIN" OR "TO_PAY"	The transfer direction specified by the merchant. TO_MAIN means to spot wallet, TO_PAY means to funding wallet
Sample Request Body
{
  "requestId": "100002021071407140001",
  "currency": "BNB",
  "amount": "0.01",
  "transferType": "TO_MAIN"
}

## Response Parameters
Attributes	Type	Required	Limitation	Description
status	string	Y	"SUCCESS" or "FAIL"	status of the API request
code	string	Y	-	request result code, refer to
data	TransferResult	N	-	response body, refer to
errorMessage	string	N	maximum length 256
Child Attribute
TransferResult

## Attributes	Type	Required	Limitation	Description
tranId	string	Y	-	the value of Request property requestId
status	string	Y	SUCCESS OR FAILURE OR PROCESS	SUCCESS (indicating that the transfer is completely successful), FAILURE (indicating that the transfer has failed, it may be that the transferor has a problem with the transferee), PROCESS (the transfer is in progress)
currency	string	Y	transfer currency
amount	string	Y	transfer amount
transferType	string	Y	transfer type
Sample Response
{
  "status": "SUCCESS",
  "code": "000000",
  "data": {
    "tranId": "100002021071407140001",
    "status": "SUCCESS",
    "currency": "BNB",
    "amount": "0.01",
    "transferType": "TO_MAIN"
  },
  "errorMessage": ""
}

## Sample Response For Idempotent Request
{
  "status": "REPEAT_REQ_SUCCESS",
  "code": "000001",
  "data": {
    "tranId": "100002021071407140001",
    "status": "SUCCESS",
    "currency": "BNB",
    "amount": "0.01",
    "transferType": "TO_MAIN"
  },
  "errorMessage": ""
}

## Result Code

• Name	Code	Reason	Solution
• UNKNOWN_ERROR	400000	An unknown error occurred while processing the request.	Try again later
• INVALID_REQUEST	400001	Parameter format is wrong or parameter transferring doesn't follow the rules.	Please check •whether the parameters are correct.
INVALID_SIGNATURE	400002	Incorrect signature result	Check whether the signature parameter and method comply with signature algorithm requirements.
INVALID_TIMESTAMP	400003	Timestamp for this request is outside of the time window.	Sync server clock
INVALID_API_KEY_OR_IP	400004	API identity key not found or invalid.	Check API identity key
BAD_API_KEY_FMT	400005	API identity key format invalid.	Check API identity key.
BAD_HTTP_METHOD	400006	Request method not supported.	Check Request method.
MEDIA_TYPE_NOT_SUPPORTED	400007	Media type not supported.	Check Request Media type.
INVALID_REQUEST_BODY	400008	Request body is not a valid json object.	Check Request body
REPEAT_REQ_INCONSISTENT	400009	Request repeated, but your request body is different from the last request.	Check Request body
MANDATORY_PARAM_EMPTY_OR_MALFORMED	400100	A parameter was missing/empty/null, or malformed.
INVALID_PARAM_WRONG_LENGTH	400101	A parameter was not valid, was empty/null, or too long/short, or wrong format.
INVALID_PARAM_WRONG_VALUE	400102	A parameter was not valid, the value is out of range.
INVALID_PARAM_ILLEGAL_CHAR	400103	A parameter was not valid, contains illegal characters
INVALID_REQUEST_TOO_LARGE	400104	Invalid request, content length too large
INVALID_ACCOUNT_STATUS	400203	Not support for this account, please check account status.
PAYMENT_ACTION_TOO_FREQUENT	400501	action Too Frequent, get the lock fail	Try again later
PAYMENT_INSUFFICIENT_BALANCE	400611	Insufficient Balance
assetDigitApi
GEt https://www.binance.com/bapi/asset/v2/public/asset/asset/get-all-asset

Attributes	Type	Required	Limitation	Description
assetCode	string	Y	-	currency code
assetDigit	long	Y	-	decimal precision
---
 README.md | 115 ++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 115 insertions(+)

diff --git a/README.md b/README.md
index fe4ca14..e9d7977 100644
--- a/README.md
+++ b/README.md
@@ -3,3 +3,118 @@
 * mkdocs is required 
 * view https://binanceapitest.github.io/Binance-api-doc/
 
+```Html
+POST /binancepay/openapi/wallet/transfer ```
+
+## Request Parameters
+Attributes	Type	Required	Limitation	Description
+requestId	string	Y	maximum length 32	Represents the unique ID of each transfer request.Generated by the merchant
+currency	string	Y	Valid currency, must be in uppercase	transfer currency, e.g. "USDT"
+amount	string	Y	Amount Range: 0.00000001 - 999999999999999.99999999, each currency amount has a precision, see the info from api refer to	the transfer amount
+transferType	string	Y	Only "TO_MAIN" OR "TO_PAY"	The transfer direction specified by the merchant. TO_MAIN means to spot wallet, TO_PAY means to funding wallet
+
+## Sample Request Body#
+
+{
+  "requestId": "100002021071407140001",
+  "currency": "BNB",
+  "amount": "0.01",
+  "transferType": "TO_MAIN"
+}
+
+
+** Binance Logo
+Merchant Acquiring (C2B)API SpecificationTransfer fundTransfer Fund
+On this page
+Transfer Fund
+Fund transfer API used for merchant/partner to initiate Fund transfer between wallets.
+
+EndPoint
+** POST /binancepay/openapi/wallet/transfer
+
+## Request Parameters
+Attributes	Type	Required	Limitation	Description
+requestId	string	Y	maximum length 32	Represents the unique ID of each transfer request.Generated by the merchant
+currency	string	Y	Valid currency, must be in uppercase	transfer currency, e.g. "USDT"
+amount	string	Y	Amount Range: 0.00000001 - 999999999999999.99999999, each currency amount has a precision, see the info from api refer to	the transfer amount
+transferType	string	Y	Only "TO_MAIN" OR "TO_PAY"	The transfer direction specified by the merchant. TO_MAIN means to spot wallet, TO_PAY means to funding wallet
+Sample Request Body
+{
+  "requestId": "100002021071407140001",
+  "currency": "BNB",
+  "amount": "0.01",
+  "transferType": "TO_MAIN"
+}
+
+## Response Parameters
+Attributes	Type	Required	Limitation	Description
+status	string	Y	"SUCCESS" or "FAIL"	status of the API request
+code	string	Y	-	request result code, refer to
+data	TransferResult	N	-	response body, refer to
+errorMessage	string	N	maximum length 256	
+Child Attribute
+TransferResult
+
+## Attributes	Type	Required	Limitation	Description
+tranId	string	Y	-	the value of Request property requestId
+status	string	Y	SUCCESS OR FAILURE OR PROCESS	SUCCESS (indicating that the transfer is completely successful), FAILURE (indicating that the transfer has failed, it may be that the transferor has a problem with the transferee), PROCESS (the transfer is in progress)
+currency	string	Y	transfer currency	
+amount	string	Y	transfer amount	
+transferType	string	Y	transfer type	
+Sample Response
+{
+  "status": "SUCCESS",
+  "code": "000000",
+  "data": {
+    "tranId": "100002021071407140001",
+    "status": "SUCCESS",
+    "currency": "BNB",
+    "amount": "0.01",
+    "transferType": "TO_MAIN"
+  },
+  "errorMessage": ""
+}
+
+## Sample Response For Idempotent Request
+{
+  "status": "REPEAT_REQ_SUCCESS",
+  "code": "000001", 
+  "data": {
+    "tranId": "100002021071407140001",
+    "status": "SUCCESS",
+    "currency": "BNB",
+    "amount": "0.01",
+    "transferType": "TO_MAIN"
+  },
+  "errorMessage": ""
+}
+
+## Result Code
+
+• Name	Code	Reason	Solution
+• UNKNOWN_ERROR	400000	An unknown error occurred while processing the request.	Try again later
+• INVALID_REQUEST	400001	Parameter format is wrong or parameter transferring doesn't follow the rules.	Please check •whether the parameters are correct.
+INVALID_SIGNATURE	400002	Incorrect signature result	Check whether the signature parameter and method comply with signature algorithm requirements.
+INVALID_TIMESTAMP	400003	Timestamp for this request is outside of the time window.	Sync server clock
+INVALID_API_KEY_OR_IP	400004	API identity key not found or invalid.	Check API identity key
+BAD_API_KEY_FMT	400005	API identity key format invalid.	Check API identity key.
+BAD_HTTP_METHOD	400006	Request method not supported.	Check Request method.
+MEDIA_TYPE_NOT_SUPPORTED	400007	Media type not supported.	Check Request Media type.
+INVALID_REQUEST_BODY	400008	Request body is not a valid json object.	Check Request body
+REPEAT_REQ_INCONSISTENT	400009	Request repeated, but your request body is different from the last request.	Check Request body
+MANDATORY_PARAM_EMPTY_OR_MALFORMED	400100	A parameter was missing/empty/null, or malformed.	
+INVALID_PARAM_WRONG_LENGTH	400101	A parameter was not valid, was empty/null, or too long/short, or wrong format.	
+INVALID_PARAM_WRONG_VALUE	400102	A parameter was not valid, the value is out of range.	
+INVALID_PARAM_ILLEGAL_CHAR	400103	A parameter was not valid, contains illegal characters	
+INVALID_REQUEST_TOO_LARGE	400104	Invalid request, content length too large	
+INVALID_ACCOUNT_STATUS	400203	Not support for this account, please check account status.	
+PAYMENT_ACTION_TOO_FREQUENT	400501	action Too Frequent, get the lock fail	Try again later
+PAYMENT_INSUFFICIENT_BALANCE	400611	Insufficient Balance	
+assetDigitApi
+GEt https://www.binance.com/bapi/asset/v2/public/asset/asset/get-all-asset
+
+Attributes	Type	Required	Limitation	Description
+assetCode	string	Y	-	currency code
+assetDigit	long	Y	-	decimal precision
+ 
+
