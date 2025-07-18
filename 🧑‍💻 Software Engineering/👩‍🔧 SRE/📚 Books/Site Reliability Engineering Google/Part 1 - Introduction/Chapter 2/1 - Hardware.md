**دیتاسنترهای گوگل چه تفاوتی دارند؟** دیتاسنترهای گوگل با دیتاسنترهای معمولی (مثل آن‌هایی که شرکت‌ها اجاره می‌کنند) فرق دارند، چون گوگل خودش همه‌چیز را طراحی کرده: از سیستم برق و خنک‌کننده تا شبکه و سخت‌افزار. این طراحی خاص باعث می‌شود هم چالش‌های جدید و هم فرصت‌های بهتری داشته باشند.

**سخت‌افزار و اصطلاحات:**

- گوگل از کلمه‌های خاصی برای توضیح اجزای سیستمش استفاده می‌کند تا جلوی سردرگمی را بگیرد:
- **ماشین (Machine**): منظور سخت‌افزار است، مثل یک سرور فیزیکی یا یک ماشین مجازی (VM).
- **سرور (Server**): منظور نرم‌افزار است، یعنی برنامه‌ای که کاری انجام می‌دهد (مثل نرم‌افزار ایمیل یا وب‌سایت).
- برخلاف جاهای دیگر که ممکن است یک سرور خاص فقط برای یک کار (مثل ایمیل) استفاده شود، در گوگل هر machine می‌تواند هر server (نرم‌افزار) را اجرا کند. این کار توسط یک سیستم به نام **Borg** مدیریت می‌شود که مثل یک مدیر منابع عمل می‌کند و تصمیم می‌گیرد کدام نرم‌افزار روی کدام سخت‌افزار اجرا شود.

**چرا این اصطلاحات مهم‌اند؟** در جاهای دیگر، کلمه "server" هم برای سخت‌افزار و هم برای نرم‌افزار استفاده می‌شود که باعث گیج شدن می‌شود. گوگل با جدا کردن این دو مفهوم (machine برای سخت‌افزار و server برای نرم‌افزار) کار را واضح‌تر کرده است.

**ساختار دیتاسنتر گوگل:** دیتاسنترهای گوگل مثل یک شهر سازمان‌دهی شده‌اند:

- **Rack**: تعدادی machine (سخت‌افزار) داخل یک قفسه (rack) قرار می‌گیرند، مثل کمدهایی پر از کامپیوتر.
- **Row**: چند rack کنار هم یک ردیف (row) تشکیل می‌دهند.
- **Cluster**: چند row کنار هم یک cluster می‌سازند، مثل یک گروه بزرگ از ماشین‌ها.
- **Datacenter Building**: چند cluster در یک ساختمان دیتاسنتر قرار دارند.
- **Campus**: چند ساختمان دیتاسنتر نزدیک به هم یک campus را تشکیل می‌دهند، مثل یک شهرک فناوری.

![[datacenter-campus.jpg]]

**مثال ساده:** فرض کنید دیتاسنتر گوگل مثل یک کتابخانه بزرگ است:

- هر کتاب (machine) یک کامپیوتر است.
- قفسه‌های کتاب (rack) چند کامپیوتر را کنار هم نگه می‌دارند.
- ردیف قفسه‌ها (row) کنار هم قرار دارند.
- چند ردیف قفسه یک بخش بزرگ (cluster) می‌سازند.
- چند بخش در یک ساختمان (datacenter) هستند.
- چند ساختمان نزدیک هم یک پردیس (campus) تشکیل می‌دهند.

**چرا این مهم است؟** این ساختار و اصطلاحات به گوگل کمک می‌کند منابعش را بهتر مدیریت کند. به جای اختصاص دادن یک ماشین به یک کار خاص، Borg مثل یک مدیر باهوش منابع را بین نرم‌افزارها تقسیم می‌کند تا همه‌چیز سریع و کارآمد باشد.