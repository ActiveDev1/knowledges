**مانیتورینگ سیاه‌جعبه در برابر سفید‌جعبه**

ما از **مانیتورینگ سفید‌جعبه** به‌طور گسترده و از **مانیتورینگ سیاه‌جعبه** به‌صورت محدود اما حیاتی استفاده می‌کنیم.

- **مانیتورینگ سیاه‌جعبه**:
  - **ماهیت**: متمرکز بر **علائم** است و مشکلات فعال و جاری (نه پیش‌بینی‌شده) را نشان می‌دهد: «سیستم هم‌اکنون درست کار نمی‌کند.»
  - **ویژگی**: رفتار سیستم را از بیرون، مانند تجربه کاربر، بررسی می‌کند.
  - **کاربرد**: برای **پیج کردن** انسان‌ها مناسب است، زیرا فقط زمانی هشدار می‌دهد که مشکل واقعی و در حال وقوع باشد و به علائم قابل‌مشاهده منجر شود.
  - **محدودیت**: برای مشکلات قریب‌الوقوع (اما هنوز رخ‌نداده) تقریباً بی‌فایده است.

- **مانیتورینگ سفید‌جعبه**:
  - **ماهیت**: به بررسی اجزای داخلی سیستم (مانند لاگ‌ها یا endpointهای HTTP) با استفاده از ابزارسازی وابسته است.
  - **ویژگی**: امکان تشخیص مشکلات قریب‌الوقوع، خرابی‌های مخفی‌شده توسط تلاش‌های مجدد (retries)، و غیره را فراهم می‌کند.
  - **کاربرد**: برای **دیباگینگ** ضروری است، زیرا اطلاعات دقیقی از عملکرد داخلی سیستم ارائه می‌دهد.
  - **دوگانه بودن**: بسته به سطح اطلاعات، می‌تواند هم **علائم‌محور** باشد و هم **علت‌محور**. مثلاً:
    - برای SRE پایگاه داده، کندی خواندن داده‌ها یک **علائم** است.
	- برای SRE فرانت‌اند که وب‌سایت کند را مشاهده می‌کند، همان کندی پایگاه داده یک **علت** است.

### مثال:
اگر وب‌سرورها برای درخواست‌های سنگین از پایگاه داده کند باشند، مانیتورینگ سفید‌جعبه به شما کمک می‌کند تا:
- درک کنید وب‌سرور پایگاه داده را چقدر کند می‌بیند.
- سرعت واقعی پایگاه داده را بررسی کنید.
این اطلاعات برای تمایز بین کندی واقعی پایگاه داده و مشکلات شبکه بین وب‌سرور و پایگاه داده حیاتی است.

### تفاوت در پیج کردن:
- **سیاه‌جعبه**: با اطمینان از اینکه فقط مشکلات واقعی و جاری باعث پیج می‌شوند، انضباط را حفظ می‌کند.
- **سفید‌جعبه**: برای شناسایی مشکلات قریب‌الوقوع مناسب است، اما ممکن است نویز بیشتری ایجاد کند اگر به‌درستی تنظیم نشود.