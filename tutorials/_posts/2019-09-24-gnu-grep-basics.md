---
layout: post
date: 2019-09-24
title: أساسيات جنو grep للمبتدئين
type: tutorial
comments: true
---


تعد Grep واحدة من مجموعة أدوات "Swiss Army knife" الخاصة بإدارة النظام ، وهي مفيدة للغاية للبحث عن السلاسل والأنماط في مجموعة من الملفات ، أو حتى المجلدات الفرعية. يقدم هذا المقال أساسيات Grep ، ويقدم أمثلة على الاستخدام المتقدم ويربطك بمزيد من الصفحات المتعلقة بهذا الموضوع.

يتم تثبيت Grep (وهو اختصار لـ "Global Regular Expression Print") افتراضيًا على كل توزيعة ﻷنظمة Linux و BSD و UNIX ، وهو متاح أيضًا لنظام Windows. تقوم GNU ومؤسسة البرمجيات الحرة بتوزيع Grep كجزء من مجموعة أدوات المصادر المفتوحة. يركِّز هذا البرنامج التعليمي في المقام الأول على إصدار جنو هذا ، لأنه الأكثر استخدامًا حاليًا.

يجد Grep سلسلة في ملف أو إدخال معين ، بسرعة وكفاءة. على الرغم من أن معظم الاستخدامات اليومية للأمر بسيطة ، إلا أن هناك مجموعة متنوعة من الاستخدامات الأكثر تقدّمًا والتي لا يعرفها معظم الأشخاص - بما في ذلك التعبيرات المعتادة وأكثر من ذلك ، والتي قد تصبح معقدة للغاية.

الأداة لها جذورها في بناء جملة التعبير العادية الموسعة التي تمت إضافتها إلى UNIX بعد تنفيذ التعبير العادي الأصلي من كين تومسون. يبحث الأخير عن أي قائمة من السلاسل الثابتة ، باستخدام خوارزمية Aho-Corasick. يتم تضمين هذه المتغيرات في معظم تطبيقات Grep الحديثة كمفاتيح تبديل لسطر الأوامر (وموحدة كـ -E و -F في POSIX.2). في مثل هذه التطبيقات المدمجة ، قد يتصرف Grep أيضًا بشكل مختلف اعتمادًا على الاسم الذي تم استدعاءه به ، مما يسمح لـ fGrep و eGrep و Grep بأن تكون روابط للبرنامج نفسه.

هناك طريقتان لتوفير المدخلات إلى Grep ، ولكل منها استخداماته الخاصة.
أولاً يمكن استخدام Grep للبحث في ملف أو ملفات معينة على نظام (بما في ذلك البحث المتكرر من خلال المجلدات الفرعية). يقبل Grep أيضًا المدخلات (عادةً عبر توجيه) من أمر أو سلسلة أوامر أخرى.

* Toc
{:toc}

# التعبيرات النمطية

تعبير نمطي (regular expression) ، غالبًا ما يتم اختصاره إلى "regex" أو "regexp" ، هو طريقة لتحديد نمط (مجموعة معينة من الأحرف أو الكلمات) في النص الذي يمكن تطبيقه على المدخلات المتغيرة للعثور على جميع التكرارات التي تتطابق مع النمط. تعمل Regexes على تعزيز القدرة على معالجة محتوى النص بشكل مفيد ، خاصةً عند دمجها مع أوامر أخرى.
عادة ، يتم تضمين التعبيرات النمطية في أمر Grep بالتنسيق التالي:

        grep [خيارات] [regexp] [اسم الملف]

يستخدم GNU Grep إصدار GNU من التعبيرات النمطية ، وهو مشابه جدًا (ولكن ليس مطابقًا) للتعبيرات المعتادة POSIX. في الواقع ، تتشابه معظم أنواع التعبيرات المعتادة تمامًا ، لكن لها اختلافات في حالات الهروب أو أحرف التعريف أو العوامل الخاصة.

يحتوي GNU Grep على مجموعتين من ميزات التعبير النمطي: Basic and Extended. في التعبيرات النمطية الأساسية ، تفقد الأحرف الوصفية ؟ و + و { و | و ( و ) معناها الخاص (الذي يرد وصف لاستخداماته لاحقًا في هذه المقالة). وكما هو مذكور أدناه ، للتبديل إلى استخدام التعبيرات النمطية الموسعة تحتاج إلى إضافة الخيار -E إلى الأمر grep.

من المعتاد إحاطة التعبير النمطي بعلامات اقتباس مفردة ، لمنع shell (مثل Bash أو غيرها) من محاولة تفسير التعبير وتوسيعه قبل بدء عملية grep. على سبيل المثال ، إذا لم يتم ذكر زوج من علامات التجزئة في إعادة الاسترداد ، فسوف ينتج عن ذلك النص بين علامات التجزئة التي يتم تنفيذها كعملية فرعية لـ Bash - وإذا حدث أن ذلك أمر صالح ، فالنص المُرجع سيأخذ مكان التعبير النمطي في تعليمة سطر الأوامر المعطاة إلى Grep! وهذا ليس ما نريد.

مرة أخرى ، نظرًا لسلوك shell ، يمكنك أيضًا تضمين regex في علامات تنصيص مزدوجة - في هذه الحالة ، يمكنك استخدام متغيرات البيئة في regex ، وستقوم shell باستبدالها قبل الاتصال بـ Grep. قد يكون هذا مفيدًا جدًا ، اعتمادًا على ما تحاول القيام به - أو قد يكون مصدر إزعاج. تذكر الفرق في السلوك.

# الاستخدام الأساسي

الآن دعنا ننتقل إلى بعض الأمثلة العملية لاستخدام Grep. لفهم النتائج بشكل أفضل ، قمت بإنشاء ملف نصي بسيط سنقوم بتشغيل عمليات البحث الخاصة به في Grep ؛ يحتوي الملف على الأسطر التالية:

        Hi 
        this 
        is test file 
        to carry out few regular expressions 
        practical with grep 
        123 456 
        Abcd
        ABCD

بحث غير حساس لحالة الأحرف (grep -i):

        [manish@clone ~]$ grep -i 'abcd' testfile 
        Abcd 
        ABCD

كما ترى ، تؤدي العلامة -i إلى البحث عن "abcd" لإرجاع المطابقات التي لها حالات مختلفة للأحرف.

البحث عن كلمة كاملة (grep -w):

        [manish@clone ~]$ grep -w 'test' testfile 
        is test file

هذا النوع من البحث يعرض فقط الأسطر التي تكون فيها السلسلة المطلوبة كلمة كاملة وليست جزءًا من كلمة أكبر.

البحث بشكل متكرر من خلال المجلدات الفرعية (grep -r <pattern> <path):

        [manish@clone ~]$ grep -r '456' /root/ 
        /root/testfile:Year is 2010

البحث العكسي (grep -v):

        [manish@clone ~]$ grep -v 'practical' testfile 
        Hi 
        this 
        is test file 
        to carry out few regular expressions 
        123 456 
        Abcd 
        ABCD

هذا يعطي جميع الأسطر في الملف ، باستثناء السطر الذي يحتوي على كلمة "practical".

من الاستخدامات المثير للاهتمام أيضا هو علامة -L (يمكنك أيضًا استخدام
 --files-without-match
) ، والتي تقوم بإخراج أسماء الملفات التي لا تحتوي على تطابقات لنمط البحث الخاص بك. لا تتم طباعة المطابقات الخاصة بنمط البحث الخاص بك، ولكن يتم طباعة الأسماء فقط.

        [manish@clone ~]$ grep -r -L "Network" /var/log/* 
        /var/log/anaconda.log 
        /var/log/anaconda.syslog 
        /var/log/audit/audit.log 
        /var/log/boot.log 
        /var/log/boot.log.1 
        ...

علامة "معاكسة" إلى -L هي -l أو - الملفات - مع التطابقات ، التي تطبع (فقط) أسماء الملفات التي تحتوي على مطابقات لنمط البحث الخاص بك.

طباعة أسطر سياق إضافية (زائدة) بعد المطابقة (grep -A <NUM>):

        [manish@clone ~]$ grep -A1 '123'  testfile
        123 456 
        Abcd

يطبع Grep السطر المطابق لكل سطر يطابق البحث، وكذلك السطر التالي بعد المطابقة. يؤدي تغيير الرقم المتاح إلى -A إلى تغيير عدد الأسطر الإضافية الموجودة في الإخراج.

قم بطباعة خطوط سياق (بادئة) إضافية قبل المطابقة (grep -B <NUM>):

        [manish@clone ~]$ grep -B2 'Abcd' testfile
        practical with grep 
        123 456 
        Abcd

طباعة أسطر سياق إضافية (بادئة وخلفية) قبل وبعد المطابقة (grep -C <NUM>):

        [manish@clone ~]$ grep -C2 'carry' testfile
        this
        is test file
        to carry out few regular expressions
        practical with grep
        123 456

كما ترى ، فقد طبع هذا سطرين قبل وبعد المطابقة الفردية الموجودة في الملف ؛ إذا كان هناك تطابقات متعددة ، يقوم Grep بإدراج سطر يحتوي على - بين كل مجموعة من الخطوط (كل تطابق وخطوط السياق الخاصة به).

اطبع اسم الملف لكل مطابقة (grep -H <pattern> filename):

        [manish@clone ~]$ grep -H 'a' testfile
        testfile:to carry out few regular expressions 
        testfile:practical with grep

الآن ، لنجري البحث بشكل مختلف قليلاً:

        [manish@clone ~]$ cat testfile | grep -H 'a' 
        (standard input):to carry out few regular expressions 
        (standard input):practical with grep

عندما يتم تمرير الدفق الذي يُطلب من Grep بحثه إلى مدخلاته القياسية عبر توجيه من أمر سابق في السلسلة ، يعرض grep -H (الإدخال القياسي) كاسم ملف.

التشغيل في الوضع "الصامت" (grep -q): عند التشغيل باستخدام هذه العلامة ، لا يكتب Grep أي شيء إلى الإخراج القياسي ، ولكنه يحدد قيمة الإرجاع (المعروفة أيضًا باسم حالة الخروج) لتعكس ما إذا كان قد تم العثور على تطابق أم لا. يستخدم هذا الخيار بشكل أساسي في البرامج النصية التي تحتاج إلى التحقق مما إذا كان الملف المحدد يحتوي على تطابق معين. تشير حالة الإرجاع 0 (صفر) إلى أنه تم العثور على تطابق ؛ 1 يشير إلى أنه لم يتم العثور على تطابق.

        [manish@clone ~]$ grep -q '2010' testfile 
        [manish@clone ~]$ echo $? 
        1
        [manish@clone ~]$ grep -q '456' testfile 
        [manish@clone ~]$ echo $? 
        0

# استخدام التعبيرات النمطية

        [manish@clone ~]$ grep 'c.r' testfile 
        to carry out few regular expressions

