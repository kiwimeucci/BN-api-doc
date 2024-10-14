# Binance-api-doc

* mkdocs is required 
* view https://binanceapitest.github.io/Binance-api-doc/

# Binance Logo
*USDⓈ-M Vadeli İşlemlerGenel *Bilgi

# Bu sayfada Genel Bilgi
* Uç noktaların çoğu testnet * platformunda kullanılabilir.
Testnet için REST temel URL'si " https://testnet.binancefuture.com "
Testnet için Websocket temel URL'si "wss://stream.binancefuture.com"dur.
SDK ve Kod 
Yasal Uyarı:

# Aşağıdaki SDK'lar ortaklar ve kullanıcılar tarafından sağlanır ve resmi olarak üretilmiştir. Bunlar yalnızca kullanıcıların API uç noktasına aşina olmalarına yardımcı olmak için kullanılır. Lütfen dikkatli kullanın ve kendi durumunuza göre Ar-Ge'yi genişletin.

Binance, SDK'ların güvenliği ve performansı konusunda herhangi bir taahhütte bulunmaz ve SDK'ların kullanımından kaynaklanan risklerden veya kayıplardan sorumlu tutulamaz.

# SDK: Binance Futures Connector için sağlanan SDK'yı edinmek için
lütfen https://github.com/binance/binance-futures-connector-python adresini ziyaret edin veya
aşağıdaki komutu kullanın:
pip install binance-futures-connector

# Binance Futures için sağlanan SDK'yı edinmek için
lütfen https://github.com/binance/binance-futures-connector-java adresini ziyaret edin veya
aşağıdaki komutu kullanın:
git clone https://github.com/binance/binance-futures-connector-java.git

# Genel API 
Bazı uç noktalar bir API Anahtarı gerektirecektir. Lütfen bu sayfaya bakın
# Temel uç nokta şudur: https://fapi.binance.com

# Tüm uç noktalar bir JSON nesnesi veya dizisi döndürür.
Veriler artan sırada döndürülür . En eskisi ilk, en yenisi son.
Tüm zaman ve zaman damgası ile ilgili alanlar milisaniye cinsindendir.
JAVA'da tüm veri tipleri tanımı benimser.
HTTP Dönüş 
Hatalı istekler için HTTP 4XXdönüş kodları kullanılır; sorun gönderici tarafındadır.
403WAF Limiti (Web Uygulama Güvenlik Duvarı) ihlal edildiğinde HTTP dönüş kodu kullanılır.
HTTP 408dönüş kodu, arka uç sunucusundan yanıt beklenirken zaman aşımı oluştuğunda kullanılır.
429İstek oranı sınırını aşarken HTTP dönüş kodu kullanılır.
HTTP 418dönüş kodu, bir IP'nin kod aldıktan sonra istek göndermeye devam etmesi nedeniyle otomatik olarak yasaklanması durumunda kullanılır 429.
Dahili hatalar için HTTP 5XXdönüş kodları kullanılıyor; sorun Binance'in tarafında.
"İstek bilinmeyen bir hatayla oluştu." hata mesajıyla karşılaşırsanız lütfen daha sonra tekrar deneyin.
HTTP 503dönüş kodu şu durumlarda kullanılır:
Yanıtta "Bilinmeyen hata, lütfen isteğinizi kontrol edin veya daha sonra tekrar deneyin." hata mesajı döndürülürse, API isteği başarıyla göndermiş ancak zaman aşımı süresi içinde bir yanıt almamıştır. Bunu bir başarısızlık işlemi olarak değerlendirmemek
önemlidir ; yürütme durumu BİLİNMİYOR ve başarılı olabilirdi;
Yanıtta "Hizmet Kullanılamıyor." hata mesajı döndürülürse , bu başarısız bir API işlemi olduğu ve hizmetin şu anda kullanılamıyor olabileceği anlamına gelir, daha sonra tekrar denemeniz gerekir.
Yanıtta "Dahili hata; isteğiniz işlenemedi. Lütfen tekrar deneyin." hata mesajı döndürülürse , bu başarısız bir API işlemi anlamına gelir ve gerekirse isteğinizi yeniden gönderebilirsiniz.
Hata Kodları ve 
Herhangi bir uç nokta bir HATA döndürebilir
Hata yükü şu şekildedir:

{
  "code": -1121,
  "msg": "Invalid symbol."
}

Hata Kodları'nda tanımlanan belirli hata kodları ve mesajları .
 Hakkında Genel Bilgiler
Uç noktalar için GETparametreler . olarak gönderilmelidir query string.
POST, PUT, ve uç noktaları için parametreler veya içerik türünde gönderilebilir DELETE. İsterseniz hem ve arasında parametreleri karıştırabilirsiniz .query stringrequest bodyapplication/x-www-form-urlencodedquery stringrequest body
Parametreler herhangi bir sırayla gönderilebilir.
query stringBir parametre hem 'de hem de ' de gönderilirse request body, query stringparametre kullanılacaktır.
Dizi /fapi/v1/exchangeInfo rateLimits, borsanın RAW_REQUEST, REQUEST_WEIGHT, ve oran limitleriyle ilgili nesneleri içerir. Bunlar , altındaki bölümde ORDERdaha ayrıntılı olarak tanımlanmıştır .ENUM definitionsRate limiters (rateLimitType)
Herhangi bir oran sınırının ihlal edilmesi durumunda A 429döndürülecektir.
Binance, saldırı niyetinde olan kullanıcılara yönelik oran limitlerini daha da sıkılaştırma hakkına sahiptir.
IP 
X-MBX-USED-WEIGHT-(intervalNum)(intervalLetter)Her istek , yanıt başlıklarında tanımlanan tüm istek oranı sınırlayıcıları için IP için kullanılan geçerli ağırlığı içerecektir .
Her rota, weighther uç noktanın saydığı istek sayısını belirleyen bir 'e sahiptir. Daha ağır uç noktalar ve birden fazla sembol üzerinde işlem yapan uç noktalar daha ağır bir weight.
429 aldığınızda, API olarak geri çekilmeniz ve API'ye spam göndermemeniz sizin sorumluluğunuzdur.
Hız sınırlarının tekrar tekrar ihlal edilmesi ve/veya 429 aldıktan sonra geri çekilmemenin başarısız olması, otomatik IP yasağına (HTTP durumu 418) neden olacaktır.
IP yasakları takip ediliyor ve tekrarlayan ihlaller için süresi 2 dakikadan 3 güne kadar değişiyor .
API'deki sınırlamalar API anahtarlarına değil IP'lere dayanmaktadır.
Verileri mümkün olduğunca almak için websocket akışının kullanılması şiddetle tavsiye edilir; bu, yalnızca mesajın zamanında iletilmesini sağlamakla kalmaz, aynı zamanda istekten kaynaklanan erişim kısıtlama baskısını da azaltır.
Sipariş Oranı 
X-MBX-ORDER-COUNT-(intervalNum)(intervalLetter)Her emir yanıtı , tanımlanan tüm emir oranı sınırlayıcıları için hesaba ait geçerli emir sayısını içeren bir başlık içerecektir .
X-MBX-ORDER-COUNT-**Reddedilen/başarısız siparişlerin yanıtta başlıklara sahip olması garanti edilmez .
Her hesaba karşılık emir oranı limiti hesaplanır .
Uç Nokta Güvenlik 
Her uç noktanın, onunla nasıl etkileşim kuracağınızı belirleyen bir güvenlik türü vardır.
API anahtarları başlık aracılığıyla Rest API'ye geçirilir X-MBX-APIKEY .
API anahtarları ve gizli anahtarlar büyük/küçük harfe duyarlıdır .
API anahtarları yalnızca belirli türdeki güvenli uç noktalara erişecek şekilde yapılandırılabilir. Örneğin, bir API anahtarı yalnızca TİCARET için kullanılabilirken, başka bir API anahtarı TİCARET rotaları hariç her şeye erişebilir.
Varsayılan olarak API anahtarları tüm güvenli rotalara erişebilir.
Güvenlik Türü	Tanım
HİÇBİRİ	Son noktaya serbestçe erişilebilir.
TİCARET	Son nokta geçerli bir API Anahtarı ve imza gönderilmesini gerektirir.
KULLANICI_VERİLERİ	Son nokta geçerli bir API Anahtarı ve imza gönderilmesini gerektirir.
KULLANICI_AKIŞI	Son nokta geçerli bir API Anahtarı gönderilmesini gerektirir.
PAZAR_VERİLERİ	Son nokta geçerli bir API Anahtarı gönderilmesini gerektirir.
TRADEve USER_DATAuç noktalar SIGNEDuç noktalardır.
İMZALANMIŞ (TİCARET ve KULLANICI_VERİSİ) Uç Nokta 
SIGNEDuç noktaların veya signatureiçinde gönderilecek ek bir parametreye, , ihtiyacı vardır .query stringrequest body
HMAC SHA256Uç noktalar imzaları kullanır . HMAC SHA256 signatureAnahtarlı bir işlemdir. Anahtar olarak your ve HMAC işlemi için değer olarak HMAC SHA256your kullanın .secretKeytotalParams
signatureBüyük / küçük harfe duyarlı değildir .
Lütfen bunun veya ' signaturenizin son kısmı olduğundan emin olun .query stringrequest body
totalParamsquery string, ile birleştirilmiş olarak tanımlanır request body
