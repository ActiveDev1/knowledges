**تعریف Toil**

 صرفاً "کاری که دوست ندارم انجام دهم" نیست و معادل کارهای اداری یا کارهای سخت و کثیف هم نیست. ترجیحات افراد برای کارهای لذت‌بخش متفاوت است و برخی حتی از کارهای دستی و تکراری لذت می‌برند. همچنین، کارهای اداری ضروری (مثل جلسات تیمی، تنظیم و ارزیابی اهداف، **snippets**، یا کاغذبازی‌های HR) به‌عنوان **overhead** شناخته می‌شوند، نه **toil**. کارهای سخت (grungy) که ارزش بلندمدت دارند نیز **toil** نیستند؛ مثلاً تمیز کردن پیکربندی **alerting** یک سرویس و حذف شلوغی‌ها ممکن است سخت باشد، اما **toil** نیست.

### پس Toil چیست؟
**Toil** کاری است که به اجرای یک سرویس **production** مرتبط است و معمولاً:
- **دستی** (manual)
- **تکراری** (repetitive)
- **قابل اتوماسیون** (automatable)
- **تاکتیکی** (tactical)
- **بدون ارزش پایدار** (devoid of enduring value)
- **متناسب با رشد سرویس به‌صورت خطی افزایش می‌یابد** (scales linearly with service growth)

هرچند هر کار **toil** لزوماً همه این ویژگی‌ها را ندارد، اما هرچه بیشتر با این توصیفات مطابقت داشته باشد، احتمال **toil** بودن آن بیشتر است:

- **دستی (Manual)**: شامل کارهایی مثل اجرای دستی اسکریپتی که برخی وظایف را خودکار می‌کند. هرچند اجرای اسکریپت سریع‌تر از انجام دستی مراحل آن باشد، زمان صرف‌شده توسط انسان برای اجرای آن همچنان **toil** است.
- **تکراری (Repetitive)**: اگر کاری را برای اولین یا دومین بار انجام می‌دهید، **toil** نیست. **Toil** کاری است که بارها و بارها تکرار می‌شود. حل یک مشکل جدید یا ابداع راه‌حل جدید **toil** نیست.
- **قابل اتوماسیون (Automatable)**: اگر ماشین بتواند کار را به‌خوبی انسان انجام دهد یا نیاز به کار قابل حذف باشد، آن کار **toil** است. اگر قضاوت انسانی برای کار ضروری باشد، احتمالاً **toil** نیست.
- **تاکتیکی (Tactical)**: **Toil** واکنشی و ناشی از وقفه‌هاست، نه استراتژیک و پیش‌فعال. مدیریت **pager alerts** نمونه‌ای از **toil** است. هرچند ممکن است نتوان این نوع کار را کاملاً حذف کرد، باید به‌طور مداوم برای کاهش آن تلاش کرد.
- **بدون ارزش پایدار (No Enduring Value)**: اگر پس از انجام کار، سرویس در همان حالت قبلی باقی بماند، احتمالاً کار **toil** بوده است. اما اگر کار به بهبود دائمی سرویس منجر شود (حتی با مقداری کار سخت مثل مرتب کردن کدهای قدیمی)، احتمالاً **toil** نیست.
- **متناسب با رشد خطی (O(n) with Service Growth)**: اگر حجم کار با افزایش اندازه سرویس، ترافیک، یا تعداد کاربران به‌صورت خطی رشد کند، احتمالاً **toil** است. یک سرویس ایده‌آل و خوب طراحی‌شده باید حداقل یک مرتبه بزرگ‌تر شود بدون نیاز به کار اضافی، جز برخی تلاش‌های یک‌بار مصرف برای افزودن منابع.
---------------------

**تاکتیکی** به این معناست که کار به‌صورت **واکنشی** (reactive) و در پاسخ به یک مشکل یا وقفه (مثل هشدار یا alert) انجام می‌شود، نه به‌صورت **پیش‌فعال** (proactive) یا برنامه‌ریزی‌شده برای دستیابی به یک استراتژی بلندمدت. به عبارت دیگر، **toil** کاری است که به دلیل یک نیاز فوری یا مشکل ناگهانی انجام می‌شود و معمولاً به حل مسائل لحظه‌ای می‌پردازد، نه بهبود دائمی سیستم.

#### ویژگی‌های کار تاکتیکی:

- **وقفه‌محور**: معمولاً به دلیل دریافت هشدار (مثل **pager alert**) یا گزارش یک مشکل فوری انجام می‌شود.
- **موقتی**: تمرکز روی رفع سریع مشکل است، نه پیشگیری از آن در آینده.
- **تکراری و بدون پیشرفت استراتژیک**: این کارها معمولاً بارها تکرار می‌شوند و به بهبود زیرساخت یا سرویس به‌صورت پایدار کمک نمی‌کنند.

#### مثال‌:
**مدیریت Pager Alerts**:
    - فرض کنید سرویسی به دلیل پر شدن دیسک سرور از کار می‌افتد و یک **alert** برای تیم SRE ارسال می‌شود. مهندس SRE وارد سیستم می‌شود، فایل‌های غیرضروری را حذف می‌کند یا دیسک را ارتقا می‌دهد تا مشکل حل شود. این کار **تاکتیکی** است، چون:
        - واکنشی است (در پاسخ به هشدار).
        - موقتاً مشکل را حل می‌کند، اما ممکن است دوباره رخ دهد.
        - اگر این کار به‌صورت دستی و مکرر انجام شود، **toil** محسوب می‌شود.
    - **حل غیرتاکتیکی**: طراحی سیستمی که به‌صورت خودکار فضای دیسک را مدیریت کند یا هشدارهای پیشگیرانه قبل از پر شدن دیسک ارسال کند.