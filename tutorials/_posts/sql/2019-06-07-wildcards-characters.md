---
permalink: /sql/wildcard_characters
layout: post
date: 2018-05-12
title: سلسلة دروس SQL| الرموز البديلة
type: tutorial
hidden: true
comments: true
---

{% include sql-content.html %}

* Toc
{:toc}

<style>

table {
  direction: ltr;
}
</style>


# الرموز البديلة في Sql

يُقصد بالرمز البديل (بالإنجليزية wildcard characters) الذي ينوب عن الأحرف. وتُستخدم لاستبدال حرف أو أكثر في عبارة نصيّة

تُستخدم الرموز البديلة مع عامل LIKE والتي تستخدم مع عبارة where للبحث عن نمط معين في عمود ما.

# الرموز البديلة في ميكروسوفت أكسس

الرمز|    الوصف | مثال
----|-----|------

*|    تُمثِّل عدد حروف صفر أو أكثر|    العبارة `bl*` تجد الكلمات bl و  black و  blue, و blob
?|    تمثل حرفا واحدا |     العبارة h?t تجد hot, hat, و hit
[] |    تمثل أي حرف ضمن الأقواس    العبارة h[oa]t  تجد hot و hat, لكن ليس hit
! |    تمثل أي حرف عدا الذي ضمن الأقواس     h[!oa]t تجد hit, لكن ليس  hot و hat
- |    تمثل مجال من الأحرف بحسب الترتيب الألفبائي    c[a-b]t  تجد cat و cbt
# |    تمثل أي رقما واحدا    2#5 تجد 205, 215, 225, 235, 245, 255, 265, 275, 285, و 295


# الرموز البديلة في SQL Server

الرمز|    الوصف | مثال
----|-----|------
%|    تُمثِّل عدد حروف صفر أو أكثر|    العبارة bl% تجد الكلمات bl و  black و  blue, و blob
_|     تمثل حرفا واحدا |     العبارة h_t تجد hot, hat, و hit
[] |    تمثل أي حرف ضمن الأقواس    العبارة h[oa]t  تجد hot و hat, لكن ليس hit
^ |    تمثل أي حرف عدا الذي ضمن الأقواس     h[^oa]t تجد hit, لكن ليس  hot و hat
- |    تمثل مجال من الأحرف بحسب الترتيب الألفبائي    c[a-b]t  تجد cat و cbt

جميع الرموز يمكن أن تُستخدم سويةً مع بضعها البعض في نفس العبارة!

فيما يلي بعض الأمثلة التي تُظهر عوامل LIKE مختلفة مع الرموز % و _ :

عبارة تحوي عامل LIKE | الوصف
------|--------
WHERE CustomerName LIKE 'a%'| تجد أي قيمة تبدأ بـ a
WHERE CustomerName LIKE '%a' | تجد أي قيمة تنتهي بـ a
WHERE CustomerName LIKE '%or%' | تجد أي قيمة تحوي العبارة or في أي موضع
WHERE CustomerName LIKE '_r%' | تجد أي قيمة تحوي الحرف r في الموقع الثاني (ثاني حرف)
WHERE CustomerName LIKE 'a_%_%' | تجد أي قيمة تبدأ بـ a وطول القيمة على الأقل ثلاثة (مؤلفة من ثلاث أحرف على الأقل أولها a)
WHERE ContactName LIKE 'a%o' | تجد أي قيمة تبدأ بـ a وتنتهي بـ o

# استعراض قاعدة  بيانات


# استخدام الرمز %

عبارة SQL التالية تحدد كل الزبائن بحيث تكون القيمة الخاصة بهم في العمود city تبدأ بـ ber

SELECT * FROM Customers
WHERE City LIKE 'ber%';

كذلك عبارة SQL التالية تحدد كل الزبائن بحيث تكون القيمة الخاصة بهم في العمود city تحوي es

SELECT * FROM Customers
WHERE City LIKE '%es%';

# استخدام الرمز _


والعبارة التالية تحدد كل الزبائن بحيث تبدأ القيمة الخاصة بهم في العمود city بأي حرف متبوعاً بـ ondon

SELECT * FROM Customers
WHERE City LIKE '_ondon';

والعبارة التالية تحدد كل الزبائن بحيث تبدأ القيمة الخاصة بهم في العمود city بالحرف L متبوعا بأي حرف، متبوعا بـ n، متبوعا بأي حرف، متبوعا بـ on

SELECT * FROM Customers
WHERE City LIKE 'L_n_on';

# استخدام رمز القائمة [ ]

عبارة SQL التالية تحدد كل الزبائن بحيث تكون القيمة الخاصة بهم في العمود city تبدأ بـأحد الأحرف b أو s أو p

SELECT * FROM Customers
WHERE City LIKE '[bsp]%';

عبارة SQL التالية تحدد كل الزبائن بحيث تكون القيمة الخاصة بهم في العمود city تبدأ بـ a أو b أو c

SELECT * FROM Customers
WHERE City LIKE '[a-c]%';

# استخدام الرمز [ !]


عبارة SQL التالية تحدد كل الزبائن بحيث تكون القيمة الخاصة بهم في العمود city **لا** تبدأ بـأحد الأحرف b أو s أو p

SELECT * FROM Customers
WHERE City LIKE '[!bsp]%';

أو لنفس الغرض يمكن كتابة:

SELECT * FROM Customers
WHERE City NOT LIKE '[bsp]%';
