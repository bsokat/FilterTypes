# FilterTypes

<h3>Bu proje ASP.NET MVC'de filtreleme ve filtre çeşitleri konularının kavranması amacıyla yapılmıştır.</h3>

## Özet

Bu projede kullanıcının sayfalar arasında gezinmesi sırasında yaptığı işlemler loglanmaktadır. Loglama işlemini gerçekleştirmek amacıylada **filtrelerden** yararlanılmıştır. Projeye ASP.NET MVC'de bulunan 4 çeşit filtreleme eklenmiştir.

####Bunlar eklenme sırasıyla:
	- Action Filter
	- Result Filter
	- Exception Filter
	- Authorize Filter

## Eklenen veya Güncellenen Dosyalar

- Controller 
	1. ErrorController.cs
	2. HomeController.cs
- Filters
	1. LogAttribute.cs
- Models
	1. Log.cs
	2. LogsData.cs
- Views
	1. Error
		- Index.cshtml
	2. Home
		- Logs.cshtml
	3. Shared
		- _Layout.cshtml
		- Error.cshtml
		- FormatError.cshtml
- Web.config

## Filtrelerin Test Edilmesi

#### Action Filter:

Action filtreleri, bir action çalışmadan hemen önce ya da hemen sonra çalışan filtredir. Oluşturulan filtre sınıfı, işlem yapılacak action'a attribute olarak tanımlandıktan sonra çalışmaya başlar.

İlk olarak **Log attribute**'u tanımlı sayfa açılır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ActionFilter1.png)

Daha sonra logların tutulduğu **Logs** sayfası açılır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ActionFilter2.png)

Üstteki ekran görüntüsündeki tip çeşitlerinden **Before**, action'ın çalışmadan hemen önce çalışan metodu yani **onActionExecuting** metodunun çalıştığını temsil eder. onActionExecuting metodu **ActionExecutingContent** türünden bir nesne alır. Bu nesne ile işlem yapılan controller ve action bilgileri ile varsa action'a gönderilen parametrelere ulaşılabilinir.

Yine aynı ekran görüntüsündeki tip çeşitlerinden **After**, action'ın çalışmasını tamamlamasından hemen sonra çalışan metodu yani **onActionExecuted** metodunun çalıştığını temsil eder. onActionExecuted metodu **ActionExecutedContent** türünden bir nesne alır. Bu nesne ile işlem yapılan controller ve action bilgileri, action'un çalışması sırasında hata var mı bilgisi, oluşabilecek hatanın hata detayı, action çalışması sırasında iptal edildi mi bilgisi ile action'ın çalışması ardından geri dönen değer bilgilerine ulaşılabilinir.

> Action'a tanımlanan **Log attribute**, tek tek action'lara tanımlamak yerine controller içindeki tüm action'larda geçerli olması isteniyorsa, action yerine controller sınıfına tanımlanmalıdır.

#### Result Filter:

Result filtreleri, bir action çalıştıktan sonra geri dönüş verisinin derlenmeye başlamasından hemen önce ya da hemen sonrasında çalışan filtrelerdir. Oluşturulan filtre sınıfı, işlem yapılacak action'a attribute olarak tanımlandıktan sonra çalışmaya başlar.

İlk olarak **Log attribute**'u tanımlı sayfa açılır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ResultFilter1.png)

Daha sonra logların tutulduğu **Logs** sayfası açılır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ResultFilter2.png)

Üstteki ekran görüntüsündeki tip çeşitlerinden **Before Result**, action'ın geri dönüş verisi işlenmeden hemen önce çalışan metodu yani **onResultExecuting** metodunun çalıştığını temsil eder. onResultExecuting metodu **ResultExecutingContent** türünden bir nesne alır. Bu nesne ile işlem yapılan controller bilgisi, action'ın geri dönüş değeri, sonucun çalışması sırasında hata var mı bilgisi, oluşabilecek hatanın hata detayı, sonucun çalışması sırasında iptal edildi mi bilgisi  ile **RouteData** ve **HttpContext** nesneleri bulunur.

Yine aynı ekran görüntüsündeki tip çeşitlerinden **After Result**, action'ın geri dönüş verisi işlenmeden hemen sonra çalışan metodu yani **onResultExecuted** metodunun çalıştığını temsil eder. onResultExecuted metodu **ResultExecutedContent** türünden bir nesne alır. Bu nesne ile işlem yapılan controller bilgisi, action'ın geri dönüş değeri, sonucun çalışması sırasında hata var mı bilgisi, oluşabilecek hatanın hata detayı, sonucun çalışması sırasında iptal edildi mi bilgisi  ile **RouteData** ve **HttpContext** nesneleri bulunur.

#### Result Filter:

Exception filtreleri, projenin çalışması sırasında oluşan hataları yakalayıp işlem yapılmasını sağlayan filtredir. Oluşturulan filtre sınıfı, işlem yapılacak action'a ya da controller'a attribute olarak tanımlandıktan sonra çalışmaya başlar.

İlk olarak format hatası fırlatan view açılmaya çalışılır ve alttaki ekran görüntüsündeki gibi hata yakalanır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ExceptionFilter1.png)

Proje devam ettirildiği zaman, görüntülenmek istenilen view yerine hata bilgilerinin bulunduğu hata view'ine yönlendirilir.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ExceptionFilter2.png)

Daha sonra logların tutulduğu **Logs** sayfası açılır.

![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/ExceptionFilter3.png)

Üstteki ekran görüntüsündeki tip çeşitlerinden **Error**, uygulama içinde bir hata oluştuğunda çalışan metodu yani **onException** metodunun çalıştığını temsil eder. onException metodu **ExceptionContent** türünden bir nesne alır. Bu nesne ile işlem yapılan controller bilgisi, action'ın geri dönüş değeri, sonucun çalışması sırasında hata var mı bilgisi, oluşabilecek hatanın hata detayı, sonucun çalışması sırasında iptal edildi mi bilgisi  ile **RouteData** ve **HttpContext** nesneleri bulunur.

#### Authorize Filter:

Authorize filtreleri, projede controller ve action'lara kullanıcı ve roller bazında yetkilendirmenin yapılmasını sağlayan filtredir. Oluşturulan filtre sınıfı, işlem yapılacak action'a ya da controller'a attribute olarak tanımlandıktan sonra çalışmaya başlar.

> Bu projede çalışmasını istediğimiz action'a **Authorize attribute**'u tanımlanmıştır ve herhangi bir kullanıcının bu siteye erişimi kesilmiştir.

> ![alt tag](https://github.com/bsokat/FilterTypes/blob/master/Source/AuthorizationFilter1.png)

> Ancak proje oluşturulurken Individual User Accounts seçeneği seçilmediği için, herhangi bir kullanıcı oluşturma ve kullanıcı girişi yapılamamaktadır. Projenin amacı sadece filtreleme olduğu için ayrı bir şekilde de yapılmamıştır. Ancak Authorization filtresinde tanımlı olan kullanıcı adıyla bir kullanıcı oluşturulup, bu kullanıcı ile giriş işleminden sonra istenilen sayfaya ulaşılmak istendiğinde başarılı bir şekilde ulaşılacaktır.