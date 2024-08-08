# Binance-api-doc

* mkdocs is required 
* view https://binanceapitest.github.io/Binance-api-doc/
2024-07-04
Changes to Simple Earn endpoints:
POST /sapi/v1/simple-earn/locked/subscribe new parameter:redeemTo
GET /sapi/v1/simple-earn/locked/position new fields in response:redeemTo
GET /sapi/v1/simple-earn/flexible/history/subscriptionRecord new fields in response:productId
GET /sapi/v1/simple-earn/locked/history/subscriptionRecord new fields in response:projectId
GET /sapi/v1/simple-earn/locked/history/redemptionRecord new fields in response:originalAmount, lossAmount, isComplete, rewardAsset, rewardAmt, extraRewardAsset, estExtraRewardAmt
Add New endpoint in Simple Earn：
POST /sapi/v1/simple-earn/locked/setRedeemOption Set the redeem option of Locked products to Flexible product or Spot wallet
2023-08-26
Changes to Simple Earn endpoints:
GET /sapi/v1/simple-earn/flexible/history/subscriptionRecord: new fields in response: sourceAccount,amtFromSpot,amtFromFunding
GET /sapi/v1/simple-earn/locked/history/subscriptionRecord: new fields in response: sourceAccount，amtFromSpot,amtFromFunding
GET /sapi/v1/simple-earn/flexible/history/redemptionRecord: new fields in response destAccount
POST /sapi/v1/simple-earn/flexible/subscribe: new parameter sourceAccount
POST /sapi/v1/simple-earn/locked/subscribe: new parameter sourceAccount
POST /sapi/v1/simple-earn/flexible/redeem: new parameter destAccount[Binance api key.txt.json](https://github.com/user-attachments/files/16538990/Binance.api.key.txt.json)

