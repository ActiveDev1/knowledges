انواع metrics های Prometheus معمولاً به چهار نوع اصلی تقسیم می‌شوند: 
1. #Counter
2. #Gauge 
3. #Histogram
4. #Summary
دو نوع اول metrics نسبتاً ساده‌اند و در چگونگی اندازه‌گیری هر چیزی که نام آنها را دارد، قرار می‌گیرند، در حالی که دو نوع دیگر کمی پیچیده‌تر هستند.

![[Prometheus-Metrics-Types.png]]

---
 #Counter
شمارنده‌ها برای شمارش تجمعی رویدادها استفاده می‌شوند، همانطور که از نام آن پیداست: به آن مانند یک شمارنده دستی فکر کنید که مردم برای نگه داشتن زبانه‌ها در اندازه یک جمعیت در یک مکان معین استفاده می‌کنند.
مقدار یک Counter فقط می‌تواند افزایش یابد یا هنگامی که دوباره راه‌اندازی می‌شود به صفر بازنشانی شود. هرگز به تنهایی کاهش نمی‌یابد. به عنوان مثال برای نشان دادن تعداد خطاها یا وظایف تکمیل شده بسته به مورد استفاده مورد استفاده قرار گیرد.

**مثال**: (nginx_http_requests_total) این metric تعداد کل request های وب‌سرور Nginx که به صورت افزایشی مقدار آن زیاد می‌شود را نشان می‌دهد.

![[Metrics-Explorer-Counter.png]]
می‌توان از بخش Metrics explorer مانند تصویر بالا اطلاعاتی مانند Type و Description هر metric را به دست آورد.
![[Metrics-Explorer-In-Dashboard.png]]

---
#Gauge
گِیج‌ها معمولاً آخرین مقدار اندازه‌گیری را نمایش می‌دهند. هیچ تفاوتی با گیج روی داشبورد اتومبیل ندارد که نشان می‌دهد چقدر بنزین در باک باقی مانده است، یا یک دماسنج که دما را در داخل یا بیرون نشان می‌دهد. برخلاف یک Counter، یک گیج می‌تواند بسته به اتفاقاتی که با نقطه اندازه‌گیری شده رخ می‌دهد، بالا یا پایین برود.
برای metricهایی که توسط  Client Prometheus جمع‌آوری می‌شوند، این می‌تواند شامل زمینه‌هایی مانند تعداد درخواست‌های همزمان یا میزان استفاده از CPU در طی یک دوره زمانی باشد.

**مثال**: (container_memory_usage_bytes) این metric میزان حافظه‌ای را که توسط یک کانتینر Docker استفاده شده است را نشان می‌دهد. این metric می‌تواند افزایش یا کاهش یابد بسته به میزان حافظه‌ای که کانتینر در زمان‌های مختلف استفاده می‌کند.

![[Metrics-Explorer-gauge.png]]

---
#Histogram
نوعی metric است که برای نمایش توزیع داده‌ها در بازه‌های مشخص استفاده می‌شود. این ابزار برای درک توزیع یک مجموعه داده مفید است، مانند زمان response time یا response size هایی که توسط یک سرویس وب صادر می‌شود.
##### چگونگی کارکرد Histogram ها

هیستوگرام ها داده‌ها را در bucket‌ هایی (buckets) قرار می‌دهند. هر bucket یک بازه مقداری را نمایندگی می‌کند. تعداد داده‌هایی که در هر bucket قرار می‌گیرند، شمرده می‌شود که به ما می‌گوید چند مورد از داده‌ها در هر بازه مقداری قرار دارند.

```PromQL
grafana_http_request_duration_seconds_sum
grafana_http_request_duration_seconds_count
grafana_http_request_duration_seconds_bucket
```
##### اجزای یک Histogram در Prometheus

1. **_count**
    شمارش کل مواردی که مشاهده شده‌اند.
2. **_sum**
    مجموع تمام مقادیر اندازه‌گیری‌هایی که انجام شده‌اند.
4. **_bucket**
    نشان دهنده تعداد مواردی که در هر bucket قرار گرفته‌اند.
    هر bucket دارای یک برچسب (label) `le` است که نشان‌دهنده حد بالایی bucket است.

![[Metrics-Explorer-gauge-Histogram.png]]
##### مثال

 **۱. grafana_http_request_duration_seconds_sum**

**توضیح**: این معیار مجموع تمام زمان‌های پاسخ درخواست‌های HTTP را نشان می‌دهد. به عبارت دیگر، این مقدار نشان‌دهنده کل زمان صرف شده برای پاسخ به درخواست‌ها است، در واحد ثانیه. این داده‌ها می‌توانند برای محاسبه میانگین زمان پاسخ استفاده شوند، زمانی که با تعداد کل درخواست‌ها (که از پسوند `_count` به دست می‌آید) تقسیم شود.

**مثال**: اگر مجموع زمان‌های پاسخ برای 100 درخواست 200 ثانیه باشد، مقدار این metric `grafana_http_request_duration_seconds_sum` برابر با 200 خواهد بود.

**۲. grafana_http_request_duration_seconds_count**

**توضیح**: این معیار تعداد کل درخواست‌هایی که زمان پاسخ‌دهی برای آن‌ها اندازه‌گیری شده است را نشان می‌دهد. این مقدار برای محاسبه میانگین زمان پاسخ مورد استفاده قرار می‌گیرد و می‌تواند برای درک تعداد نمونه‌های موجود در داده‌ها مفید باشد.

**مثال**: اگر 100 درخواست مورد پردازش قرار گرفته باشند، مقدار `grafana_http_request_duration_seconds_count` برابر با 100 خواهد بود.

**۳. grafana_http_request_duration_seconds_bucket**

**توضیح**: این معیار تعداد درخواست‌هایی که در هر سطل (bucket) از مقادیر زمان پاسخ قرار دارند را نشان می‌دهد. هر bucket یک حد بالایی مشخص دارد (برچسب `le` مانند "le=0.1" برای 0.1 ثانیه)، و این معیار شمارش می‌کند که چند درخواست در هر bucket قرار گرفته‌اند. این داده‌ها برای درک توزیع زمان‌های پاسخ درخواست‌ها استفاده می‌شود.

**مثال**: اگر 50 درخواست زمان پاسخ کمتر از 0.1 ثانیه داشته باشند، مقدار `grafana_http_request_duration_seconds_bucket{le="0.1"}` برابر با 50 خواهد بود.

##### کاربرد count و sum در تجزیه و تحلیل

با استفاده از مقادیر `_count` و `_sum`، می‌توان متوسط زمان پاسخ به هر درخواست را محاسبه کرد. به عنوان مثال، اگر تعداد کل درخواست‌ها (count) 100 باشد و مجموع زمان‌های پاسخ (sum) 50 ثانیه باشد، میانگین زمان پاسخ به هر درخواست برابر با 0.5 ثانیه است.
از این قابلیت می‌توان استفاده کرد تا بررسی شود که یک API میانگین زمان پاسخ به هر درخواست اش چقدر است.

```PromQL
grafana_http_request_duration_seconds_count{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", method="GET", status_code="200"} 39

grafana_http_request_duration_seconds_sum{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", method="GET", status_code="200"} 0.7952658450000002

grafana_http_request_duration_seconds_bucket{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", le="0.005", method="GET", status_code="200"} 0

grafana_http_request_duration_seconds_bucket{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", le="0.01", method="GET", status_code="200"} 2

grafana_http_request_duration_seconds_bucket{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", le="0.025", method="GET", status_code="200"} 36

grafana_http_request_duration_seconds_bucket{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", le="25.0", method="GET", status_code="200"} 39

grafana_http_request_duration_seconds_bucket{handler="/login", instance="monitor.mojtel.ir:80", job="grafana", le="+Inf", method="GET", status_code="200"} 39
```
![[Historgram-Response-Time.webp]]
**توجه**: histogram در ذخیره‌سازی و پهنای باند بیشتری مصرف می‌کنند، زیرا هر نمونه فقط یک عدد ساده نیست بلکه چند نمونه است.

---
#Summary
 برای نمایش توزیع داده‌هایی که بر اساس quantile ها تجزیه و تحلیل می‌شوند، استفاده می‌شوند. Summary ها اجازه می‌دهند تا نه تنها تعداد و مجموع مقادیر را بدانیم، بلکه همچنین توزیع آماری داده‌ها را بر اساس quantile های تعریف‌شده نیز ببینیم. quantile ها نقاط معینی در توزیع داده‌ها هستند که می‌توانند برای تعیین مانند میانه یا درصدهای خاصی مانند ۹۰ درصد بالاترین زمان‌ها استفاده شوند.

##### اجزای یک خلاصه در Prometheus

1. **count**
	1. مشابه هیستوگرام، تعداد کل مواردی که مشاهده شده‌اند.
2. **sum**
	1. مجموع تمام مقادیر اندازه‌گیری‌ها.
3. **quantile**  
	1.  کوانتیل هایی که توزیع داده‌ها را بر اساس آستانه‌های مشخص نشان می‌دهند، مانند 50مین quantile (میانه)، 90مین quantile و غیره.

##### مثال: تجزیه و تحلیل زمان پاسخ سرور

فرض کنید که ما یک سرور وب داریم و می‌خواهیم توزیع زمان پاسخ به درخواست‌های HTTP را اندازه‌گیری کنیم. ما می‌خواهیم نه تنها میانگین، بلکه توزیع پاسخ‌ها را در کوانتیل‌های مختلف ببینیم تا درک بهتری از تجربه کاربری داشته باشیم.

##### متریک‌های Summary در Prometheus:

- **http_request_duration_seconds_count**: تعداد کل درخواست‌هایی که اندازه‌گیری شده‌اند.
- **http_request_duration_seconds_sum**: مجموع تمام زمان‌های پاسخ درخواست‌ها.
- **http_request_duration_seconds{quantile="0.5"}**: میانه زمان پاسخ‌ها (یعنی ۵۰مین کوانتیل).
- **http_request_duration_seconds{quantile="0.9"}**: زمان پاسخ برای ۹۰مین کوانتیل.
- **http_request_duration_seconds{quantile="0.99"}**: زمان پاسخ برای ۹۹مین کوانتیل.

##### سناریوی عملی:

فرض کنید که طی یک ساعت گذشته، سرور شما ۱۰۰۰ درخواست HTTP دریافت کرده است. زمان‌های پاسخ این درخواست‌ها ثبت شده‌اند و در زیر نمونه‌ای از داده‌هایی که می‌توان با استفاده از خلاصه در Prometheus دید را بیان می‌کنیم:

- **http_request_duration_seconds_count**: 1000
- **http_request_duration_seconds_sum**: 850 ثانیه
- **http_request_duration_seconds{quantile="0.5"}**: 0.8 ثانیه
- **http_request_duration_seconds{quantile="0.9"}**: 1.5 ثانیه
- **http_request_duration_seconds{quantile="0.99"}**: 2.0 ثانیه

##### تفسیر داده‌ها:

- **تعداد کل درخواست‌ها (count)**: ۱۰۰۰ درخواست در ساعت گذشته پردازش شده‌اند.
- **مجموع زمان‌های پاسخ (sum)**: کل زمان پاسخ‌دهی برابر با ۸۵۰ ثانیه بوده است.
- **میانه زمان پاسخ (0.5 quantile)**: نیمی از درخواست‌ها در کمتر از ۰.۸ ثانیه پاسخ داده شده‌اند.
- **زمان پاسخ برای ۹۰٪ درخواست‌ها (0.9 quantile)**: ۹۰٪ درخواست‌ها کمتر از ۱.۵ ثانیه پاسخ داده شده‌اند.
- **زمان پاسخ برای ۹۹٪ درخواست‌ها (0.99 quantile)**: ۹۹٪ درخواست‌ها کمتر از ۲ ثانیه پاسخ داده شده‌اند.

این اطلاعات به مدیران سیستم کمک می‌کند تا درک بهتری از عملکرد سرور در موقعیت‌های مختلف داشته باشند و بتوانند نقاط ضعف عملکردی را شناسایی و رفع کنند، به خصوص در مواقعی که زمان پاسخ بسیار بالا می‌رود.

```PromQL
# HELP http_request_duration_seconds Api requests response time in seconds
# TYPE http_request_duration_seconds summary
http_request_duration_seconds_sum{api="add_product" instance="host1.domain.com"} 8953.332
http_request_duration_seconds_count{api="add_product" instance="host1.domain.com"} 27892
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="0"}
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="0.5"} 0.232227334
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="0.90"} 0.821139321
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="0.95"} 1.528948804
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="0.99"} 2.829188272
http_request_duration_seconds{api="add_product" instance="host1.domain.com" quantile="1"} 34.283829292
```

از این داده‌ها، درک کرد که بیشتر صفحات چقدر سریع بارگذاری می‌شوند و آیا بخشی از صفحات بسیار کندتر از بقیه بارگذاری می‌شوند.

جدول زیر مزایا و معایب Histogram ها و Summary ها را خلاصه می کند.

![[histogram-summary-prometheus-timescale.png]]