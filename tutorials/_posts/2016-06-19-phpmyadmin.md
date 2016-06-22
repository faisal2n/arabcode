---
layout: post
date: 2016-06-18
title: إدارة قواعد البيانات باستخدام phpMyAdmin
type: tutorial
---





[phpMyAdmin](http://phpmyadmin.net/) هو تطبيق إنترنت مجاني يتيح لك إدارة قواعد البيانات بطريقة سهلة



# الوصول لـ phpMyAdmin



## من خلال لوحة التحكم ﻷصحاب المواقع :


1. قم بتسجيل الدخول للوحة التحكم


2. اضغط على   phpMyAdmin


3. اضغط على Connect to database بجوار قاعدة البيانات المراد إدارتها


## أو يمكنك  تنزيله من الموقع الرسمي وتنصيبه على السيرفر المحلي .


عند الفتح ستظهر شاشة تُظهر لك جميع الجداول الموجودة ضمن قاعدة البيانات المختارة ، إذا كان لديك عدة سكريبتات تستخدم نفس قاعدة البيانات ، فكل واحدة سيظهر بادئته الخاصة في أسمار الجداول . مثل `forum_` , `phpbb_`, `wp_` وما إلى ذلك .



# الوظائف



القوائم في أعلى البرنامج تتيح لك القيام بالعديد من الوظائف والعمليات على قاعدة البيانات ..


* `Structure` تعرض جميع الجداول الحالية

* `SQL` تتيح لك تنفيذ أوامر sql مباشرة

* `Search` تتيح لك البحث في جداول قاعدة البيانات

* `Query` تتيح لك إنشاء أوامر معقدة للتنفيذ على قاعدة البيانات

* `Export` تتيح لك تصدير نسخة احتياطية لقاعدة البيانات

* `Import` تتيح لك استيراد نسخ احتياطية أو ملفات sql أخرى

* `Operations` تتيح لك إنشاء جداول جديدو بسهولة ، والمزيد


إذا أدرت فحص جدول ستجد قائمة منسدلة أسفل الجدول تحتوي على خيارات تتيح لك القيام بعدد من المهمات


* `Empty` تتيح لك حذف جميع البيانات ضمن الجدول المحدد

* `Drop` تتيح لك الحذف النهائي للجدول المحدد

* `Print View` يقوم بإنشاء دليل مرجعي

* `Check` يبحث عن وجود أية أخطاء في الأداء ضمن الجداول

* `Optimize` يقوم اختبار أداء ويتأكد من أن البيانات مهيئة بشكل صحيح

* `Repair` يبحث عن الأخطاء ويصلحها إن وجدت

* `Analyze` يجمع معلومات جول الجدول ، يتأكد من هيكله ويحدد المعلومات


# عرض جدول



عند فتح جدول ما ستتمكن من مشاهدة الحقول التي يحويها ، بضغطك على المربع بجوار أحد صفوف الجدول ستتمكن من القيام بالعمليات عليه كتحريره والمزيد من الأيقونات في الأسفل ..


# لمزيد من المعلومات ..


هذه مقالة مختصرة جداً تغطي أساسيات phpMyAdmin ، إذا أردت المزيد من المعلومات والتعلم أكثر يمكنك قراءة الوثائق التالية (بالإنكليزي)
<http://wiki.phpmyadmin.net/pma/Articles#English>

> هل يهمك هذا الموضوع وتريد قراءة المزيد بالعربية؟ إن لم تجد ما يكفيك من المصادر العربية حول هذا الموضوع فيمكنك إرسال [طلب ترجمة](/about/request) لي لكي أترجم لك باقي الدروس مجاناً!

> تنويه:
> 
> التعليمات والشروحات الموجودة في مواقع أخرى قد لا تكون كاملة أو دقيقة أو قابلة للتنفيذ .. الاعتماد على شرح من موقع خارجي قد يكون خطر ويتم على مسؤوليتك الخاصة ..