<?xml version="1.0" encoding="UTF-8"?>
<sbe:messageSchema xmlns:mbx="https://binance-docs.github.io/apidocs/spot/en/"
                   xmlns:sbe="http://fixprotocol.io/2016/sbe"
                   xmlns:xi="http://www.w3.org/2001/XInclude"
                   package="spot_sbe"
                   id="2"
                   version="0"
                   semanticVersion="5.2"
                   description="Spot SBE message schema"
                   byteOrder="littleEndian">
    <types>
        <composite name="messageHeader" description="Template ID and length of message root">
            <type name="blockLength" primitiveType="uint16"/>
            <type name="templateId" primitiveType="uint16"/>
            <type name="schemaId" primitiveType="uint16"/>
            <type name="version" primitiveType="uint16"/>
        </composite>

        <composite name="groupSizeEncoding" description="Repeating group dimensions.">
            <type name="blockLength" primitiveType="uint16"/>
            <type name="numInGroup" primitiveType="uint32" maxValue="2147483647"/>
        </composite>

        <composite name="groupSize16Encoding" description="Repeating group dimensions.">
            <type name="blockLength" primitiveType="uint16"/>
            <type name="numInGroup" primitiveType="uint16"/>
        </composite>

        <composite name="varString" description="Variable length UTF-8 string.">
            <type name="length" primitiveType="uint16"/>
            <type name="varData" length="0" primitiveType="uint8" characterEncoding="UTF-8"/>
        </composite>

        <composite name="varString8" description="Variable length UTF-8 string.">
            <type name="length" primitiveType="uint8"/>
            <type name="varData" length="0" primitiveType="uint8" characterEncoding="UTF-8"/>
        </composite>

        <composite name="optionalVarString" description="Variable length UTF-8 string where an empty string means null.">
            <type name="length" primitiveType="uint16"/>
            <type name="varData" length="0" primitiveType="uint8" characterEncoding="UTF-8"/>
        </composite>

        <composite name="optionalVarString8" description="Variable length UTF-8 string where an empty string means null.">
            <type name="length" primitiveType="uint8"/>
            <type name="varData" length="0" primitiveType="uint8" characterEncoding="UTF-8"/>
        </composite>

        <composite name="messageData" description="Message header plus SBE-encoded message.">
            <type name="length" primitiveType="uint32" maxValue="2147483647"/>
            <type name="varData" length="0" primitiveType="uint8"/>
        </composite>

        <composite name="messageData16" description="Message header plus SBE-encoded message.">
            <type name="length" primitiveType="uint16"/>
            <type name="varData" length="0" primitiveType="uint8"/>
        </composite>

        <composite name="messageData8" description="Message header plus SBE-encoded message.">
            <type name="length" primitiveType="uint8"/>
            <type name="varData" length="0" primitiveType="uint8"/>
        </composite>

        <composite name="optionalMessageData" description="Message header plus SBE-encoded message where 0-length means null.">
            <type name="length" primitiveType="uint32" maxValue="2147483647"/>
            <type name="varData" length="0" primitiveType="uint8"/>
        </composite>

        <composite name="optionalMessageData16" description="Message header plus SBE-encoded message where 0-length means null.">
            <type name="length" primitiveType="uint16"/>
            <type name="varData" length="0" primitiveType="uint8"/>
        </composite>

        <type name="mantissa64" primitiveType="int64" description="
            64-bit mantissa for a decimal floating point number. The name of
            the field containing the exponent value is specified in the
            mbx:exponent attribute of the mantissa64 field. The exponent field
            will always precede the mantissa field."
        />
        <type name="mantissa128" length="16" primitiveType="uint8" description="
            Signed 128-bit mantissa for a decimal floating point number
            represented as a little-endian byte array. The name of the field
            containing the exponent value is specified in the mbx:exponent
            attribute of the mantissa128 field. The exponent field will always
            precede the mantissa field. Following the convention set by the
            FIX SBE Standard, the value −2^127 is nullValue by default."
        />
        <type name="exponent8" primitiveType="int8" description="
            Exponent for a decimal floating point number."
        />

        <type name="aggTradeId" primitiveType="int64"/>
        <type name="allocId" primitiveType="int64"/>
        <type name="orderId" primitiveType="int64"/>
        <type name="orderListId" primitiveType="int64"/>
        <type name="preventedMatchId" primitiveType="int64"/>
        <type name="tradeGroupId" primitiveType="int64"/>
        <type name="tradeId" primitiveType="int64"/>
        <type name="updateId" primitiveType="int64"/>
        <type name="utcTimestampUs" primitiveType="int64" description="UTC timestamp in microseconds"/>

        <enum name="boolEnum" encodingType="uint8">
            <validValue name="False">0</validValue>
            <validValue name="True">1</validValue>
        </enum>

        <enum name="rateLimitType" encodingType="uint8">
            <validValue name="RawRequests" mbx:jsonValue="RAW_REQUESTS">0</validValue>
            <validValue name="Connections" mbx:jsonValue="CONNECTIONS">1</validValue>
            <validValue name="RequestWeight" mbx:jsonValue="REQUEST_WEIGHT">2</validValue>
            <validValue name="Orders" mbx:jsonValue="ORDERS">3</validValue>
        </enum>
        <enum name="rateLimitInterval" encodingType="uint8">
            <validValue name="Second" mbx:jsonValue="SECOND">0</validValue>
            <validValue name="Minute" mbx:jsonValue="MINUTE">1</validValue>
            <validValue name="Hour" mbx:jsonValue="HOUR">2</validValue>
            <validValue name="Day" mbx:jsonValue="DAY">3</validValue>
        </enum>

        <enum name="filterType" encodingType="uint8">
            <validValue name="MaxPosition" mbx:jsonValue="MAX_POSITION">0</validValue>
            <validValue name="PriceFilter" mbx:jsonValue="PRICE_FILTER">1</validValue>
            <validValue name="TPlusSell" mbx:jsonValue="T_PLUS_SELL">2</validValue>
            <validValue name="LotSize" mbx:jsonValue="LOT_SIZE">3</validValue>
            <validValue name="MaxNumOrders" mbx:jsonValue="MAX_NUM_ORDERS">4</validValue>
            <validValue name="MinNotional" mbx:jsonValue="MIN_NOTIONAL">5</validValue>
            <validValue name="MaxNumAlgoOrders" mbx:jsonValue="MAX_NUM_ALGO_ORDERS">6</validValue>
            <validValue name="ExchangeMaxNumOrders" mbx:jsonValue="EXCHANGE_MAX_NUM_ORDERS">7</validValue>
            <validValue name="ExchangeMaxNumAlgoOrders" mbx:jsonValue="EXCHANGE_MAX_NUM_ALGO_ORDERS">8</validValue>
            <validValue name="IcebergParts" mbx:jsonValue="ICEBERG_PARTS">9</validValue>
            <validValue name="MarketLotSize" mbx:jsonValue="MARKET_LOT_SIZE">10</validValue>
            <validValue name="PercentPrice" mbx:jsonValue="PERCENT_PRICE">11</validValue>
            <validValue name="MaxNumIcebergOrders" mbx:jsonValue="MAX_NUM_ICEBERG_ORDERS">12</validValue>
            <validValue name="ExchangeMaxNumIcebergOrders" mbx:jsonValue="EXCHANGE_MAX_NUM_ICEBERG_ORDERS">13</validValue>
            <validValue name="TrailingDelta" mbx:jsonValue="TRAILING_DELTA">14</validValue>
            <validValue name="PercentPriceBySide" mbx:jsonValue="PERCENT_PRICE_BY_SIDE">15</validValue>
            <validValue name="Notional" mbx:jsonValue="NOTIONAL">16</validValue>
        </enum>

        <enum name="symbolStatus" encodingType="uint8">
            <validValue name="PreTrading" mbx:jsonValue="PRE_TRADING">0</validValue>
            <validValue name="Trading" mbx:jsonValue="TRADING">1</validValue>
            <validValue name="PostTrading" mbx:jsonValue="POST_TRADING">2</validValue>
            <validValue name="EndOfDay" mbx:jsonValue="END_OF_DAY">3</validValue>
            <validValue name="Halt" mbx:jsonValue="HALT">4</validValue>
            <validValue name="AuctionMatch" mbx:jsonValue="AUCTION_MATCH">5</validValue>
            <validValue name="Break" mbx:jsonValue="BREAK">7</validValue>
        </enum>

        <enum name="orderType" encodingType="uint8">
            <validValue name="Market" mbx:jsonValue="MARKET">0</validValue>
            <validValue name="Limit" mbx:jsonValue="LIMIT">1</validValue>
            <validValue name="StopLoss" mbx:jsonValue="STOP_LOSS">2</validValue>
            <validValue name="StopLossLimit" mbx:jsonValue="STOP_LOSS_LIMIT">3</validValue>
            <validValue name="TakeProfit" mbx:jsonValue="TAKE_PROFIT">4</validValue>
            <validValue name="TakeProfitLimit" mbx:jsonValue="TAKE_PROFIT_LIMIT">5</validValue>
            <validValue name="LimitMaker" mbx:jsonValue="LIMIT_MAKER">6</validValue>
        </enum>

        <set name="orderTypes" encodingType="uint16">
            <choice name="Market" mbx:jsonValue="MARKET">0</choice>
            <choice name="Limit" mbx:jsonValue="LIMIT">1</choice>
            <choice name="StopLoss" mbx:jsonValue="STOP_LOSS">2</choice>
            <choice name="StopLossLimit" mbx:jsonValue="STOP_LOSS_LIMIT">3</choice>
            <choice name="TakeProfit" mbx:jsonValue="TAKE_PROFIT">4</choice>
            <choice name="TakeProfitLimit" mbx:jsonValue="TAKE_PROFIT_LIMIT">5</choice>
            <choice name="LimitMaker" mbx:jsonValue="LIMIT_MAKER">6</choice>
        </set>

        <enum name="selfTradePreventionMode" encodingType="uint8">
            <validValue name="None" mbx:jsonValue="NONE">1</validValue>
            <validValue name="ExpireTaker" mbx:jsonValue="EXPIRE_TAKER">2</validValue>
            <validValue name="ExpireMaker" mbx:jsonValue="EXPIRE_MAKER">3</validValue>
            <validValue name="ExpireBoth" mbx:jsonValue="EXPIRE_BOTH">4</validValue>
        </enum>

        <enum name="allocationType" encodingType="uint8">
            <validValue name="Unknown" mbx:jsonValue="UNKNOWN">0</validValue>
            <validValue name="Sor" mbx:jsonValue="SOR">2</validValue>
        </enum>

        <enum name="accountType" encodingType="uint8">
            <validValue name="Spot" mbx:jsonValue="SPOT">0</validValue>
            <validValue name="Unknown" mbx:jsonValue="UNKNOWN">2</validValue>
        </enum>

        <set name="allowedSelfTradePreventionModes" encodingType="uint8">
            <choice name="None" mbx:jsonValue="NONE">0</choice>
            <choice name="ExpireTaker" mbx:jsonValue="EXPIRE_TAKER">1</choice>
            <choice name="ExpireMaker" mbx:jsonValue="EXPIRE_MAKER">2</choice>
            <choice name="ExpireBoth" mbx:jsonValue="EXPIRE_BOTH">3</choice>
        </set>

        <enum name="orderStatus" encodingType="uint8">
            <validValue name="New" mbx:jsonValue="NEW">0</validValue>
            <validValue name="PartiallyFilled" mbx:jsonValue="PARTIALLY_FILLED">1</validValue>
            <validValue name="Filled" mbx:jsonValue="FILLED">2</validValue>
            <validValue name="Canceled" mbx:jsonValue="CANCELED">3</validValue>
            <validValue name="PendingCancel" mbx:jsonValue="PENDING_CANCEL">4</validValue>
            <validValue name="Rejected" mbx:jsonValue="REJECTED">5</validValue>
            <validValue name="Expired" mbx:jsonValue="EXPIRED">6</validValue>
            <validValue name="ExpiredInMatch" mbx:jsonValue="EXPIRED_IN_MATCH">9</validValue>
            <validValue name="PendingNew" mbx:jsonValue="PENDING_NEW">11</validValue>
            <validValue name="Unknown" mbx:jsonValue="UNKNOWN">254</validValue>
        </enum>

        <enum name="orderSide" encodingType="uint8">
            <validValue name="Buy" mbx:jsonValue="BUY">0</validValue>
            <validValue name="Sell" mbx:jsonValue="SELL">1</validValue>
        </enum>

        <enum name="orderCapacity" encodingType="uint8">
            <validValue name="Principal" mbx:jsonValue="PRINCIPAL">1</validValue>
            <validValue name="Agency" mbx:jsonValue="AGENCY">2</validValue>
        </enum>

        <enum name="timeInForce" encodingType="uint8">
            <validValue name="Gtc" mbx:jsonValue="GTC">0</validValue>
            <validValue name="Ioc" mbx:jsonValue="IOC">1</validValue>
            <validValue name="Fok" mbx:jsonValue="FOK">2</validValue>
        </enum>

        <enum name="floor" encodingType="uint8">
            <validValue name="Exchange" mbx:jsonValue="EXCHANGE">1</validValue>
            <validValue name="Broker" mbx:jsonValue="BROKER">2</validValue>
            <validValue name="Sor" mbx:jsonValue="SOR">3</validValue>
        </enum>

        <enum name="matchType" encodingType="uint8">
            <validValue name="AutoMatch" mbx:jsonValue="AUTO_MATCH">1</validValue>
            <validValue name="OnePartyTradeReport" mbx:jsonValue="ONE_PARTY_TRADE_REPORT">2</validValue>
        </enum>

        <enum name="contingencyType" encodingType="uint8">
            <validValue name="Oco" mbx:jsonValue="OCO">1</validValue>
            <validValue name="Oto" mbx:jsonValue="OTO">2</validValue>
        </enum>

        <enum name="listStatusType" encodingType="uint8">
            <validValue name="Response" mbx:jsonValue="RESPONSE">0</validValue>
            <validValue name="ExecStarted" mbx:jsonValue="EXEC_STARTED">1</validValue>
            <validValue name="AllDone" mbx:jsonValue="ALL_DONE">2</validValue>
        </enum>

        <enum name="listOrderStatus" encodingType="uint8">
            <validValue name="Canceling" mbx:jsonValue="CANCELING">0</validValue>
            <validValue name="Executing" mbx:jsonValue="EXECUTING">1</validValue>
            <validValue name="AllDone" mbx:jsonValue="ALL_DONE">2</validValue>
            <validValue name="Reject" mbx:jsonValue="REJECT">3</validValue>
        </enum>

        <enum name="cancelReplaceStatus" encodingType="uint8">
            <validValue name="Success" mbx:jsonValue="SUCCESS">0</validValue>
            <validValue name="Failure" mbx:jsonValue="FAILURE">1</validValue>
            <validValue name="NotAttempted" mbx:jsonValue="NOT_ATTEMPTED">2</validValue>
        </enum>
    </types>

    <sbe:message name="PriceFilter" id="1">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.PriceFilter"/>
        <field id="2" name="priceExponent" type="exponent8"/>
        <field id="3" name="minPrice" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="4" name="maxPrice" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="5" name="tickSize" type="mantissa64" mbx:exponent="priceExponent"/>
    </sbe:message>
    <sbe:message name="PercentPriceFilter" id="2">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.PercentPrice"/>
        <field id="2" name="multiplierExponent" type="exponent8"/>
        <field id="3" name="multiplierUp" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="4" name="multiplierDown" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="5" name="avgPriceMins" type="int32"/>
    </sbe:message>
    <sbe:message name="PercentPriceBySideFilter" id="3">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.PercentPriceBySide"/>
        <field id="2" name="multiplierExponent" type="exponent8"/>
        <field id="3" name="bidMultiplierUp" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="4" name="bidMultiplierDown" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="5" name="askMultiplierUp" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="6" name="askMultiplierDown" type="mantissa64" mbx:exponent="multiplierExponent"/>
        <field id="7" name="avgPriceMins" type="int32"/>
    </sbe:message>
    <sbe:message name="LotSizeFilter" id="4">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.LotSize"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="minQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="4" name="maxQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="5" name="stepSize" type="mantissa64" mbx:exponent="qtyExponent"/>
    </sbe:message>
    <sbe:message name="MinNotionalFilter" id="5">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MinNotional"/>
        <field id="2" name="priceExponent" type="exponent8"/>
        <field id="3" name="minNotional" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="4" name="applyToMarket" type="boolEnum"/>
        <field id="5" name="avgPriceMins" type="int32"/>
    </sbe:message>
    <sbe:message name="NotionalFilter" id="6">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.Notional"/>
        <field id="2" name="priceExponent" type="exponent8"/>
        <field id="3" name="minNotional" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="4" name="applyMinToMarket" type="boolEnum"/>
        <field id="5" name="maxNotional" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="6" name="applyMaxToMarket" type="boolEnum"/>
        <field id="7" name="avgPriceMins" type="int32"/>
    </sbe:message>
    <sbe:message name="IcebergPartsFilter" id="7">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.IcebergParts"/>
        <field id="2" name="filterLimit" type="int64" mbx:jsonPath="limit"/>
    </sbe:message>
    <sbe:message name="MarketLotSizeFilter" id="8">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MarketLotSize"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="minQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="4" name="maxQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="5" name="stepSize" type="mantissa64" mbx:exponent="qtyExponent"/>
    </sbe:message>
    <sbe:message name="MaxNumOrdersFilter" id="9">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MaxNumOrders"/>
        <field id="2" name="maxNumOrders" type="int64"/>
    </sbe:message>
    <sbe:message name="MaxNumAlgoOrdersFilter" id="10">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MaxNumAlgoOrders"/>
        <field id="2" name="maxNumAlgoOrders" type="int64"/>
    </sbe:message>
    <sbe:message name="MaxNumIcebergOrdersFilter" id="11">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MaxNumIcebergOrders"/>
        <field id="2" name="maxNumIcebergOrders" type="int64"/>
    </sbe:message>
    <sbe:message name="MaxPositionFilter" id="12">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.MaxPosition"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="maxPosition" type="mantissa64" mbx:exponent="qtyExponent"/>
    </sbe:message>
    <sbe:message name="TrailingDeltaFilter" id="13">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.TrailingDelta"/>
        <field id="2" name="minTrailingAboveDelta" type="int64"/>
        <field id="3" name="maxTrailingAboveDelta" type="int64"/>
        <field id="4" name="minTrailingBelowDelta" type="int64"/>
        <field id="5" name="maxTrailingBelowDelta" type="int64"/>
    </sbe:message>
    <sbe:message name="TPlusSellFilter" id="14">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.TPlusSell"/>
        <field id="2" name="endTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
    </sbe:message>

    <sbe:message name="ExchangeMaxNumOrdersFilter" id="15">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.ExchangeMaxNumOrders"/>
        <field id="2" name="maxNumOrders" type="int64"/>
    </sbe:message>
    <sbe:message name="ExchangeMaxNumAlgoOrdersFilter" id="16">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.ExchangeMaxNumAlgoOrders"/>
        <field id="2" name="maxNumAlgoOrders" type="int64"/>
    </sbe:message>
    <sbe:message name="ExchangeMaxNumIcebergOrdersFilter" id="17">
        <field id="1" name="filterType" type="filterType" presence="constant" valueRef="filterType.ExchangeMaxNumIcebergOrders"/>
        <field id="2" name="maxNumIcebergOrders" type="int64"/>
    </sbe:message>

    <!-- Endpoint responses begin here -->
    <sbe:message name="WebSocketResponse" id="50" description="Message wrapper for WebSocket API.">
        <field id="1" name="sbeSchemaIdVersionDeprecated" type="boolEnum"/>
        <field id="2" name="status" type="uint16"/>
        <group id="100" name="rateLimits" dimensionType="groupSize16Encoding">
            <field id="1" name="rateLimitType" type="rateLimitType"/>
            <field id="2" name="interval" type="rateLimitInterval"/>
            <field id="3" name="intervalNum" type="uint8"/>
            <field id="4" name="rateLimit" type="int64" mbx:jsonPath="limit"/>
            <field id="5" name="current" type="int64" mbx:jsonPath="count"/>
        </group>
        <!-- While the request parameter "id" may be an integer, string or
            null, the response field "id" is always a string. Integers are
            converted to strings and null is converted to the empty string. -->
        <data id="200" name="id" type="varString8"/>
        <!-- Contains one of the <sbe:message/> types that follow.
            Use the "templateId" field from the "messageHeader" to
            differentiate them. When using WebSocket API, even
            "ErrorResponse" is wrapped by "WebSocketResponse". -->
        <data id="201" name="result" type="messageData"/>
    </sbe:message>

    <!-- Response for WebSocket "method":"session.logon" -->
    <sbe:message name="WebSocketSessionLogonResponse" id="51">
        <field id="1" name="authorizedSince" type="utcTimestampUs"/>
        <field id="2" name="connectedSince" type="utcTimestampUs"/>
        <field id="3" name="returnRateLimits" type="boolEnum"/>
        <field id="4" name="serverTime" type="utcTimestampUs"/>
        <data id="200" name="apiKey" type="varString"/>
    </sbe:message>

    <!-- Response for WebSocket "method":"session.status" -->
    <sbe:message name="WebSocketSessionStatusResponse" id="52">
        <field id="1" name="authorizedSince" type="utcTimestampUs" presence="optional"/>
        <field id="2" name="connectedSince" type="utcTimestampUs"/>
        <field id="3" name="returnRateLimits" type="boolEnum"/>
        <field id="4" name="serverTime" type="utcTimestampUs"/>
        <data id="200" name="apiKey" type="optionalVarString"/>
    </sbe:message>

    <!-- Response for WebSocket "method":"session.logout" -->
    <sbe:message name="WebSocketSessionLogoutResponse" id="53">
        <field id="1" name="authorizedSince" type="utcTimestampUs" presence="optional"/>
        <field id="2" name="connectedSince" type="utcTimestampUs"/>
        <field id="3" name="returnRateLimits" type="boolEnum"/>
        <field id="4" name="serverTime" type="utcTimestampUs"/>
        <data id="200" name="apiKey" type="optionalVarString"/>
    </sbe:message>

    <sbe:message name="ErrorResponse" id="100">
        <field id="1" name="code" type="int16"/>
        <field id="2" name="serverTime" type="utcTimestampUs" presence="optional"/>
        <field id="3" name="retryAfter" type="utcTimestampUs" presence="optional"/>
        <data id="200" name="msg" type="varString"/>
        <!-- May contain a "CancelReplaceOrderResponse" message -->
        <data id="201" name="data" type="optionalMessageData"/>
    </sbe:message>

    <!-- General endpoints -->
    <!-- Response for
        - REST GET /api/v3/ping
        - WebSocket "method":"ping" -->
    <sbe:message name="PingResponse" id="101">
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/time
        - WebSocket "method":"time" -->
    <sbe:message name="ServerTimeResponse" id="102">
        <field id="1" name="serverTime" type="utcTimestampUs"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/exchangeInfo
        - WebSocket "method":"exchangeInfo" -->
    <sbe:message name="ExchangeInfoResponse" id="103">
        <!-- "timeZone" in JSON response is omitted. All timestamps in SBE
            responses are in UTC. -->
        <!-- "serverTime" in JSON response is omitted. See GET /api/v3/time -->
        <group id="100" name="rateLimits">
            <field id="1" name="rateLimitType" type="rateLimitType"/>
            <field id="2" name="interval" type="rateLimitInterval"/>
            <field id="3" name="intervalNum" type="uint8"/>
            <field id="4" name="rateLimit" type="int64" mbx:jsonPath="limit"/>
        </group>

        <group id="101" name="exchangeFilters">
            <!-- Contains one of
                - "ExchangeMaxNumOrdersFilter"
                - "ExchangeMaxNumAlgoOrdersFilter"
                - "ExchangeMaxNumIcebergOrdersFilter"
                Use the "templateId" field from the "messageHeader" to
                differentiate them. -->
            <data id="200" name="filter" type="messageData8" mbx:jsonPath=".."/>
        </group>

        <group id="102" name="symbols">
            <field id="1" name="status" type="symbolStatus"/>
            <field id="2" name="baseAssetPrecision" type="uint8"/>
            <field id="3" name="quoteAssetPrecision" type="uint8"/>
            <field id="4" name="baseCommissionPrecision" type="uint8"/>
            <field id="5" name="quoteCommissionPrecision" type="uint8"/>
            <field id="6" name="orderTypes" type="orderTypes"/>
            <field id="7" name="icebergAllowed" type="boolEnum"/>
            <field id="8" name="ocoAllowed" type="boolEnum"/>
            <field id="9" name="otoAllowed" type="boolEnum"/>
            <field id="10" name="quoteOrderQtyMarketAllowed" type="boolEnum"/>
            <field id="11" name="allowTrailingStop" type="boolEnum"/>
            <field id="12" name="cancelReplaceAllowed" type="boolEnum"/>
            <field id="13" name="isSpotTradingAllowed" type="boolEnum"/>
            <field id="14" name="isMarginTradingAllowed" type="boolEnum"/>
            <field id="15" name="defaultSelfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="16" name="allowedSelfTradePreventionModes" type="allowedSelfTradePreventionModes"/>

            <group id="100" name="filters">
                <!-- Contains one of
                    - "PriceFilter"
                    - "PercentPriceFilter"
                    - "PercentPriceBySideFilter"
                    - "LotSizeFilter"
                    - "MinNotionalFilter"
                    - "NotionalFilter"
                    - "IcebergPartsFilter"
                    - "MarketLotSizeFilter"
                    - "MaxNumOrdersFilter"
                    - "MaxNumAlgoOrdersFilter"
                    - "MaxNumIcebergOrdersFilter"
                    - "MaxPositionFilter"
                    - "TrailingDeltaFilter"
                    - "TPlusSellFilter"
                    Use the "templateId" field from the "messageHeader" to
                    differentiate them. -->
                <data id="200" name="filter" type="messageData8" mbx:jsonPath=".."/>
            </group>

            <group id="101" name="permissionSets">
                <group id="100" name="permissions" mbx:jsonPath="..">
                    <data id="200" name="permission" type="varString8" mbx:jsonPath=".."/>
                </group>
            </group>

            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="baseAsset" type="varString8"/>
            <data id="202" name="quoteAsset" type="varString8"/>
        </group>

        <group id="103" name="sors" mbx:jsonOmitNull="true">
            <group id="1" name="sorSymbols" mbx:jsonPath="symbols">
                <data id="200" name="symbol" type="varString8" mbx:jsonPath=".."/>
            </group>
            <data id="200" name="baseAsset" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Market data endpoint -->
    <!-- Response for
        - REST GET /api/v3/depth
        - WebSocket "method":"depth" -->
    <sbe:message name="DepthResponse" id="200">
        <field id="1" name="lastUpdateId" type="updateId"/>
        <field id="2" name="priceExponent" type="exponent8"/>
        <field id="3" name="qtyExponent" type="exponent8"/>
        <group id="100" name="bids">
            <field id="1" name="price" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="2" name="qty" type="mantissa64" mbx:exponent="qtyExponent" mbx:jsonPath="[]"/>
        </group>
        <group id="101" name="asks">
            <field id="1" name="price" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="2" name="qty" type="mantissa64" mbx:exponent="qtyExponent" mbx:jsonPath="[]"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/trades
        - REST GET /api/v3/historicalTrades
        - WebSocket "method":"trades.recent"
        - WebSocket "method":"trades.historical" -->
    <sbe:message name="TradesResponse" id="201">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <group id="100" name="trades" mbx:jsonPath="..">
            <field id="1" name="id" type="tradeId"/>
            <field id="2" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="3" name="qty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="4" name="quoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="5" name="time" type="utcTimestampUs"/>
            <field id="6" name="isBuyerMaker" type="boolEnum"/>
            <field id="7" name="isBestMatch" type="boolEnum"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/aggTrades
        - WebSocket "method":"trades.aggregate" -->
    <sbe:message name="AggTradesResponse" id="202">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <group id="100" name="aggTrades" mbx:jsonPath="..">
            <field id="1" name="aggTradeId" type="aggTradeId" mbx:jsonPath="a"/>
            <field id="2" name="price" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="p"/>
            <field id="3" name="qty" type="mantissa64" mbx:exponent="qtyExponent" mbx:jsonPath="q"/>
            <field id="4" name="firstTradeId" type="tradeId" mbx:jsonPath="f"/>
            <field id="5" name="lastTradeId" type="tradeId" mbx:jsonPath="l"/>
            <field id="7" name="time" type="utcTimestampUs" mbx:jsonPath="T"/>
            <field id="8" name="isBuyerMaker" type="boolEnum" mbx:jsonPath="m"/>
            <field id="9" name="isBestMatch" type="boolEnum" mbx:jsonPath="M"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/klines
        - REST GET /api/v3/uiKlines
        - WebSocket "method":"klines"
        - WebSocket "method":"uiKlines" -->
    <sbe:message name="KlinesResponse" id="203">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <group id="100" name="klines" mbx:jsonPath="..">
            <field id="1" name="openTime" type="utcTimestampUs" mbx:jsonPath="[]"/>
            <field id="2" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="3" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="4" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="5" name="closePrice" type="mantissa64" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="6" name="volume" type="mantissa128" mbx:exponent="qtyExponent" mbx:jsonPath="[]"/>
            <field id="7" name="closeTime" type="utcTimestampUs" mbx:jsonPath="[]"/>
            <field id="8" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
            <field id="9" name="numTrades" type="int64" mbx:jsonPath="[]"/>
            <field id="10" name="takerBuyBaseVolume" type="mantissa128" mbx:exponent="qtyExponent" mbx:jsonPath="[]"/>
            <field id="11" name="takerBuyQuoteVolume" type="mantissa128" mbx:exponent="priceExponent" mbx:jsonPath="[]"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/avgPrice
        - WebSocket "method":"avgPrice" -->
    <sbe:message name="AveragePriceResponse" id="204">
        <field id="1" name="mins" type="int64"/>
        <field id="2" name="priceExponent" type="exponent8"/>
        <field id="3" name="price" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="closeTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/24hr?symbol=SYMBOL&type=FULL
        - WebSocket "method":"ticker.24hr","params":{"symbol":"<SYMBOL>","type":"FULL"} -->
    <sbe:message name="Ticker24hSymbolFullResponse" id="205">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="priceChange" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="priceChangePercent" type="float" presence="optional" mbx:jsonDefaultValue="0.0"/>
        <field id="5" name="weightedAvgPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="6" name="prevClosePrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="7" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="8" name="lastQty" type="mantissa128" mbx:exponent="qtyExponent"/>
        <field id="9" name="bidPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="10" name="bidQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="11" name="askPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="12" name="askQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="13" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="14" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="15" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="16" name="volume" type="mantissa128" mbx:exponent="qtyExponent" />
        <field id="17" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
        <field id="18" name="openTime" type="utcTimestampUs"/>
        <field id="19" name="closeTime" type="utcTimestampUs"/>
        <field id="20" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="21" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="22" name="numTrades" type="int64" mbx:jsonPath="count"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/24hr?type=FULL
        - WebSocket "method":"ticker.24hr","params":{"type":"FULL"} -->
    <sbe:message name="Ticker24hFullResponse" id="206">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="priceChange" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="4" name="priceChangePercent" type="float" presence="optional" mbx:jsonDefaultValue="0.0"/>
            <field id="5" name="weightedAvgPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="6" name="prevClosePrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="7" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="8" name="lastQty" type="mantissa128" mbx:exponent="qtyExponent"/>
            <field id="9" name="bidPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="10" name="bidQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="11" name="askPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="12" name="askQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="13" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="14" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="15" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="16" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
            <field id="17" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
            <field id="18" name="openTime" type="utcTimestampUs"/>
            <field id="19" name="closeTime" type="utcTimestampUs"/>
            <field id="20" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="21" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="22" name="numTrades" type="int64" mbx:jsonPath="count"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/24hr?symbol=SYMBOL&type=MINI
        - WebSocket "method":"ticker.24hr","params":{"symbol":"<SYMBOL>","type":"MINI"} -->
    <sbe:message name="Ticker24hSymbolMiniResponse" id="207">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="5" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="6" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="7" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
        <field id="8" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
        <field id="9" name="openTime" type="utcTimestampUs"/>
        <field id="10" name="closeTime" type="utcTimestampUs"/>
        <field id="11" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="12" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="13" name="numTrades" type="int64" mbx:jsonPath="count"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/24hr?type=MINI
        - WebSocket "method":"ticker.24hr","params":{"type":"MINI"} -->
    <sbe:message name="Ticker24hMiniResponse" id="208">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="4" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="5" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="6" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="7" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
            <field id="8" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
            <field id="9" name="openTime" type="utcTimestampUs"/>
            <field id="10" name="closeTime" type="utcTimestampUs"/>
            <field id="11" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="12" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="13" name="numTrades" type="int64" mbx:jsonPath="count"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/price?symbol=
        - WebSocket "method":"ticker.price","params":{"symbol":"<SYMBOL>"} -->
    <sbe:message name="PriceTickerSymbolResponse" id="209">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="price" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/price?symbols=
        - Websocket "method":"ticker.price","params":{"symbols":[<SYMBOLS>]} -->
    <sbe:message name="PriceTickerResponse" id="210">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="price" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/bookTicker?symbol=
        - WebSocket "method":"ticker.book","params":{"symbol":"<SYMBOL>"} -->
    <sbe:message name="BookTickerSymbolResponse" id="211">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="bidPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="bidQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="5" name="askPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="6" name="askQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker/bookTicker?symbols=
        - WebSocket "method":"ticker.book","params":{"symbols":[<SYMBOLS>]} -->
    <sbe:message name="BookTickerResponse" id="212">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="bidPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="4" name="bidQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="5" name="askPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="6" name="askQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker?symbol=SYMBOL&type=FULL
        - REST GET /api/v3/tradingDay?symbol=SYMBOL&type=FULL
        - WebSocket "method":"ticker","params":{"symbol":"<SYMBOL>","type":"FULL"}
        - WebSocket "method":"ticker.tradingDay","params":{"symbol":"<SYMBOL>","type":"FULL"} -->
    <sbe:message name="TickerSymbolFullResponse" id="213">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="priceChange" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="priceChangePercent" type="float" presence="optional" mbx:jsonDefaultValue="0.0"/>
        <field id="5" name="weightedAvgPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="6" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="7" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="8" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="9" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="10" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
        <field id="11" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
        <field id="12" name="openTime" type="utcTimestampUs"/>
        <field id="13" name="closeTime" type="utcTimestampUs"/>
        <field id="14" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="15" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="16" name="numTrades" type="int64" mbx:jsonPath="count"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker?type=FULL&symbols=
        - REST GET /api/v3/tradingDay?type=FULL&symbols=
        - WebSocket "method":"ticker","params":{"type":"FULL","symbols":[<SYMBOLS>]}
        - WebSocket "method":"ticker.tradingDay","params":{"type":"FULL","symbols":[<SYMBOLS>]} -->
    <sbe:message name="TickerFullResponse" id="214">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="priceChange" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="4" name="priceChangePercent" type="float" presence="optional" mbx:jsonDefaultValue="0.0"/>
            <field id="5" name="weightedAvgPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="6" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="7" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="8" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="9" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="10" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
            <field id="11" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
            <field id="12" name="openTime" type="utcTimestampUs"/>
            <field id="13" name="closeTime" type="utcTimestampUs"/>
            <field id="14" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="15" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="16" name="numTrades" type="int64" mbx:jsonPath="count"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker?symbol=SYMBOL&type=MINI
        - REST GET /api/v3/tradingDay?symbol=SYMBOL&type=MINI
        - WebSocket "method":"ticker","params":{"symbol":"<SYMBOL>","type":"MINI"]}
        - WebSocket "method":"ticker.tradingDay","params":{"symbol":"<SYMBOL>","type":"MINI"} -->
    <sbe:message name="TickerSymbolMiniResponse" id="215">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="4" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="5" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="6" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
        <field id="7" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
        <field id="8" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
        <field id="9" name="openTime" type="utcTimestampUs"/>
        <field id="10" name="closeTime" type="utcTimestampUs"/>
        <field id="11" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="12" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="13" name="numTrades" type="int64" mbx:jsonPath="count"/>
        <data id="200" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/ticker?type=MINI&symbols=
        - REST GET /api/v3/tradingDay?type=MINI&symbols=
        - WebSocket "method":"ticker","params":{"type":"MINI","symbols":[<SYMBOLS>]}
        - WebSocket "method":"ticker.tradingDay","params":{"type":"MINI","symbols":[<SYMBOLS>]} -->
    <sbe:message name="TickerMiniResponse" id="216">
        <group id="100" name="tickers" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="openPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="4" name="highPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="5" name="lowPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="6" name="lastPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional" mbx:jsonDefaultValue="0"/>
            <field id="7" name="volume" type="mantissa128" mbx:exponent="qtyExponent"/>
            <field id="8" name="quoteVolume" type="mantissa128" mbx:exponent="priceExponent"/>
            <field id="9" name="openTime" type="utcTimestampUs"/>
            <field id="10" name="closeTime" type="utcTimestampUs"/>
            <field id="11" name="firstId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="12" name="lastId" type="tradeId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="13" name="numTrades" type="int64" mbx:jsonPath="count"/>
            <data id="200" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Trading endpoints -->
    <!-- Response for
        - REST POST /api/v3/order?newOrderRespType=ACK
        - REST POST /api/v3/sor/order?newOrderRespType=ACK
        - WebSocket "method":"order.place","params":{"newOrderRespType":"ACK"}
        - WebSocket "method":"sor.order.place","params":{"newOrderRespType":"ACK"} -->
    <sbe:message name="NewOrderAckResponse" id="300">
        <field id="1" name="orderId" type="orderId"/>
        <field id="2" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="3" name="transactTime" type="utcTimestampUs"/>
        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="clientOrderId" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/order?newOrderRespType=RESULT
        - REST POST /api/v3/sor/order?newOrderRespType=RESULT
        - WebSocket "method":"order.place","params":{"newOrderRespType":"RESULT"}
        - WebSocket "method":"sor.order.place","params":{"newOrderRespType":"RESULT"} -->
    <sbe:message name="NewOrderResultResponse" id="301">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="orderId" type="orderId"/>
        <field id="4" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="5" name="transactTime" type="utcTimestampUs"/>
        <field id="6" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="7" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="8" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="9" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="10" name="status" type="orderStatus"/>
        <field id="11" name="timeInForce" type="timeInForce"/>
        <field id="12" name="orderType" type="orderType" mbx:jsonPath="type"/>
        <field id="13" name="side" type="orderSide"/>
        <field id="14" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
        <field id="15" name="trailingDelta" type="int64" presence="optional"/>
        <field id="16" name="trailingTime" type="utcTimestampUs" presence="optional"/>
        <field id="17" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="18" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="19" name="strategyId" type="int64" presence="optional"/>
        <field id="20" name="strategyType" type="int32" presence="optional"/>
        <field id="21" name="orderCapacity" type="orderCapacity" presence="optional"/>
        <field id="22" name="workingFloor" type="floor" presence="optional"/>
        <field id="23" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
        <field id="24" name="tradeGroupId" type="int64" presence="optional"/>
        <field id="25" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="26" name="usedSor" type="boolEnum" presence="optional"/>
        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="clientOrderId" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/order?newOrderRespType=FULL
        - REST POST /api/v3/sor/order?newOrderRespType=FULL
        - WebSocket "method":"order.place","params":{"newOrderRespType":"FULL"}
        - WebSocket "method":"sor.order.place","params":{"newOrderRespType":"FULL"} -->
    <sbe:message name="NewOrderFullResponse" id="302">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="orderId" type="orderId"/>
        <field id="4" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="5" name="transactTime" type="utcTimestampUs"/>
        <field id="6" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="7" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="8" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="9" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="10" name="status" type="orderStatus"/>
        <field id="11" name="timeInForce" type="timeInForce"/>
        <field id="12" name="orderType" type="orderType" mbx:jsonPath="type"/>
        <field id="13" name="side" type="orderSide"/>
        <field id="14" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
        <field id="15" name="trailingDelta" type="int64" presence="optional"/>
        <field id="16" name="trailingTime" type="utcTimestampUs" presence="optional"/>
        <field id="17" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="18" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="19" name="strategyId" type="int64" presence="optional"/>
        <field id="20" name="strategyType" type="int32" presence="optional"/>
        <field id="21" name="orderCapacity" type="orderCapacity" presence="optional"/>
        <field id="22" name="workingFloor" type="floor" presence="optional"/>
        <field id="23" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
        <field id="24" name="tradeGroupId" type="int64" presence="optional"/>
        <field id="25" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="26" name="usedSor" type="boolEnum" presence="optional"/>

        <group id="100" name="fills">
            <field id="1" name="commissionExponent" type="exponent8"/>
            <field id="2" name="matchType" type="matchType" presence="optional"/>
            <field id="3" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="4" name="qty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="5" name="commission" type="mantissa64" mbx:exponent="commissionExponent"/>
            <field id="6" name="tradeId" type="tradeId" presence="optional"/>
            <field id="7" name="allocId" type="int64" presence="optional"/>
            <data id="200" name="commissionAsset" type="optionalVarString8"/>
        </group>

        <group id="101" name="preventedMatches">
            <field id="1" name="preventedMatchId" type="int64"/>
            <field id="2" name="makerOrderId" type="orderId" presence="optional"/>
            <field id="3" name="price" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="4" name="takerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="5" name="makerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <data id="200" name="makerSymbol" type="optionalVarString8"/>
        </group>

        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="clientOrderId" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/order/test
        - REST POST /api/v3/sor/order/test
        - WebSocket "method":"order.test"
        - WebSocket "method":"sor.order.test" -->
    <sbe:message name="OrderTestResponse" id="303">
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/order
        - WebSocket "method":"order.status" -->
    <sbe:message name="OrderResponse" id="304">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="orderId" type="orderId"/>
        <field id="4" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="5" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="6" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="7" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="8" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="9" name="status" type="orderStatus"/>
        <field id="10" name="timeInForce" type="timeInForce"/>
        <field id="11" name="orderType" type="orderType" mbx:jsonPath="type"/>
        <field id="12" name="side" type="orderSide"/>
        <field id="13" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
        <field id="14" name="trailingDelta" type="int64" presence="optional"/>
        <field id="15" name="trailingTime" type="utcTimestampUs" presence="optional"/>
        <field id="16" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="17" name="time" type="utcTimestampUs"/>
        <field id="18" name="updateTime" type="utcTimestampUs"/>
        <field id="19" name="isWorking" type="boolEnum"/>
        <field id="20" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="21" name="origQuoteOrderQty" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="22" name="strategyId" type="int64" presence="optional"/>
        <field id="23" name="strategyType" type="int32" presence="optional"/>
        <field id="24" name="orderCapacity" type="orderCapacity" presence="optional"/>
        <field id="25" name="workingFloor" type="floor" presence="optional"/>
        <field id="26" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
        <field id="27" name="preventedMatchId" type="int64" presence="optional"/>
        <field id="28" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="29" name="usedSor" type="boolEnum" presence="optional"/>
        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="clientOrderId" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST DELETE /api/v3/order
        - WebSocket "method":"order.cancel" -->
    <sbe:message name="CancelOrderResponse" id="305">
        <field id="1" name="priceExponent" type="exponent8"/>
        <field id="2" name="qtyExponent" type="exponent8"/>
        <field id="3" name="orderId" type="orderId"/>
        <field id="4" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
        <field id="5" name="transactTime" type="utcTimestampUs"/>
        <field id="6" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="7" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="8" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
        <field id="9" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
        <field id="10" name="status" type="orderStatus"/>
        <field id="11" name="timeInForce" type="timeInForce"/>
        <field id="12" name="orderType" type="orderType" mbx:jsonPath="type"/>
        <field id="13" name="side" type="orderSide"/>
        <field id="14" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
        <field id="15" name="trailingDelta" type="int64" presence="optional"/>
        <field id="16" name="trailingTime" type="utcTimestampUs" presence="optional"/>
        <field id="17" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="18" name="strategyId" type="int64" presence="optional"/>
        <field id="19" name="strategyType" type="int32" presence="optional"/>
        <field id="20" name="orderCapacity" type="orderCapacity" presence="optional"/>
        <field id="21" name="workingFloor" type="floor" presence="optional"/>
        <field id="22" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
        <field id="23" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
        <field id="24" name="usedSor" type="boolEnum" presence="optional"/>
        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="origClientOrderId" type="varString8"/>
        <data id="202" name="clientOrderId" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST DELETE /api/v3/openOrders
        - WebSocket "method":"openOrders.cancelAll" -->
    <sbe:message name="CancelOpenOrdersResponse" id="306">
        <group id="100" name="responses" mbx:jsonPath="..">
            <!-- Contains one of
                - "CancelOrderResponse"
                - "CancelOrderListResponse"
                Use the "templateId" field from the "messageHeader" to
                differentiate them. -->
            <data id="200" name="response" type="messageData16"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/order/cancelReplace
        - WebSocket "method":"order.cancelReplace" -->
    <sbe:message name="CancelReplaceOrderResponse" id="307">
        <field id="1" name="cancelResult" type="cancelReplaceStatus"/>
        <field id="2" name="newOrderResult" type="cancelReplaceStatus"/>
        <!-- If non-null (length > 0), contains
            - "ErrorResponse" if "cancelResult" is "FAILURE"
            - "CancelOrderResponse" if "cancelResult" is "SUCCESS"
        -->
        <data id="200" name="cancelResponse" type="optionalMessageData16"/>
        <!-- If non-null (length > 0), contains
            - "ErrorResponse" if "newOrderResult" is "FAILURE"
            - "NewOrder[Ack|Result|Full]Response" if "newOrderResult" is
              "SUCCESS". The value of the "newOrderRespType" HTTP request
              parameter determines [Ack|Result|Full].
        -->
        <data id="201" name="newOrderResponse" type="optionalMessageData"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/openOrders
        - REST GET /api/v3/allOrders
        - WebSocket "method":"openOrders.status"
        - WebSocket "method":"allOrders" -->
    <sbe:message name="OrdersResponse" id="308">
        <group id="100" name="orders" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="orderId" type="orderId"/>
            <field id="4" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="5" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="6" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="7" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="8" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="9" name="status" type="orderStatus"/>
            <field id="10" name="timeInForce" type="timeInForce"/>
            <field id="11" name="orderType" type="orderType" mbx:jsonPath="type"/>
            <field id="12" name="side" type="orderSide"/>
            <field id="13" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="14" name="trailingDelta" type="int64" presence="optional"/>
            <field id="15" name="trailingTime" type="utcTimestampUs" presence="optional"/>
            <field id="16" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="17" name="time" type="utcTimestampUs"/>
            <field id="18" name="updateTime" type="utcTimestampUs"/>
            <field id="19" name="isWorking" type="boolEnum"/>
            <field id="20" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="21" name="origQuoteOrderQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="22" name="strategyId" type="int64" presence="optional"/>
            <field id="23" name="strategyType" type="int32" presence="optional"/>
            <field id="24" name="orderCapacity" type="orderCapacity" presence="optional"/>
            <field id="25" name="workingFloor" type="floor" presence="optional"/>
            <field id="26" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="27" name="preventedMatchId" type="int64" presence="optional"/>
            <field id="28" name="preventedQuantity" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="29" name="usedSor" type="boolEnum" presence="optional"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/orderList/oco?newOrderRespType=ACK
        - REST POST /api/v3/orderList/oto?newOrderRespType=ACK
        - REST POST /api/v3/orderList/otoco?newOrderRespType=ACK
        - WebSocket "method":"orderList.place.oco","params":{"newOrderRespType":"ACK"}
        - WebSocket "method":"orderList.place.oto","params":{"newOrderRespType":"ACK"}
        - WebSocket "method":"orderList.place.otoco","params":{"newOrderRespType":"ACK"} -->
    <sbe:message name="NewOrderListAckResponse" id="309">
        <field id="1" name="orderListId" type="orderListId"/>
        <field id="2" name="contingencyType" type="contingencyType"/>
        <field id="3" name="listStatusType" type="listStatusType"/>
        <field id="4" name="listOrderStatus" type="listOrderStatus"/>
        <field id="5" name="transactionTime" type="utcTimestampUs"/>

        <group id="100" name="orders" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <group id="101" name="orderReports" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <field id="2" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="3" name="transactTime" type="utcTimestampUs"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <data id="200" name="listClientOrderId" type="varString8"/>
        <data id="201" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/orderList/oco?newOrderRespType=RESULT
        - REST POST /api/v3/orderList/oto?newOrderRespType=RESULT
        - REST POST /api/v3/orderList/otoco?newOrderRespType=RESULT
        - WebSocket "method":"orderList.place.oco","params":{"newOrderRespType":"RESULT"}
        - WebSocket "method":"orderList.place.oto","params":{"newOrderRespType":"RESULT"}
        - WebSocket "method":"orderList.place.otoco","params":{"newOrderRespType":"RESULT"} -->
    <sbe:message name="NewOrderListResultResponse" id="310">
        <field id="1" name="orderListId" type="orderListId"/>
        <field id="2" name="contingencyType" type="contingencyType"/>
        <field id="3" name="listStatusType" type="listStatusType"/>
        <field id="4" name="listOrderStatus" type="listOrderStatus"/>
        <field id="5" name="transactionTime" type="utcTimestampUs"/>
        <field id="6" name="priceExponent" type="exponent8"/>
        <field id="7" name="qtyExponent" type="exponent8"/>

        <group id="100" name="orders" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <group id="101" name="orderReports" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <field id="2" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="3" name="transactTime" type="utcTimestampUs"/>
            <field id="4" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="5" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="6" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="7" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="8" name="status" type="orderStatus"/>
            <field id="9" name="timeInForce" type="timeInForce"/>
            <field id="10" name="orderType" type="orderType" mbx:jsonPath="type"/>
            <field id="11" name="side" type="orderSide"/>
            <field id="12" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="13" name="trailingDelta" type="int64" presence="optional"/>
            <field id="14" name="trailingTime" type="utcTimestampUs" presence="optional"/>
            <field id="15" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="16" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="17" name="strategyId" type="int64" presence="optional"/>
            <field id="18" name="strategyType" type="int32" presence="optional"/>
            <field id="19" name="orderCapacity" type="orderCapacity" presence="optional"/>
            <field id="20" name="workingFloor" type="floor" presence="optional"/>
            <field id="21" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="22" name="tradeGroupId" type="int64" presence="optional"/>
            <field id="23" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="24" name="usedSor" type="boolEnum" presence="optional"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <data id="200" name="listClientOrderId" type="varString8"/>
        <data id="201" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/orderList/oco?newOrderRespType=FULL
        - REST POST /api/v3/orderList/oto?newOrderRespType=FULL
        - REST POST /api/v3/orderList/otoco?newOrderRespType=FULL
        - WebSocket "method":"orderList.place.oco","params":{"newOrderRespType":"FULL"}
        - WebSocket "method":"orderList.place.oto","params":{"newOrderRespType":"FULL"}
        - WebSocket "method":"orderList.place.otoco","params":{"newOrderRespType":"FULL"} -->
    <sbe:message name="NewOrderListFullResponse" id="311">
        <field id="1" name="orderListId" type="orderListId"/>
        <field id="2" name="contingencyType" type="contingencyType"/>
        <field id="3" name="listStatusType" type="listStatusType"/>
        <field id="4" name="listOrderStatus" type="listOrderStatus"/>
        <field id="5" name="transactionTime" type="utcTimestampUs"/>
        <field id="6" name="priceExponent" type="exponent8"/>
        <field id="7" name="qtyExponent" type="exponent8"/>

        <group id="100" name="orders" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <group id="101" name="orderReports" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <field id="2" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="3" name="transactTime" type="utcTimestampUs"/>
            <field id="4" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="5" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="6" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="7" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="8" name="status" type="orderStatus"/>
            <field id="9" name="timeInForce" type="timeInForce"/>
            <field id="10" name="orderType" type="orderType" mbx:jsonPath="type"/>
            <field id="11" name="side" type="orderSide"/>
            <field id="12" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="13" name="trailingDelta" type="int64" presence="optional"/>
            <field id="14" name="trailingTime" type="utcTimestampUs" presence="optional"/>
            <field id="15" name="workingTime" type="utcTimestampUs" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="16" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="17" name="strategyId" type="int64" presence="optional"/>
            <field id="18" name="strategyType" type="int32" presence="optional"/>
            <field id="19" name="orderCapacity" type="orderCapacity" presence="optional"/>
            <field id="20" name="workingFloor" type="floor" presence="optional"/>
            <field id="21" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="22" name="tradeGroupId" type="int64" presence="optional"/>
            <field id="23" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="24" name="usedSor" type="boolEnum" presence="optional"/>

            <group id="100" name="fills">
                <field id="1" name="commissionExponent" type="exponent8"/>
                <field id="2" name="matchType" type="matchType" presence="optional"/>
                <field id="3" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
                <field id="4" name="qty" type="mantissa64" mbx:exponent="qtyExponent"/>
                <field id="5" name="commission" type="mantissa64" mbx:exponent="commissionExponent"/>
                <field id="6" name="tradeId" type="tradeId" presence="optional"/>
                <field id="7" name="allocId" type="int64" presence="optional"/>
                <data id="200" name="commissionAsset" type="optionalVarString8"/>
            </group>

            <group id="101" name="preventedMatches">
                <field id="1" name="preventedMatchId" type="int64"/>
                <field id="2" name="makerOrderId" type="orderId" presence="optional"/>
                <field id="3" name="price" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
                <field id="4" name="takerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
                <field id="5" name="makerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
                <data id="200" name="makerSymbol" type="optionalVarString8"/>
            </group>

            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <data id="200" name="listClientOrderId" type="varString8"/>
        <data id="201" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST DELETE /api/v3/order
        - REST DELETE /api/v3/orderList
        - WebSocket "method":"order.cancel"
        - WebSocket "method":"orderList.cancel" -->
    <sbe:message name="CancelOrderListResponse" id="312">
        <field id="1" name="orderListId" type="orderListId"/>
        <field id="2" name="contingencyType" type="contingencyType"/>
        <field id="3" name="listStatusType" type="listStatusType"/>
        <field id="4" name="listOrderStatus" type="listOrderStatus"/>
        <field id="5" name="transactionTime" type="utcTimestampUs"/>
        <field id="6" name="priceExponent" type="exponent8"/>
        <field id="7" name="qtyExponent" type="exponent8"/>

        <group id="100" name="orders" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <group id="101" name="orderReports" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <field id="2" name="orderListId" type="orderId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="3" name="transactTime" type="utcTimestampUs"/>
            <field id="4" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="5" name="origQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="6" name="executedQty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="7" name="cummulativeQuoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="8" name="status" type="orderStatus"/>
            <field id="9" name="timeInForce" type="timeInForce"/>
            <field id="10" name="orderType" type="orderType" mbx:jsonPath="type"/>
            <field id="11" name="side" type="orderSide"/>
            <field id="12" name="stopPrice" type="mantissa64" mbx:exponent="priceExponent" presence="optional"/>
            <field id="13" name="trailingDelta" type="int64" presence="optional"/>
            <field id="14" name="trailingTime" type="utcTimestampUs" presence="optional"/>
            <field id="15" name="icebergQty" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="16" name="strategyId" type="int64" presence="optional"/>
            <field id="17" name="strategyType" type="int32" presence="optional"/>
            <field id="18" name="orderCapacity" type="orderCapacity" presence="optional"/>
            <field id="19" name="workingFloor" type="floor" presence="optional"/>
            <field id="20" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="21" name="preventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="22" name="usedSor" type="boolEnum" presence="optional"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="origClientOrderId" type="varString8"/>
            <data id="202" name="clientOrderId" type="varString8"/>
        </group>

        <data id="200" name="listClientOrderId" type="varString8"/>
        <data id="201" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/orderList
        - WebSocket "method":"orderList.status" -->
    <sbe:message name="OrderListResponse" id="313">
        <field id="1" name="orderListId" type="orderListId"/>
        <field id="2" name="contingencyType" type="contingencyType"/>
        <field id="3" name="listStatusType" type="listStatusType"/>
        <field id="4" name="listOrderStatus" type="listOrderStatus"/>
        <field id="5" name="transactionTime" type="utcTimestampUs"/>

        <group id="100" name="orders" dimensionType="groupSize16Encoding">
            <field id="1" name="orderId" type="orderId"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="clientOrderId" type="varString8"/>
        </group>

        <data id="200" name="listClientOrderId" type="varString8"/>
        <data id="201" name="symbol" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/allOrderList
        - WebSocket "method":"openOrderLists.status" -->
    <sbe:message name="OrderListsResponse" id="314">
        <group id="100" name="orderLists" mbx:jsonPath="..">
            <field id="1" name="orderListId" type="orderListId"/>
            <field id="2" name="contingencyType" type="contingencyType"/>
            <field id="3" name="listStatusType" type="listStatusType"/>
            <field id="4" name="listOrderStatus" type="listOrderStatus"/>
            <field id="5" name="transactionTime" type="utcTimestampUs"/>

            <group id="100" name="orders">
                <field id="1" name="orderId" type="orderId"/>
                <data id="200" name="symbol" type="varString8"/>
                <data id="201" name="clientOrderId" type="varString8"/>
            </group>

            <data id="200" name="listClientOrderId" type="varString8"/>
            <data id="201" name="symbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST POST /api/v3/order/test?computeCommissionRates=true
        - REST POST /api/v3/sor/order/test?computeCommissionRates=true
        - WebSocket "method":"order.test","params":{"computeCommissionRates",true}
        - WebSocket "method":"sor.order.test","params":{"computeCommissionRates",true} -->
    <sbe:message name="OrderTestWithCommissionsResponse" id="315">
        <field id="1" name="commissionExponent" type="exponent8"/>
        <field id="2" name="discountExponent" type="exponent8"/>
        <field id="3" name="standardCommissionForOrderMaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommissionForOrder.maker"/>
        <field id="4" name="standardCommissionForOrderTaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommissionForOrder.taker"/>
        <field id="5" name="taxCommissionForOrderMaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommissionForOrder.maker"/>
        <field id="6" name="taxCommissionForOrderTaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommissionForOrder.taker"/>
        <field id="7" name="discountEnabledForAccount" type="boolEnum" mbx:jsonPath="discount.enabledForAccount"/>
        <field id="8" name="discountEnabledForSymbol" type="boolEnum" mbx:jsonPath="discount.enabledForSymbol"/>
        <field id="9" name="discount" type="mantissa64" mbx:exponent="discountExponent" mbx:jsonPath="discount.discount"/>
        <data id="200" name="discountAsset" type="optionalVarString8" mbx:jsonPath="discount.discountAsset"/>
    </sbe:message>

    <!-- Account endpoints -->
    <!-- Response for
        - REST GET /api/v3/account
        - WebSocket "method":"account.status" -->
    <sbe:message name="AccountResponse" id="400">
        <!-- The following fields in the JSON response do NOT appear in this
            SBE response.
            - "makerCommission"
            - "takerCommission"
            - "buyerCommission"
            - "sellerCommission"
            Commission rates may be found in fields 1 to 4 of this message as
            decimal floating-point numbers.
        -->
        <field id="1" name="commissionExponent" type="exponent8"/>
        <field id="2" name="commissionRateMaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="commissionRates.maker"/>
        <field id="3" name="commissionRateTaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="commissionRates.taker"/>
        <field id="4" name="commissionRateBuyer" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="commissionRates.buyer"/>
        <field id="5" name="commissionRateSeller" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="commissionRates.seller"/>
        <field id="6" name="canTrade" type="boolEnum"/>
        <field id="7" name="canWithdraw" type="boolEnum"/>
        <field id="8" name="canDeposit" type="boolEnum"/>
        <field id="9" name="brokered" type="boolEnum"/>
        <field id="10" name="requireSelfTradePrevention" type="boolEnum"/>
        <field id="11" name="preventSor" type="boolEnum"/>
        <field id="12" name="updateTime" type="utcTimestampUs"/>
        <field id="13" name="accountType" type="accountType"/>
        <field id="14" name="tradeGroupId" type="tradeGroupId" presence="optional"/>
        <field id="15" name="uid" type="int64"/>

        <group id="100" name="balances">
            <field id="1" name="exponent" type="exponent8"/>
            <field id="2" name="free" type="mantissa64" mbx:exponent="exponent"/>
            <field id="3" name="locked" type="mantissa64" mbx:exponent="exponent"/>
            <data id="200" name="asset" type="varString8"/>
        </group>

        <group id="101" name="permissions">
            <data id="200" name="permission" type="varString8" mbx:jsonPath=".."/>
        </group>

        <group id="102" name="reduceOnlyAssets">
            <data id="200" name="asset" type="varString8" mbx:jsonPath=".."/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/myTrades
        - WebSocket "method":"myTrades" -->
    <sbe:message name="AccountTradesResponse" id="401">
        <group id="100" name="trades" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="commissionExponent" type="exponent8"/>
            <field id="4" name="id" type="tradeId"/>
            <field id="5" name="orderId" type="orderId"/>
            <field id="6" name="orderListId" type="orderListId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="7" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="8" name="qty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="9" name="quoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="10" name="commission" type="mantissa64" mbx:exponent="commissionExponent"/>
            <field id="11" name="time" type="utcTimestampUs"/>
            <field id="12" name="isBuyer" type="boolEnum"/>
            <field id="13" name="isMaker" type="boolEnum"/>
            <field id="14" name="isBestMatch" type="boolEnum"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="commissionAsset" type="optionalVarString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/rateLimit/order
        - WebSocket "method":"account.rateLimits.orders" -->
    <sbe:message name="AccountOrderRateLimitResponse" id="402">
        <group id="100" name="rateLimits" mbx:jsonPath="..">
            <field id="1" name="rateLimitType" type="rateLimitType"/>
            <field id="2" name="interval" type="rateLimitInterval"/>
            <field id="3" name="intervalNum" type="uint8"/>
            <field id="4" name="rateLimit" type="int64" mbx:jsonPath="limit"/>
            <field id="5" name="numOrders" type="int64" mbx:jsonPath="count"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/myPreventedMatches
        - WebSocket "method":"myPreventedMatches" -->
    <sbe:message name="AccountPreventedMatchesResponse" id="403">
        <group id="100" name="preventedMatches" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="preventedMatchId" type="preventedMatchId"/>
            <field id="4" name="takerOrderId" type="orderId"/>
            <field id="5" name="makerOrderId" type="orderId"/>
            <field id="6" name="tradeGroupId" type="tradeGroupId"/>
            <field id="7" name="selfTradePreventionMode" type="selfTradePreventionMode"/>
            <field id="8" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="9" name="takerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="10" name="makerPreventedQuantity" type="mantissa64" mbx:exponent="qtyExponent" presence="optional"/>
            <field id="11" name="transactTime" type="utcTimestampUs"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="makerSymbol" type="varString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET /api/v3/myAllocations
        - WebSocket "method":"myAllocations" -->
    <sbe:message name="AccountAllocationsResponse" id="404">
        <group id="100" name="allocations" mbx:jsonPath="..">
            <field id="1" name="priceExponent" type="exponent8"/>
            <field id="2" name="qtyExponent" type="exponent8"/>
            <field id="3" name="commissionExponent" type="exponent8" presence="optional"/>
            <field id="4" name="allocationId" type="allocId"/>
            <field id="5" name="allocationType" type="allocationType"/>
            <!-- "sourceOrderId" when "isAllocator" is "TRUE" -->
            <field id="6" name="orderId" type="orderId"/>
            <!-- "sourceOrderListId" when "isAllocator" is "TRUE" -->
            <field id="7" name="orderListId" type="orderListId" presence="optional" mbx:jsonDefaultValue="-1"/>
            <field id="8" name="sourceTradeId" type="tradeId" presence="optional"/>
            <field id="9" name="sourceAllocationId" type="allocId" presence="optional"/>
            <field id="10" name="price" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="11" name="qty" type="mantissa64" mbx:exponent="qtyExponent"/>
            <field id="12" name="quoteQty" type="mantissa64" mbx:exponent="priceExponent"/>
            <field id="13" name="commission" type="mantissa64" mbx:exponent="commissionExponent" presence="optional"/>
            <field id="14" name="time" type="utcTimestampUs"/>
            <field id="15" name="isBuyer" type="boolEnum"/>
            <field id="16" name="isMaker" type="boolEnum"/>
            <!-- When "isAllocator" is "TRUE" the following fields
                may be set:
                - "sourceTradeId"
                - "sourceAllocationId"
                will be set:
                - "sourceSymbol"
            -->
            <field id="17" name="isAllocator" type="boolEnum"/>
            <data id="200" name="symbol" type="varString8"/>
            <data id="201" name="commissionAsset" type="optionalVarString8"/>
            <data id="202" name="sourceSymbol" type="optionalVarString8"/>
        </group>
    </sbe:message>

    <!-- Response for
        - REST GET GET /api/v3/account/commission
        - WebSocket "method":"account.commission" -->
    <sbe:message name="AccountCommissionResponse" id="405">
        <field id="1" name="commissionExponent" type="exponent8"/>
        <field id="2" name="discountExponent" type="exponent8"/>
        <field id="3" name="standardCommissionMaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommission.maker"/>
        <field id="4" name="standardCommissionTaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommission.taker"/>
        <field id="5" name="standardCommissionBuyer" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommission.buyer"/>
        <field id="6" name="standardCommissionSeller" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="standardCommission.seller"/>
        <field id="7" name="taxCommissionMaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommission.maker"/>
        <field id="8" name="taxCommissionTaker" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommission.taker"/>
        <field id="9" name="taxCommissionBuyer" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommission.buyer"/>
        <field id="10" name="taxCommissionSeller" type="mantissa64" mbx:exponent="commissionExponent" mbx:jsonPath="taxCommission.seller"/>
        <field id="11" name="discountEnabledForAccount" type="boolEnum" mbx:jsonPath="discount.enabledForAccount"/>
        <field id="12" name="discountEnabledForSymbol" type="boolEnum" mbx:jsonPath="discount.enabledForSymbol"/>
        <field id="13" name="discount" type="mantissa64" mbx:exponent="discountExponent" mbx:jsonPath="discount.discount"/>
        <data id="200" name="symbol" type="varString8"/>
        <data id="201" name="discountAsset" type="optionalVarString8" mbx:jsonPath="discount.discountAsset"/>
    </sbe:message>

    <!-- User data stream endpoints -->
    <!-- Response for
        - REST POST /api/v3/userDataStream
        - WebSocket "method":"userDataStream.start" -->
    <sbe:message name="UserDataStreamStartResponse" id="500">
        <data id="200" name="listenKey" type="varString8"/>
    </sbe:message>

    <!-- Response for
        - REST PUT /api/v3/userDataStream
        - WebSocket "method":"userDataStream.ping" -->
    <sbe:message name="UserDataStreamPingResponse" id="501">
    </sbe:message>

    <!-- Response for
        - REST DELETE /api/v3/userDataStream
        - WebSocket "method":"userDataStream.stop" -->
    <sbe:message name="UserDataStreamStopResponse" id="502">
    </sbe:message>
</sbe:messageSchema>
