# Binance-api-doc

* mkdocs is required 
* view https://binanceapitest.github.io/Binance-api-doc/

### Ana içeriğe geç Binance Logo Web Soket Akışları

Bu sayfada
Binance için Web Socket Akışları (2024-06-11)
Genel WSS bilgileri
Temel uç nokta şudur: wss://stream.binance.com:9443 veya wss://stream.binance.com:443
Akışlara tek bir ham akışta veya birleşik akışta erişilebilir
Ham akışlara /ws/<streamName> adresinden erişilir
Birleştirilmiş akışlara /stream?streams=<streamName1>/<streamName2>/<streamName3> adresinden erişilir
Birleştirilmiş akış olayları aşağıdaki gibi sarılır: {"stream":"<streamName>","data":<rawPayload>}
Akışlar için tüm semboller küçük harflidir
Stream.binance.com'a tek bir bağlantı yalnızca 24 saat geçerlidir; 24 saatlik sürenin sonunda bağlantınızın kesilmesini bekleyin
ping frameWebsocket sunucusu her 3 dakikada bir gönderecektir .
pong frameEğer websocket sunucusu 10 dakika içerisinde bağlantıdan geri dönüş alamazsa bağlantı kesilecektir.
Ping aldığınızda, mümkün olan en kısa sürede ping'in yükünün bir kopyasını içeren bir pong göndermelisiniz.
İstenmeyenlere pong framesizin verilir, ancak bağlantının kesilmesini engellemez. Bu pong çerçeveleri için yükün boş olması önerilir.
Temel uç nokta wss://data-stream.binance.vision yalnızca piyasa verisi mesajlarını almak için abone olunabilir .
Kullanıcı veri akışı bu URL'den kullanılamaz .
Websocket
WebSocket bağlantıları saniyede 5 gelen mesaj sınırına sahiptir. Bir mesaj şu şekilde değerlendirilir:
Bir PING çerçevesi
Bir PONG çerçevesi
JSON kontrollü bir mesaj (örneğin abone ol, aboneliği iptal et)
Sınırı aşan bağlantı kesilir; tekrar tekrar kesilen IP'ler yasaklanabilir.
Tek bir bağlantıyla en fazla 1024 yayın dinlenebilir.
Her IP için her 5 dakikada bir deneme başına 300 bağlantı sınırı vardır .
Canlı
Akışlara abone olmak/abonelikten çıkmak için aşağıdaki veriler websocket örneği üzerinden gönderilebilir. Örnekler aşağıda görülebilir.
idİleri geri giden mesajları benzersiz bir şekilde tanımlamak için bir tanımlayıcı olarak kullanılır. Aşağıdaki biçimler kabul edilir :
64 bitlik işaretli tamsayı
alfanümerik dizeler; maksimum uzunluk 36
null
Cevapta resultalınan nullbu ise, sorgu dışı istekler (örneğin Abone Olma/Abonelikten Çıkma) için gönderilen isteğin başarılı olduğu anlamına gelir.
Bir
Rica etmek

{
  "method": "SUBSCRIBE",
  "params": [
    "btcusdt@aggTrade",
    "btcusdt@depth"
  ],
  "id": 1
}

Cevap

{
  "result": null,
  "id": 1
}

Bir
Rica etmek

{
  "method": "UNSUBSCRIBE",
  "params": [
    "btcusdt@depth"
  ],
  "id": 312
}

Cevap

{
  "result": null,
  "id": 312
}

Listeleme
Rica etmek

{
  "method": "LIST_SUBSCRIPTIONS",
  "id": 3
}

Cevap

{
  "result": [
    "btcusdt@aggTrade"
  ],
  "id": 3
}

 Ayarlama
Şu anda ayarlanabilen tek özellik, akış yüklerinin etkinleştirilip etkinleştirilmeyeceğidir. Birleşik özellik , ("ham akışlar") kullanılarak bağlanırken ve kullanılarak bağlanırken combinedolarak ayarlanır .false/ws/true/stream/

Rica etmek

{
  "method": "SET_PROPERTY",
  "params": [
    "combined",
    true
  ],
  "id": 5
}

Cevap

{
  "result": null,
  "id": 5
}

 Alma
Rica etmek

{
  "method": "GET_PROPERTY",
  "params": [
    "combined"
  ],
  "id": 2
}

Cevap

{
  "result": true, // Indicates that combined is set to true.
  "id": 2
}


Hata
Hata Mesajı	Tanım
{"kod": 0, "msg": "Bilinmeyen özellik","id": %s}	SET_PROPERTYveya'da kullanılan parametre GET_PROPERTYgeçersizdi
{"kod": 1, "msg": "Geçersiz değer türü: beklenen Boolean"}	trueDeğer yalnızca veya olmalıdırfalse
{"code": 2, "msg": "Geçersiz istek: özellik adı bir dize olmalıdır"}	Sağlanan mülk adı geçersizdi
{"code": 2, "msg": "Geçersiz istek: istek kimliği işaretsiz bir tamsayı olmalıdır"}	Parametre idsağlanması gerekiyordu veya parametrede sağlanan değer iddesteklenmeyen bir türdü
{"kod": 2, "msg": "Geçersiz istek: bilinmeyen değişken %s, 1. satır 28. sütunda SUBSCRIBE, UNSUBSCRIBE, LIST_SUBSCRIPTIONS, SET_PROPERTY,' den biri bekleniyordu"}GET_PROPERTY	Sağlanan yöntemde olası bir yazım hatası veya sağlanan yöntem beklenen değerlerden hiçbiri değildi
{"code": 2, "msg": "Geçersiz istek: çok fazla parametre"}	Verilerde gereksiz parametreler sağlandı
{"code": 2, "msg": "Geçersiz istek: özellik adı bir dize olmalıdır"}	Mülk adı sağlanmadı
{"code": 2, "msg": "Geçersiz istek: method1. satır 73. sütunda eksik alan"}	methodverilerde sağlanmamıştır
{"code":3,"msg":"Geçersiz JSON: %s satırında beklenen değer %s sütununda"}	Gönderilen JSON verisinin söz dizimi hatalı.
Ayrıntılı Akış bilgisi
Toplam Ticaret
Toplu İşlem Akışları, tek bir alıcı emri için toplanan işlem bilgilerini iletir.

Akış Adı: <sembol>@aggTrade

Güncelleme Hızı: Gerçek zamanlı

Yük:

{
  "e": "aggTrade",    // Event type
  "E": 1672515782136, // Event time
  "s": "BNBBTC",      // Symbol
  "a": 12345,         // Aggregate trade ID
  "p": "0.001",       // Price
  "q": "100",         // Quantity
  "f": 100,           // First trade ID
  "l": 105,           // Last trade ID
  "T": 1672515782136, // Trade time
  "m": true,          // Is the buyer the market maker?
  "M": true           // Ignore
}


Ticaret
Ticaret Akışları ham ticaret bilgilerini iletir; her ticaretin kendine özgü bir alıcısı ve satıcısı vardır.

Akış Adı: <sembol>@trade

Güncelleme Hızı: Gerçek zamanlı

Yük:

{
  "e": "trade",       // Event type
  "E": 1672515782136, // Event time
  "s": "BNBBTC",      // Symbol
  "t": 12345,         // Trade ID
  "p": "0.001",       // Price
  "q": "100",         // Quantity
  "T": 1672515782136, // Trade time
  "m": true,          // Is the buyer the market maker?
  "M": true           // Ignore
}


 için Kline/Mum Akışları
Kline/Mum Akışı, UTC+0zaman dilimindeki her saniye mevcut kline/mum çubuğuna güncelleme gönderir

Kline/Mum grafik aralıkları:

s-> saniye; m -> dakika; h -> saat; g -> gün; h -> hafta; M -> ay

1s
1m
3m
5m
15m
30m
1s
2s
4s
6s
8s
12s
1 gün
3 boyutlu
1h
1M
Akış Adı: <sembol>@kline_<aralık>

Güncelleme Hızı: 1000ms 1s, diğer aralıklar için 2000ms

Yük:

{
  "e": "kline",         // Event type
  "E": 1672515782136,   // Event time
  "s": "BNBBTC",        // Symbol
  "k": {
    "t": 1672515780000, // Kline start time
    "T": 1672515839999, // Kline close time
    "s": "BNBBTC",      // Symbol
    "i": "1m",          // Interval
    "f": 100,           // First trade ID
    "L": 200,           // Last trade ID
    "o": "0.0010",      // Open price
    "c": "0.0020",      // Close price
    "h": "0.0025",      // High price
    "l": "0.0015",      // Low price
    "v": "1000",        // Base asset volume
    "n": 100,           // Number of trades
    "x": false,         // Is this kline closed?
    "q": "1.0000",      // Quote asset volume
    "V": "500",         // Taker buy base asset volume
    "Q": "0.500",       // Taker buy quote asset volume
    "B": "123456"       // Ignore
  }
}


Zaman dilimi
Kline/Mum Akışı, UTC+8zaman dilimindeki her saniye mevcut kline/mum çubuğuna güncelleme gönderir

Kline/Mum grafik aralıkları:

Desteklenen aralıklar: Bkz.Kline/Candlestick chart intervals

UTC+8 saat dilimi farkı:

Kline aralıkları UTC+8zaman diliminde açılır ve kapanır. Örneğin 1dkline'lar günün başında açılır UTC+8ve günün sonunda kapanır UTC+8.
Yükteki E(olay zamanı), t(başlangıç ​​zamanı) ve (kapanış zamanı) Unix zaman damgaları olduğunu ve her zaman UTC olarak yorumlandığını unutmayın .T
Akış Adı: <sembol>@kline_<aralık>@+08:00

Güncelleme Hızı: 1000ms 1s, diğer aralıklar için 2000ms

Yük:

{
  "e": "kline",         // Event type
  "E": 1672515782136,   // Event time
  "s": "BNBBTC",        // Symbol
  "k": {
    "t": 1672515780000, // Kline start time
    "T": 1672515839999, // Kline close time
    "s": "BNBBTC",      // Symbol
    "i": "1m",          // Interval
    "f": 100,           // First trade ID
    "L": 200,           // Last trade ID
    "o": "0.0010",      // Open price
    "c": "0.0020",      // Close price
    "h": "0.0025",      // High price
    "l": "0.0015",      // Low price
    "v": "1000",        // Base asset volume
    "n": 100,           // Number of trades
    "x": false,         // Is this kline closed?
    "q": "1.0000",      // Quote asset volume
    "V": "500",         // Taker buy base asset volume
    "Q": "0.500",       // Taker buy quote asset volume
    "B": "123456"       // Ignore
  }
}


Bireysel Sembol Mini Ticker
24 saatlik kayan pencere mini-ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir.

Akış Adı: <sembol>@miniTicker

Güncelleme Hızı: 1000ms

Yük:

  {
    "e": "24hrMiniTicker",  // Event type
    "E": 1672515782136,     // Event time
    "s": "BNBBTC",          // Symbol
    "c": "0.0025",          // Close price
    "o": "0.0010",          // Open price
    "h": "0.0025",          // High price
    "l": "0.0010",          // Low price
    "v": "10000",           // Total traded base asset volume
    "q": "18"               // Total traded quote asset volume
  }


Tüm Piyasa Mini Ticker
Bir dizide değişen tüm semboller için 24 saatlik kayan pencere mini-ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.

Akış Adı: !miniTicker@arr

Güncelleme Hızı: 1000ms

Yük:

[
  {
    // Same as <symbol>@miniTicker payload
  }
]


Bireysel Sembol Ticker
Tek bir sembol için 24 saatlik kayan pencere ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir.

Akış Adı: <sembol>@ticker

Güncelleme Hızı: 1000ms

Yük:

{
  "e": "24hrTicker",  // Event type
  "E": 1672515782136, // Event time
  "s": "BNBBTC",      // Symbol
  "p": "0.0015",      // Price change
  "P": "250.00",      // Price change percent
  "w": "0.0018",      // Weighted average price
  "x": "0.0009",      // First trade(F)-1 price (first trade before the 24hr rolling window)
  "c": "0.0025",      // Last price
  "Q": "10",          // Last quantity
  "b": "0.0024",      // Best bid price
  "B": "10",          // Best bid quantity
  "a": "0.0026",      // Best ask price
  "A": "100",         // Best ask quantity
  "o": "0.0010",      // Open price
  "h": "0.0025",      // High price
  "l": "0.0010",      // Low price
  "v": "10000",       // Total traded base asset volume
  "q": "18",          // Total traded quote asset volume
  "O": 0,             // Statistics open time
  "C": 86400000,      // Statistics close time
  "F": 0,             // First trade ID
  "L": 18150,         // Last trade Id
  "n": 18151          // Total number of trades
}


Tüm Piyasa Ticker
Bir dizide değişen tüm semboller için 24 saatlik kayan pencere ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.

Akış Adı: !ticker@arr

Güncelleme Hızı: 1000ms

Yük:

[
  {
    // Same as <symbol>@ticker payload
  }
]

Bireysel Sembol Kayan Pencere İstatistik
Tek bir sembol için birden fazla pencere üzerinden hesaplanan kayan pencere istatistikleri.

Akış Adı: <sembol>@ticker_<pencere_boyutu>

Pencere Boyutları: 1s,4s,1d

Güncelleme Hızı: 1000ms

Not : Bu akış <sembol>@ticker akışından farklıdır. Açılış zamanı "O"her zaman bir dakikada başlarken, kapanış zamanı "C"güncellemenin geçerli zamanıdır. Bu nedenle, etkili pencere <window_size>'dan 59999ms daha geniş olabilir.

Yük:

{
  "e": "1hTicker",    // Event type
  "E": 1672515782136, // Event time
  "s": "BNBBTC",      // Symbol
  "p": "0.0015",      // Price change
  "P": "250.00",      // Price change percent
  "o": "0.0010",      // Open price
  "h": "0.0025",      // High price
  "l": "0.0010",      // Low price
  "c": "0.0025",      // Last price
  "w": "0.0018",      // Weighted average price
  "v": "10000",       // Total traded base asset volume
  "q": "18",          // Total traded quote asset volume
  "O": 0,             // Statistics open time
  "C": 1675216573749, // Statistics close time
  "F": 0,             // First trade ID
  "L": 18150,         // Last trade Id
  "n": 18151          // Total number of trades
}


Tüm Piyasa Kayan Pencere İstatistik
Tüm piyasa sembolleri için yuvarlanan pencere ticker istatistikleri, birden fazla pencere üzerinden hesaplanır. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.

Akış Adı: !ticker_<pencere boyutu>@arr

Pencere Boyutu: 1s,4s,1g

Güncelleme Hızı: 1000ms

Yük:

[
  {
    // Same as <symbol>@ticker_<window-size> payload,
    // one for each symbol updated within the interval.
  }
]


Bireysel Sembol Kitabı Ticker
Belirli bir sembol için en iyi alış veya satış fiyatına veya miktarına gerçek zamanlı olarak herhangi bir güncelleme gönderir. Tek <symbol>@bookTickerbir bağlantı üzerinden birden fazla akışa abone olunabilir.

Akış Adı: <sembol>@bookTicker

Güncelleme Hızı: Gerçek zamanlı

Yük:

{
  "u":400900217,     // order book updateId
  "s":"BNBUSDT",     // symbol
  "b":"25.35190000", // best bid price
  "B":"31.21000000", // best bid qty
  "a":"25.36520000", // best ask price
  "A":"40.66000000"  // best ask qty
}


Ortalama
Ortalama fiyat akımları, sabit bir zaman aralığında ortalama fiyatlardaki değişiklikleri yansıtır.

Akış Adı: <sembol>@avgPrice

Güncelleme Hızı: 1000ms

Yük:

{
  "e": "avgPrice",          // Event type
  "E": 1693907033000,       // Event time
  "s": "BTCUSDT",           // Symbol
  "i": "5m",                // Average price interval
  "w": "25776.86000000",    // Average price
  "T": 1693907032213        // Last trade time
}


Kısmi Kitap Derinlik
En yüksek <seviye> teklifleri ve talepleri, her saniye itilir. Geçerli <seviye> 5, 10 veya 20'dir.

Akış Adları: <sembol>@depth<seviyeler> VEYA <sembol>@depth<seviyeler>@100ms

Güncelleme Hızı: 1000ms veya 100ms

Yük:

{
  "lastUpdateId": 160,  // Last update ID
  "bids": [             // Bids to be updated
    [
      "0.0024",         // Price level to be updated
      "10"              // Quantity
    ]
  ],
  "asks": [             // Asks to be updated
    [
      "0.0026",         // Price level to be updated
      "100"             // Quantity
    ]
  ]
}


Farklı Derinlik
Sipariş defterinin yerel olarak yönetilmesi için kullanılan sipariş defteri fiyat ve miktar derinliği güncellemeleri.

Akış Adı: <sembol>@depth VEYA <sembol>@depth@100ms

Güncelleme Hızı: 1000ms veya 100ms

Yük:

{
  "e": "depthUpdate", // Event type
  "E": 1672515782136, // Event time
  "s": "BNBBTC",      // Symbol
  "U": 157,           // First update ID in event
  "u": 160,           // Final update ID in event
  "b": [              // Bids to be updated
    [
      "0.0024",       // Price level to be updated
      "10"            // Quantity
    ]
  ],
  "a": [              // Asks to be updated
    [
      "0.0026",       // Price level to be updated
      "100"           // Quantity
    ]
  ]
}


Yerel sipariş defterini
wss://stream.binance.com:9443/ws/bnbbtc@depth adresine bir akış açın .
Akıştan aldığınız olayları arabelleğe alın.
https://api.binance.com/api/v3/depth?symbol=BNBBTC&limit=1000 adresinden derinlik anlık görüntüsünü alın .
Anlık görüntüde uis <= olan herhangi bir olayı bırakın .lastUpdateId
İlk işlenen olayın değeri U<= lastUpdateId+1 VE u >= lastUpdateId+1 olmalıdır.
Yayını dinlerken her yeni olayın değeri bir önceki olayın değerine +1 Ueşit olmalıdır .u
Her bir olaydaki veriler, bir fiyat düzeyi için mutlak niceliği oluşturur.
Miktar 0 ise fiyat seviyesini kaldırın .
Yerel emir defterinizde bulunmayan bir fiyat seviyesini kaldıran bir olay almanız mümkün ve normaldir.
Not: Derinlik anlık görüntülerinin fiyat seviyeleri sayısında bir sınırlama olması nedeniyle, miktar değişikliği olmayan ilk anlık görüntünün dışındaki bir fiyat seviyesi Diff. Depth Stream'de bir güncellemeye sahip olmayacaktır. Sonuç olarak, bu fiyat seviyeleri Diff. Depth Stream'den gelen tüm güncellemeler doğru şekilde uygulansa bile yerel emir defterinde görünmeyecek ve yerel emir defterinin gerçek emir defteriyle bazı ufak farklılıklara sahip olmasına neden olacaktır. Ancak, çoğu kullanım durumu için 5000'lik derinlik sınırı piyasayı anlamak ve etkili bir şekilde işlem yapmak için yeterlidir.

Öncesi
API'yi düzelt
Sonraki
Kullanıcı Veri Akışı
Telif Hakkı © 2024 Binance.
---
 README.md | 538 ++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 538 insertions(+)

diff --git a/README.md b/README.md
index fe4ca14..6809429 100644
--- a/README.md
+++ b/README.md
@@ -3,3 +3,541 @@
 * mkdocs is required 
 * view https://binanceapitest.github.io/Binance-api-doc/
 
+Ana içeriğe geç
+Binance Logo
+Web Soket Akışları
+
+Bu sayfada
+Binance için Web Socket Akışları (2024-06-11)
+Genel WSS bilgileri
+Temel uç nokta şudur: wss://stream.binance.com:9443 veya wss://stream.binance.com:443
+Akışlara tek bir ham akışta veya birleşik akışta erişilebilir
+Ham akışlara /ws/<streamName> adresinden erişilir
+Birleştirilmiş akışlara /stream?streams=<streamName1>/<streamName2>/<streamName3> adresinden erişilir
+Birleştirilmiş akış olayları aşağıdaki gibi sarılır: {"stream":"<streamName>","data":<rawPayload>}
+Akışlar için tüm semboller küçük harflidir
+Stream.binance.com'a tek bir bağlantı yalnızca 24 saat geçerlidir; 24 saatlik sürenin sonunda bağlantınızın kesilmesini bekleyin
+ping frameWebsocket sunucusu her 3 dakikada bir gönderecektir .
+pong frameEğer websocket sunucusu 10 dakika içerisinde bağlantıdan geri dönüş alamazsa bağlantı kesilecektir.
+Ping aldığınızda, mümkün olan en kısa sürede ping'in yükünün bir kopyasını içeren bir pong göndermelisiniz.
+İstenmeyenlere pong framesizin verilir, ancak bağlantının kesilmesini engellemez. Bu pong çerçeveleri için yükün boş olması önerilir.
+Temel uç nokta wss://data-stream.binance.vision yalnızca piyasa verisi mesajlarını almak için abone olunabilir .
+Kullanıcı veri akışı bu URL'den kullanılamaz .
+Websocket 
+WebSocket bağlantıları saniyede 5 gelen mesaj sınırına sahiptir. Bir mesaj şu şekilde değerlendirilir:
+Bir PING çerçevesi
+Bir PONG çerçevesi
+JSON kontrollü bir mesaj (örneğin abone ol, aboneliği iptal et)
+Sınırı aşan bağlantı kesilir; tekrar tekrar kesilen IP'ler yasaklanabilir.
+Tek bir bağlantıyla en fazla 1024 yayın dinlenebilir.
+Her IP için her 5 dakikada bir deneme başına 300 bağlantı sınırı vardır .
+Canlı 
+Akışlara abone olmak/abonelikten çıkmak için aşağıdaki veriler websocket örneği üzerinden gönderilebilir. Örnekler aşağıda görülebilir.
+idİleri geri giden mesajları benzersiz bir şekilde tanımlamak için bir tanımlayıcı olarak kullanılır. Aşağıdaki biçimler kabul edilir :
+64 bitlik işaretli tamsayı
+alfanümerik dizeler; maksimum uzunluk 36
+null
+Cevapta resultalınan nullbu ise, sorgu dışı istekler (örneğin Abone Olma/Abonelikten Çıkma) için gönderilen isteğin başarılı olduğu anlamına gelir.
+Bir 
+Rica etmek
+
+{
+  "method": "SUBSCRIBE",
+  "params": [
+    "btcusdt@aggTrade",
+    "btcusdt@depth"
+  ],
+  "id": 1
+}
+
+Cevap
+
+{
+  "result": null,
+  "id": 1
+}
+
+Bir 
+Rica etmek
+
+{
+  "method": "UNSUBSCRIBE",
+  "params": [
+    "btcusdt@depth"
+  ],
+  "id": 312
+}
+
+Cevap
+
+{
+  "result": null,
+  "id": 312
+}
+
+Listeleme 
+Rica etmek
+
+{
+  "method": "LIST_SUBSCRIPTIONS",
+  "id": 3
+}
+
+Cevap
+
+{
+  "result": [
+    "btcusdt@aggTrade"
+  ],
+  "id": 3
+}
+
+ Ayarlama
+Şu anda ayarlanabilen tek özellik, akış yüklerinin etkinleştirilip etkinleştirilmeyeceğidir. Birleşik özellik , ("ham akışlar") kullanılarak bağlanırken ve kullanılarak bağlanırken combinedolarak ayarlanır .false/ws/true/stream/
+
+Rica etmek
+
+{
+  "method": "SET_PROPERTY",
+  "params": [
+    "combined",
+    true
+  ],
+  "id": 5
+}
+
+Cevap
+
+{
+  "result": null,
+  "id": 5
+}
+
+ Alma
+Rica etmek
+
+{
+  "method": "GET_PROPERTY",
+  "params": [
+    "combined"
+  ],
+  "id": 2
+}
+
+Cevap
+
+{
+  "result": true, // Indicates that combined is set to true.
+  "id": 2
+}
+
+
+Hata 
+Hata Mesajı	Tanım
+{"kod": 0, "msg": "Bilinmeyen özellik","id": %s}	SET_PROPERTYveya'da kullanılan parametre GET_PROPERTYgeçersizdi
+{"kod": 1, "msg": "Geçersiz değer türü: beklenen Boolean"}	trueDeğer yalnızca veya olmalıdırfalse
+{"code": 2, "msg": "Geçersiz istek: özellik adı bir dize olmalıdır"}	Sağlanan mülk adı geçersizdi
+{"code": 2, "msg": "Geçersiz istek: istek kimliği işaretsiz bir tamsayı olmalıdır"}	Parametre idsağlanması gerekiyordu veya parametrede sağlanan değer iddesteklenmeyen bir türdü
+{"kod": 2, "msg": "Geçersiz istek: bilinmeyen değişken %s, 1. satır 28. sütunda SUBSCRIBE, UNSUBSCRIBE, LIST_SUBSCRIPTIONS, SET_PROPERTY,' den biri bekleniyordu"}GET_PROPERTY	Sağlanan yöntemde olası bir yazım hatası veya sağlanan yöntem beklenen değerlerden hiçbiri değildi
+{"code": 2, "msg": "Geçersiz istek: çok fazla parametre"}	Verilerde gereksiz parametreler sağlandı
+{"code": 2, "msg": "Geçersiz istek: özellik adı bir dize olmalıdır"}	Mülk adı sağlanmadı
+{"code": 2, "msg": "Geçersiz istek: method1. satır 73. sütunda eksik alan"}	methodverilerde sağlanmamıştır
+{"code":3,"msg":"Geçersiz JSON: %s satırında beklenen değer %s sütununda"}	Gönderilen JSON verisinin söz dizimi hatalı.
+Ayrıntılı Akış bilgisi
+Toplam Ticaret 
+Toplu İşlem Akışları, tek bir alıcı emri için toplanan işlem bilgilerini iletir.
+
+Akış Adı: <sembol>@aggTrade
+
+Güncelleme Hızı: Gerçek zamanlı
+
+Yük:
+
+{
+  "e": "aggTrade",    // Event type
+  "E": 1672515782136, // Event time
+  "s": "BNBBTC",      // Symbol
+  "a": 12345,         // Aggregate trade ID
+  "p": "0.001",       // Price
+  "q": "100",         // Quantity
+  "f": 100,           // First trade ID
+  "l": 105,           // Last trade ID
+  "T": 1672515782136, // Trade time
+  "m": true,          // Is the buyer the market maker?
+  "M": true           // Ignore
+}
+
+
+Ticaret 
+Ticaret Akışları ham ticaret bilgilerini iletir; her ticaretin kendine özgü bir alıcısı ve satıcısı vardır.
+
+Akış Adı: <sembol>@trade
+
+Güncelleme Hızı: Gerçek zamanlı
+
+Yük:
+
+{
+  "e": "trade",       // Event type
+  "E": 1672515782136, // Event time
+  "s": "BNBBTC",      // Symbol
+  "t": 12345,         // Trade ID
+  "p": "0.001",       // Price
+  "q": "100",         // Quantity
+  "T": 1672515782136, // Trade time
+  "m": true,          // Is the buyer the market maker?
+  "M": true           // Ignore
+}
+
+
+ için Kline/Mum Akışları
+Kline/Mum Akışı, UTC+0zaman dilimindeki her saniye mevcut kline/mum çubuğuna güncelleme gönderir
+
+Kline/Mum grafik aralıkları:
+
+s-> saniye; m -> dakika; h -> saat; g -> gün; h -> hafta; M -> ay
+
+1s
+1m
+3m
+5m
+15m
+30m
+1s
+2s
+4s
+6s
+8s
+12s
+1 gün
+3 boyutlu
+1h
+1M
+Akış Adı: <sembol>@kline_<aralık>
+
+Güncelleme Hızı: 1000ms 1s, diğer aralıklar için 2000ms
+
+Yük:
+
+{
+  "e": "kline",         // Event type
+  "E": 1672515782136,   // Event time
+  "s": "BNBBTC",        // Symbol
+  "k": {
+    "t": 1672515780000, // Kline start time
+    "T": 1672515839999, // Kline close time
+    "s": "BNBBTC",      // Symbol
+    "i": "1m",          // Interval
+    "f": 100,           // First trade ID
+    "L": 200,           // Last trade ID
+    "o": "0.0010",      // Open price
+    "c": "0.0020",      // Close price
+    "h": "0.0025",      // High price
+    "l": "0.0015",      // Low price
+    "v": "1000",        // Base asset volume
+    "n": 100,           // Number of trades
+    "x": false,         // Is this kline closed?
+    "q": "1.0000",      // Quote asset volume
+    "V": "500",         // Taker buy base asset volume
+    "Q": "0.500",       // Taker buy quote asset volume
+    "B": "123456"       // Ignore
+  }
+}
+
+
+Zaman dilimi 
+Kline/Mum Akışı, UTC+8zaman dilimindeki her saniye mevcut kline/mum çubuğuna güncelleme gönderir
+
+Kline/Mum grafik aralıkları:
+
+Desteklenen aralıklar: Bkz.Kline/Candlestick chart intervals
+
+UTC+8 saat dilimi farkı:
+
+Kline aralıkları UTC+8zaman diliminde açılır ve kapanır. Örneğin 1dkline'lar günün başında açılır UTC+8ve günün sonunda kapanır UTC+8.
+Yükteki E(olay zamanı), t(başlangıç zamanı) ve (kapanış zamanı) Unix zaman damgaları olduğunu ve her zaman UTC olarak yorumlandığını unutmayın .T
+Akış Adı: <sembol>@kline_<aralık>@+08:00
+
+Güncelleme Hızı: 1000ms 1s, diğer aralıklar için 2000ms
+
+Yük:
+
+{
+  "e": "kline",         // Event type
+  "E": 1672515782136,   // Event time
+  "s": "BNBBTC",        // Symbol
+  "k": {
+    "t": 1672515780000, // Kline start time
+    "T": 1672515839999, // Kline close time
+    "s": "BNBBTC",      // Symbol
+    "i": "1m",          // Interval
+    "f": 100,           // First trade ID
+    "L": 200,           // Last trade ID
+    "o": "0.0010",      // Open price
+    "c": "0.0020",      // Close price
+    "h": "0.0025",      // High price
+    "l": "0.0015",      // Low price
+    "v": "1000",        // Base asset volume
+    "n": 100,           // Number of trades
+    "x": false,         // Is this kline closed?
+    "q": "1.0000",      // Quote asset volume
+    "V": "500",         // Taker buy base asset volume
+    "Q": "0.500",       // Taker buy quote asset volume
+    "B": "123456"       // Ignore
+  }
+}
+
+
+Bireysel Sembol Mini Ticker 
+24 saatlik kayan pencere mini-ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir.
+
+Akış Adı: <sembol>@miniTicker
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+  {
+    "e": "24hrMiniTicker",  // Event type
+    "E": 1672515782136,     // Event time
+    "s": "BNBBTC",          // Symbol
+    "c": "0.0025",          // Close price
+    "o": "0.0010",          // Open price
+    "h": "0.0025",          // High price
+    "l": "0.0010",          // Low price
+    "v": "10000",           // Total traded base asset volume
+    "q": "18"               // Total traded quote asset volume
+  }
+
+
+Tüm Piyasa Mini Ticker 
+Bir dizide değişen tüm semboller için 24 saatlik kayan pencere mini-ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.
+
+Akış Adı: !miniTicker@arr
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+[
+  {
+    // Same as <symbol>@miniTicker payload
+  }
+]
+
+
+Bireysel Sembol Ticker 
+Tek bir sembol için 24 saatlik kayan pencere ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir.
+
+Akış Adı: <sembol>@ticker
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+{
+  "e": "24hrTicker",  // Event type
+  "E": 1672515782136, // Event time
+  "s": "BNBBTC",      // Symbol
+  "p": "0.0015",      // Price change
+  "P": "250.00",      // Price change percent
+  "w": "0.0018",      // Weighted average price
+  "x": "0.0009",      // First trade(F)-1 price (first trade before the 24hr rolling window)
+  "c": "0.0025",      // Last price
+  "Q": "10",          // Last quantity
+  "b": "0.0024",      // Best bid price
+  "B": "10",          // Best bid quantity
+  "a": "0.0026",      // Best ask price
+  "A": "100",         // Best ask quantity
+  "o": "0.0010",      // Open price
+  "h": "0.0025",      // High price
+  "l": "0.0010",      // Low price
+  "v": "10000",       // Total traded base asset volume
+  "q": "18",          // Total traded quote asset volume
+  "O": 0,             // Statistics open time
+  "C": 86400000,      // Statistics close time
+  "F": 0,             // First trade ID
+  "L": 18150,         // Last trade Id
+  "n": 18151          // Total number of trades
+}
+
+
+Tüm Piyasa Ticker 
+Bir dizide değişen tüm semboller için 24 saatlik kayan pencere ticker istatistikleri. Bunlar UTC gününün istatistikleri DEĞİLDİR, ancak önceki 24 saat için 24 saatlik kayan bir penceredir. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.
+
+Akış Adı: !ticker@arr
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+[
+  {
+    // Same as <symbol>@ticker payload
+  }
+]
+
+Bireysel Sembol Kayan Pencere İstatistik 
+Tek bir sembol için birden fazla pencere üzerinden hesaplanan kayan pencere istatistikleri.
+
+Akış Adı: <sembol>@ticker_<pencere_boyutu>
+
+Pencere Boyutları: 1s,4s,1d
+
+Güncelleme Hızı: 1000ms
+
+Not : Bu akış <sembol>@ticker akışından farklıdır. Açılış zamanı "O"her zaman bir dakikada başlarken, kapanış zamanı "C"güncellemenin geçerli zamanıdır. Bu nedenle, etkili pencere <window_size>'dan 59999ms daha geniş olabilir.
+
+Yük:
+
+{
+  "e": "1hTicker",    // Event type
+  "E": 1672515782136, // Event time
+  "s": "BNBBTC",      // Symbol
+  "p": "0.0015",      // Price change
+  "P": "250.00",      // Price change percent
+  "o": "0.0010",      // Open price
+  "h": "0.0025",      // High price
+  "l": "0.0010",      // Low price
+  "c": "0.0025",      // Last price
+  "w": "0.0018",      // Weighted average price
+  "v": "10000",       // Total traded base asset volume
+  "q": "18",          // Total traded quote asset volume
+  "O": 0,             // Statistics open time
+  "C": 1675216573749, // Statistics close time
+  "F": 0,             // First trade ID
+  "L": 18150,         // Last trade Id
+  "n": 18151          // Total number of trades
+}
+
+
+Tüm Piyasa Kayan Pencere İstatistik 
+Tüm piyasa sembolleri için yuvarlanan pencere ticker istatistikleri, birden fazla pencere üzerinden hesaplanır. Dizide yalnızca değişen ticker'ların bulunacağını unutmayın.
+
+Akış Adı: !ticker_<pencere boyutu>@arr
+
+Pencere Boyutu: 1s,4s,1g
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+[
+  {
+    // Same as <symbol>@ticker_<window-size> payload,
+    // one for each symbol updated within the interval.
+  }
+]
+
+
+Bireysel Sembol Kitabı Ticker 
+Belirli bir sembol için en iyi alış veya satış fiyatına veya miktarına gerçek zamanlı olarak herhangi bir güncelleme gönderir. Tek <symbol>@bookTickerbir bağlantı üzerinden birden fazla akışa abone olunabilir.
+
+Akış Adı: <sembol>@bookTicker
+
+Güncelleme Hızı: Gerçek zamanlı
+
+Yük:
+
+{
+  "u":400900217,     // order book updateId
+  "s":"BNBUSDT",     // symbol
+  "b":"25.35190000", // best bid price
+  "B":"31.21000000", // best bid qty
+  "a":"25.36520000", // best ask price
+  "A":"40.66000000"  // best ask qty
+}
+
+
+Ortalama 
+Ortalama fiyat akımları, sabit bir zaman aralığında ortalama fiyatlardaki değişiklikleri yansıtır.
+
+Akış Adı: <sembol>@avgPrice
+
+Güncelleme Hızı: 1000ms
+
+Yük:
+
+{
+  "e": "avgPrice",          // Event type
+  "E": 1693907033000,       // Event time
+  "s": "BTCUSDT",           // Symbol
+  "i": "5m",                // Average price interval
+  "w": "25776.86000000",    // Average price
+  "T": 1693907032213        // Last trade time
+}
+
+
+Kısmi Kitap Derinlik 
+En yüksek <seviye> teklifleri ve talepleri, her saniye itilir. Geçerli <seviye> 5, 10 veya 20'dir.
+
+Akış Adları: <sembol>@depth<seviyeler> VEYA <sembol>@depth<seviyeler>@100ms
+
+Güncelleme Hızı: 1000ms veya 100ms
+
+Yük:
+
+{
+  "lastUpdateId": 160,  // Last update ID
+  "bids": [             // Bids to be updated
+    [
+      "0.0024",         // Price level to be updated
+      "10"              // Quantity
+    ]
+  ],
+  "asks": [             // Asks to be updated
+    [
+      "0.0026",         // Price level to be updated
+      "100"             // Quantity
+    ]
+  ]
+}
+
+
+Farklı Derinlik 
+Sipariş defterinin yerel olarak yönetilmesi için kullanılan sipariş defteri fiyat ve miktar derinliği güncellemeleri.
+
+Akış Adı: <sembol>@depth VEYA <sembol>@depth@100ms
+
+Güncelleme Hızı: 1000ms veya 100ms
+
+Yük:
+
+{
+  "e": "depthUpdate", // Event type
+  "E": 1672515782136, // Event time
+  "s": "BNBBTC",      // Symbol
+  "U": 157,           // First update ID in event
+  "u": 160,           // Final update ID in event
+  "b": [              // Bids to be updated
+    [
+      "0.0024",       // Price level to be updated
+      "10"            // Quantity
+    ]
+  ],
+  "a": [              // Asks to be updated
+    [
+      "0.0026",       // Price level to be updated
+      "100"           // Quantity
+    ]
+  ]
+}
+
+
+Yerel sipariş defterini 
+wss://stream.binance.com:9443/ws/bnbbtc@depth adresine bir akış açın .
+Akıştan aldığınız olayları arabelleğe alın.
+https://api.binance.com/api/v3/depth?symbol=BNBBTC&limit=1000 adresinden derinlik anlık görüntüsünü alın .
+Anlık görüntüde uis <= olan herhangi bir olayı bırakın .lastUpdateId
+İlk işlenen olayın değeri U<= lastUpdateId+1 VE u >= lastUpdateId+1 olmalıdır.
+Yayını dinlerken her yeni olayın değeri bir önceki olayın değerine +1 Ueşit olmalıdır .u
+Her bir olaydaki veriler, bir fiyat düzeyi için mutlak niceliği oluşturur.
+Miktar 0 ise fiyat seviyesini kaldırın .
+Yerel emir defterinizde bulunmayan bir fiyat seviyesini kaldıran bir olay almanız mümkün ve normaldir.
+Not: Derinlik anlık görüntülerinin fiyat seviyeleri sayısında bir sınırlama olması nedeniyle, miktar değişikliği olmayan ilk anlık görüntünün dışındaki bir fiyat seviyesi Diff. Depth Stream'de bir güncellemeye sahip olmayacaktır. Sonuç olarak, bu fiyat seviyeleri Diff. Depth Stream'den gelen tüm güncellemeler doğru şekilde uygulansa bile yerel emir defterinde görünmeyecek ve yerel emir defterinin gerçek emir defteriyle bazı ufak farklılıklara sahip olmasına neden olacaktır. Ancak, çoğu kullanım durumu için 5000'lik derinlik sınırı piyasayı anlamak ve etkili bir şekilde işlem yapmak için yeterlidir.
+
+Öncesi
+API'yi düzelt
+Sonraki
+Kullanıcı Veri Akışı
+Telif Hakkı © 2024 Binance.
