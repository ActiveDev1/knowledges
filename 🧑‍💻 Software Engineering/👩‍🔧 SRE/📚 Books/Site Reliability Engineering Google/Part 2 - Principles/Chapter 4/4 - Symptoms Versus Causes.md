**علائم در برابر علل**

سیستم مانیتورینگ شما باید به دو سؤال پاسخ دهد: **چه چیزی خراب است؟** و **چرا؟**  
- **چه چیزی خراب است؟** نشان‌دهنده **علائم** (symptom) است.  
- **چرا؟** نشان‌دهنده **علت** (cause) است که ممکن است یک علت میانی باشد.  

جدول زیر (جدول 6-1) نمونه‌هایی از علائم و علل مربوطه را نشان می‌دهد:

**جدول 6-1. نمونه‌های علائم و علل**

| علائم                                                 | علت                                                                                                                                  |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| در حال ارائه HTTP 500 یا 404 هستم                     | سرورهای پایگاه داده از پذیرش اتصال‌ها امتناع می‌کنند                                                                                 |
| پاسخ‌ها کند هستند                                     | پردازنده‌ها به دلیل یک الگوریتم bogosort بیش‌ازحد بارگذاری شده‌اند یا کابل اترنت زیر یک رک فشرده شده و باعث افت جزئی بسته‌ها شده است |
| کاربران در قطب جنوب GIFهای متحرک گربه دریافت نمی‌کنند | شبکه توزیع محتوا (CDN) از دانشمندان و گربه‌ها متنفر است و برخی IPهای کلاینت را بلک‌لیست کرده است                                     |
| محتوای خصوصی برای همه قابل خواندن است                 | یک push نرم‌افزاری جدید باعث فراموشی ACLها شده و همه درخواست‌ها را مجاز کرده است                                                     |

### اهمیت تمایز "چه" و "چرا"
تمایز بین **"چه چیزی"** (علائم) و **"چرا"** (علل) یکی از مهم‌ترین اصول در ایجاد مانیتورینگ مؤثر با **حداکثر سیگنال** و **حداقل نویز** است. تمرکز بر این تمایز به شناسایی سریع مشکلات و علل ریشه‌ای آن‌ها کمک می‌کند.


--------------------------
**ACLs چیست؟**

مخفف **Access Control Lists** (لیست‌های کنترل دسترسی) است. این اصطلاح در حوزه فناوری اطلاعات و سیستم‌های کامپیوتری به فهرستی از قوانین یا مجوزها اشاره دارد که تعیین می‌کند چه کاربران یا فرآیندهایی می‌توانند به منابع خاصی (مانند فایل‌ها، دایرکتوری‌ها، یا سرویس‌ها) دسترسی داشته باشند و چه نوع عملیاتی (مثل خواندن، نوشتن، یا اجرا) مجاز است.