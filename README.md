# Stock

نظام إدارة المخزون والأصول مبني على نسخة منفصلة من GLPI، ويهدف إلى إدارة الأصناف والمشتريات والموردين وتسليم الأصول وتتبع حركة المخزون.

## المزايا

- إدارة الأصول ومواقعها وحالاتها
- إدارة الأصناف والمكونات وحركات المخزون
- إدارة المشتريات والموردين والطلبات
- تتبع التكاليف والضمانات والعمر التشغيلي للأصول
- واجهة إدارة عربية قابلة للتخصيص
- تشغيل سريع على Windows دون Docker

## التقنيات

- PHP 8.3 أو أحدث
- Apache 2.4
- MySQL 8.x
- Composer
- GLPI 11
- Twig وSymfony
- Vue 3 وJavaScript وBootstrap/Tabler

## التشغيل على Windows باستخدام Laragon

1. ثبّت Laragon وحدد Apache وMySQL وPHP 8.3 أو أحدث.
2. ضع المشروع داخل مجلد Laragon أو شغله مباشرة من مجلد `stockes`.
3. أنشئ قاعدة بيانات باسم `glpi` بترميز UTF-8.
4. أنشئ ملف `config/config_db.php` بالمعلومات التالية، أو عدّل الملف الحالي:

```php
<?php
class DB extends DBmysql {
   public $dbhost = '127.0.0.1:3306';
   public $dbuser = 'root';
   public $dbpassword = '';
   public $dbdefault = 'glpi';
   public $use_timezones = true;
   public $use_utf8mb4 = true;
   public $allow_datetime = false;
   public $allow_signed_keys = false;
}
```

5. ثبّت المكتبات:

```powershell
composer install
```

6. شغل Apache وMySQL من Laragon، ثم افتح المشروع عبر Virtual Host أو المنفذ المخصص.

مثال للتشغيل المحلي:

```text
http://127.0.0.1:8082
```

## إعداد قاعدة البيانات

لا يتم رفع قاعدة البيانات داخل المستودع ولا يجب رفع dump يحتوي بيانات حقيقية أو حسابات مستخدمين.

استورد نسخة قاعدة البيانات المحلية فقط في بيئة العمل الداخلية، ثم حدّث بيانات اتصال قاعدة البيانات في `config/config_db.php`.

## حسابات الدخول

لا توجد بيانات دخول افتراضية محفوظة داخل مستودع المشروع. أنشئ حساب مدير جديد من تثبيت GLPI، أو استخدم حسابك المحلي السابق، مع تغيير كلمة المرور قبل تشغيل المشروع في بيئة حقيقية.

## Docker

Docker اختياري للمشروع ويمكن تشغيله بالكامل مباشرة عبر Laragon وApache وPHP وMySQL على Windows للحصول على استجابة أسرع واستهلاك أقل للموارد.

## الملفات المستبعدة من Git

يجب عدم رفع الملفات التالية:

- `vendor`
- `node_modules`
- `config/config_db.php`
- ملفات قاعدة البيانات وSQL dumps
- ملفات السجل والملفات المؤقتة داخل `files`
- إعدادات IDE والبيئة المحلية

## المستودع

https://github.com/Mhmdzakariaj/stock
