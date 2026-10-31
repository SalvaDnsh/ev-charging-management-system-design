# نمودار مورد کاربرد فرایند مدیریت نشست شارژ

[فهرست گزارش‌ها](../../../INDEX.md)

# نمودار مورد کاربرد<sup><a href="#fn-1-64" id="fnref-1-64">1</a></sup> فرآیند مدیریت نشست شارژ

## ۱. مقدمه

این متن نمودار مورد کاربرد و تحلیل رفتاری مرتبط با آن را برای **سامانه مدیریت ایستگاه‌های شارژ (**CSMS<sup><a href="#fn-2-64" id="fnref-2-64">2</a></sup>**)** تشریح می‌کند. هدف از نمودار این است که با شناسایی بازیگران<sup><a href="#fn-3-64" id="fnref-3-64">3</a></sup> و کارکردهای اصلی<sup><a href="#fn-4-64" id="fnref-4-64">4</a></sup>، نمایی کلی از تعاملات و فرآیندهای سیستم ارائه شود.

## ۲. معرفی بازیگران

بازیگران، موجودیت‌هایی هستند که با سیستم تعامل دارند. این بازیگران به دو دسته انسانی و سیستمی تقسیم می‌شوند:

<div>

<div>

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th aria-sort="none" scope="col"><div>
&#10;</div></th>
<th aria-sort="none" scope="col"><div>
&#10;</div></th>
<th aria-sort="none" scope="col"><div>
&#10;</div></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>انسانی</strong></td>
<td>راننده<sup><a href="#fn-5-64" id="fnref-5-64">5</a></sup></td>
<td>درخواست شروع/پایان نشست شارژ از طریق اپلیکیشن.</td>
</tr>
<tr class="even">
<td></td>
<td>اپراتور شبکه شارژ<sup><a href="#fn-6-64" id="fnref-6-64">6</a></sup></td>
<td>مدیریت نشست‌ها، صدور دستورات و پیگیری رخدادهای عملیاتی.</td>
</tr>
<tr class="odd">
<td></td>
<td>مالک سایت<sup><a href="#fn-7-64" id="fnref-7-64">7</a></sup></td>
<td>دریافت گزارش‌های مالی، تحلیل عملکرد و بهره‌وری تجهیزات سایت.</td>
</tr>
<tr class="even">
<td></td>
<td>مدیر سامانه<sup><a href="#fn-8-64" id="fnref-8-64">8</a></sup></td>
<td>تحلیل جامع عملکرد سیستم، درآمد و گزارش‌های کلان.</td>
</tr>
<tr class="odd">
<td></td>
<td>کارشناس عملیات<sup><a href="#fn-9-64" id="fnref-9-64">9</a></sup></td>
<td>آنالیز کیفیت سرویس و شناسایی نقاط قابل بهبود در فرآیندها.</td>
</tr>
<tr class="even">
<td><strong>سیستمی</strong></td>
<td>شارژر<sup><a href="#fn-10-64" id="fnref-10-64">10</a></sup></td>
<td>تجهیز فیزیکی که دستورات را از CSMS دریافت کرده و داده‌های عملکردی را ارسال می‌کند.</td>
</tr>
<tr class="odd">
<td></td>
<td>سیستم پیام‌رسان<sup><a href="#fn-11-64" id="fnref-11-64">11</a></sup></td>
<td>مسئول ارسال اعلان‌ها به ذی‌نفعان.</td>
</tr>
<tr class="even">
<td></td>
<td>سیستم پرداخت<sup><a href="#fn-12-64" id="fnref-12-64">12</a></sup></td>
<td>مسئول پردازش نهایی هزینه‌ها و ثبت تراکنش‌های مالی.</td>
</tr>
</tbody>
</table>

</div>

<div role="status" aria-live="polite" aria-atomic="true">

</div>

</div>

## ۳. تحلیل کارکردها و روابط

در این بخش، کارکردهای اصلی سامانه بر اساس نمودار توضیح داده می‌شوند.

- ‏**include (الزام):** نشان‌دهنده یک کارکرد الزامی است که همیشه به عنوان بخشی از کارکرد اصلی اجرا می‌شود.
- ‏**extend (توسعه/شرط):** نشان‌دهنده یک کارکرد اختیاری یا شرطی است که تنها در شرایط خاصی به کارکرد اصلی اضافه می‌شود.

### ۳.۱. فاز اول: شروع نشست شارژ<sup><a href="#fn-13-64" id="fnref-13-64">13</a></sup>

این فرآیند، نقطه آغاز تعامل کاربر با سیستم برای شارژ خودرو است و جریان اصلی آن شامل گام‌های الزامی زیر است:

- ‏**Start charging session**<sup><a href="#fn-14-64" id="fnref-14-64">14</a></sup>: این کارکرد اصلی توسط **راننده** یا **اپراتور شبکه شارژ** آغاز می‌شود.
- ‏(include) **Check equipment status**<sup><a href="#fn-15-64" id="fnref-15-64">15</a></sup> (بررسی وضعیت تجهیزات): اولین گام الزامی، بررسی در دسترس بودن تجهیزات است.
  - ‏(extend) **Show Unavailable status**<sup><a href="#fn-16-64" id="fnref-16-64">16</a></sup> (نمایش وضعیت عدم دسترسی): **اگر و تنها اگر** تجهیزات (ایستگاه، شارژر یا کانکتور) در دسترس نباشند، این کارکرد اجرا می‌شود.
- ‏(include) **Register Initial Session Info**<sup><a href="#fn-17-64" id="fnref-17-64">17</a></sup> (ثبت اطلاعات اولیه): در صورت شروع نشست، اطلاعات اولیه نشست ثبت می‌شود.
- ‏(include)**Create Session with Unique ID**<sup><a href="#fn-18-64" id="fnref-18-64">18</a></sup> (ایجاد نشست با شناسه یکتا): یک شناسه منحصر‌به‌فرد برای نشست جدید ایجاد می‌شود.
- ‏(include) **Send Start command to charger**<sup><a href="#fn-19-64" id="fnref-19-64">19</a></sup> (ارسال فرمان شروع به شارژر): وقتی نشست شروع شود، دستور شروع به **شارژر** فیزیکی ارسال می‌شود.
- ‏(extend) **Receive Confirmation from Charger**<sup><a href="#fn-20-64" id="fnref-20-64">20</a></sup> (دریافت تأییدیه از شارژر): سامانه منتظر پاسخ از **شارژر** می‌ماند.
- ‏(extend) **Update Session & Connector status**<sup><a href="#fn-21-64" id="fnref-21-64">21</a></sup> (به‌روزرسانی وضعیت): **پس از دریافت تأییدیه مثبت** از شارژر، این کارکرد اجرا شده و وضعیت نشست و کانکتور به‌روز می‌شود.
- ‏(extend) **Receive & Store performance data**<sup><a href="#fn-22-64" id="fnref-22-64">22</a></sup> (دریافت و ذخیره داده‌های عملکردی): در صورت شروع نشست می‌تواند داده‌های عملکردی را دریافت و ذخیره کند.

### ۳.۲. فاز دوم: پایش نشست<sup><a href="#fn-23-64" id="fnref-23-64">23</a></sup>

در طول اجرای نشست، سامانه به صورت پیوسته داده‌ها را پایش می‌کند.

- ‏**Receive & Store performance data**<sup><a href="#fn-22" id="fnref-22-2">22</a></sup> (دریافت و ذخیره داده‌های عملکردی): این کارکرد وظیفه جمع‌آوری داده‌های لحظه‌ای از شارژر را دارد.
- ‏(extend) **Detect events during session**<sup><a href="#fn-24-64" id="fnref-24-64">24</a></sup> (تشخیص رخدادها): این کارکرد وقتی داده‌های عملکردی دریافت و ذخیره شود می‌توان رخدادها را تشخیص داد.
- ‏(extend) **Monitor session data**<sup><a href="#fn-25-64" id="fnref-25-64">25</a></sup> (پایش مستمر نشست): وقتی نشست شروع شود این کارکرد به صورت پیوسته داده‌هایی مانند انرژی، توان و زمان را در طول نشست پایش می‌کند و به کارکرد اصلی متصل است.

### ۳.۳. فاز سوم: مدیریت خطا و رویدادها

سامانه رویدادهای غیرمنتظره یا خطاها را مدیریت کرده و اقدامات لازم را انجام می‌دهد.

‏**Detect events during session**<sup><a href="#fn-24" id="fnref-24-2">24</a></sup> (تشخیص رخدادها): این کارکرد به طور مداوم در حال بررسی رخدادها است.

- ‏(include) **Log Event in Session Records**<sup><a href="#fn-26-64" id="fnref-26-64">26</a></sup> (ثبت رخداد): هر رخدادی به صورت الزامی در سوابق نشست ثبت می‌شود.
- ‏(extend) **Safely stop session on critical error**<sup><a href="#fn-27-64" id="fnref-27-64">27</a></sup> (توقف ایمن در خطای بحرانی): این کارکرد **تنها در صورت بروز خطای بحرانی**، کارکرد اصلی پایش را توسعه می‌دهد و نشست را متوقف می‌کند. این توقف ایمن خود شامل موارد زیر است:
  - ‏(include) **Set Equipment Out of Service**<sup><a href="#fn-28-64" id="fnref-28-64">28</a></sup> (خارج از سرویس کردن تجهیز): وضعیت تجهیز معیوب به صورت الزامی به "خارج از سرویس" تغییر می‌کند.
- **Create fault event / inspection request**<sup><a href="#fn-29-64" id="fnref-29-64">29</a></sup> (ایجاد درخواست بررسی): یک درخواست بازرسی برای **اپراتور** جهت پیگیری مشکل ایجاد می‌شود.
  - ‏(extend) **Notify and suggest alternative equipment**<sup><a href="#fn-30-64" id="fnref-30-64">30</a></sup> (اطلاع‌رسانی و پیشنهاد جایگزین): اگر خطای بحرانی رخ دهد، این کارکرد فعال شده و به کاربر اطلاع‌رسانی می‌کند. و طبق روابطی که دارد این اعلان ذخیره می‌شود.

### ۳.۴. فاز چهارم: خاتمه نشست و تسویه مالی

این فرآیند با درخواست کاربر، اپراتور یا به صورت خودکار (تکمیل شارژ یا بروز خطا) آغاز می‌شود.

- ‏**End charging session**<sup><a href="#fn-31-64" id="fnref-31-64">31</a></sup>: کارکرد اصلی خاتمه نشست.
- ‏(include) **Record Session End Info**<sup><a href="#fn-32-64" id="fnref-32-64">32</a></sup> (ثبت اطلاعات نهایی): اطلاعات پایانی مانند انرژی کل، زمان و علت توقف به صورت الزامی ثبت می‌شود.
- ‏(include) **Update Final Connector Status**<sup><a href="#fn-33-64" id="fnref-33-64">33</a></sup> (به‌روزرسانی وضعیت نهایی کانکتور): وضعیت کانکتور پس از پایان نشست به‌روز می‌شود.
- ‏(include) **Calculate session cost**<sup><a href="#fn-34-64" id="fnref-34-64">34</a></sup> (محاسبه هزینه): پس از پایان نشست هزینه نشست بر اساس تعرفه‌ها محاسبه می‌شود.
- ‏(include) **Store Cost Financial Report**<sup><a href="#fn-35-64" id="fnref-35-64">35</a></sup> (ذخیره گزارش مالی): پس از محاسبه‌ی هزینه نتایج مالی برای گزارش‌گیری‌های بعدی ذخیره می‌شود.
- ‏**Process Payment**<sup><a href="#fn-36-64" id="fnref-36-64">36</a></sup> (پردازش پرداخت): این کارکرد به **سیستم پرداخت** متصل است و عملیات مالی را انجام می‌دهد.
- ‏(extend) **Create Operational Event for Abnormal End**<sup><a href="#fn-37-64" id="fnref-37-64">37</a></sup> (ایجاد رخداد برای پایان غیرعادی): **اگر نشست به دلیلی غیر از درخواست کاربر یا تکمیل شارژ پایان یابد** (مثلاً قطع ارتباط)، یک رخداد عملیاتی برای پیگیری **اپراتور** ایجاد می‌شود.

### ۳.۵. فاز پنجم: تحلیل و گزارش‌گیری

این کارکردها توسط بازیگران مدیریتی و عملیاتی برای تحلیل داده‌های جمع‌آوری شده استفاده می‌شوند:

- ‏**Analyze service quality**<sup><a href="#fn-38-64" id="fnref-38-64">38</a></sup>: توسط **کارشناس عملیات** برای تحلیل کیفیت خدمات.
- ‏**Performance & Utilization Analysis**<sup><a href="#fn-39-64" id="fnref-39-64">39</a></sup>: توسط **مالک سایت، کارشناس عملیات** و **مدیر سامانه** برای تحلیل بهره‌وری.
- ‏**Financial Report / Revenue Analysis**<sup><a href="#fn-40-64" id="fnref-40-64">40</a></sup>: توسط **مالک سایت** و **مدیر سامانه** برای تحلیل درآمد.
- ‏**Operator follows up operational event**<sup><a href="#fn-41-64" id="fnref-41-64">41</a></sup>: **اپراتور** رخدادهای باز را پیگیری و مدیریت می‌کند.
  - ‏(include) **Create fault event / inspection request**<sup><a href="#fn-29" id="fnref-29-2">29</a></sup>: این کارکرد نشان می‌دهد که پیگیری رویداد عملیاتی توسط اپراتور، الزاماً و همیشه شامل ایجاد یک رویداد خطا یا درخواست بازرسی است.

## ۴. تعامل با سیستم‌های جانبی

همانطور که در نمودار مشخص است، سامانه برای تکمیل چرخه کاری خود با دو سیستم خارجی کلیدی در تعامل است:

- **تعامل با سیستم پیام‌رسان<sup><a href="#fn-11" id="fnref-11-2">11</a></sup>**:

  - کارکرد **Send Notification**<sup><a href="#fn-42-64" id="fnref-42-64">42</a></sup> مسئول ارسال تمامی پیام‌ها به ذی‌نفعان است.
  - این سیستم، اطلاعاتی مانند شروع/پایان شارژ، بروز خطا، یا پیشنهاد تجهیز جایگزین را به کاربران و اپراتورها اطلاع می‌دهد و سوابق آن در **Store Notification Log**<sup><a href="#fn-43-64" id="fnref-43-64">43</a></sup> ذخیره می‌شود.

- **تعامل با سیستم پرداخت<sup><a href="#fn-12" id="fnref-12-2">12</a></sup>**:

  - کارکرد **Process Payment**<sup><a href="#fn-36" id="fnref-36-2">36</a></sup> پس از محاسبه هزینه، فرآیند تسویه حساب را از طریق این سیستم انجام می‌دهد. این تعامل برای تکمیل چرخه مالی نشست ضروری است.

## تصویر نمودار

<a href="../../../../../assets/uml/session/use-case.jpg" aria-description="Click to view image in full screen" aria-haspopup="dialog"><img src="../../../../../assets/uml/session/use-case.jpg" decoding="async" loading="lazy" width="900" height="462" alt="نمودار مورد کاربرد فرایند مدیریت نشست شارژ" /></a>

## پانویس‌ها

<div class="section">

1.  <div id="fn-1-64">

    Use Case [↩](#fnref-1-64 "Back to reference 1")

    </div>

2.  <div id="fn-2-64">

    Charging Station Management System [↩](#fnref-2-64 "Back to reference 2")

    </div>

3.  <div id="fn-3-64">

    Actors [↩](#fnref-3-64 "Back to reference 3")

    </div>

4.  <div id="fn-4-64">

    Use Cases [↩](#fnref-4-64 "Back to reference 4")

    </div>

5.  <div id="fn-5-64">

    Driver [↩](#fnref-5-64 "Back to reference 5")

    </div>

6.  <div id="fn-6-64">

    Charge Point Operator (CPO) [↩](#fnref-6-64 "Back to reference 6")

    </div>

7.  <div id="fn-7-64">

    Site Owner [↩](#fnref-7-64 "Back to reference 7")

    </div>

8.  <div id="fn-8-64">

    System Manager [↩](#fnref-8-64 "Back to reference 8")

    </div>

9.  <div id="fn-9-64">

    Operations Expert [↩](#fnref-9-64 "Back to reference 9")

    </div>

10. <div id="fn-10-64">

    Charger [↩](#fnref-10-64 "Back to reference 10")

    </div>

11. <div id="fn-11-64">

    Notification System [↩](#fnref-11-64 "Back to reference 11") [↩<sup>2</sup>](#fnref-11-2)

    </div>

12. <div id="fn-12-64">

    Payment System [↩](#fnref-12-64 "Back to reference 12") [↩<sup>2</sup>](#fnref-12-2)

    </div>

13. <div id="fn-13-64">

    Start Charging Session [↩](#fnref-13-64 "Back to reference 13")

    </div>

14. <div id="fn-14-64">

    Start charging session [↩](#fnref-14-64 "Back to reference 14")

    </div>

15. <div id="fn-15-64">

    Check equipment status [↩](#fnref-15-64 "Back to reference 15")

    </div>

16. <div id="fn-16-64">

    Show Unavailable status [↩](#fnref-16-64 "Back to reference 16")

    </div>

17. <div id="fn-17-64">

    Register Initial Session Info [↩](#fnref-17-64 "Back to reference 17")

    </div>

18. <div id="fn-18-64">

    Create Session with Unique ID [↩](#fnref-18-64 "Back to reference 18")

    </div>

19. <div id="fn-19-64">

    Send Start command to charger [↩](#fnref-19-64 "Back to reference 19")

    </div>

20. <div id="fn-20-64">

    Receive Confirmation from Charger [↩](#fnref-20-64 "Back to reference 20")

    </div>

21. <div id="fn-21-64">

    Update Session & Connector status [↩](#fnref-21-64 "Back to reference 21")

    </div>

22. <div id="fn-22-64">

    Receive & Store performance data [↩](#fnref-22-64 "Back to reference 22") [↩<sup>2</sup>](#fnref-22-2)

    </div>

23. <div id="fn-23-64">

    Monitoring [↩](#fnref-23-64 "Back to reference 23")

    </div>

24. <div id="fn-24-64">

    Detect events during session [↩](#fnref-24-64 "Back to reference 24") [↩<sup>2</sup>](#fnref-24-2)

    </div>

25. <div id="fn-25-64">

    Monitor session data [↩](#fnref-25-64 "Back to reference 25")

    </div>

26. <div id="fn-26-64">

    Log Event in Session Records [↩](#fnref-26-64 "Back to reference 26")

    </div>

27. <div id="fn-27-64">

    Safely stop session on critical error [↩](#fnref-27-64 "Back to reference 27")

    </div>

28. <div id="fn-28-64">

    Set Equipment Out of Service [↩](#fnref-28-64 "Back to reference 28")

    </div>

29. <div id="fn-29-64">

    Create fault event / inspection request [↩](#fnref-29-64 "Back to reference 29") [↩<sup>2</sup>](#fnref-29-2)

    </div>

30. <div id="fn-30-64">

    Notify and suggest alternative equipment [↩](#fnref-30-64 "Back to reference 30")

    </div>

31. <div id="fn-31-64">

    End charging session [↩](#fnref-31-64 "Back to reference 31")

    </div>

32. <div id="fn-32-64">

    Record Session End Info [↩](#fnref-32-64 "Back to reference 32")

    </div>

33. <div id="fn-33-64">

    Update Final Connector Status [↩](#fnref-33-64 "Back to reference 33")

    </div>

34. <div id="fn-34-64">

    Calculate session cost [↩](#fnref-34-64 "Back to reference 34")

    </div>

35. <div id="fn-35-64">

    Store Cost Financial Report [↩](#fnref-35-64 "Back to reference 35")

    </div>

36. <div id="fn-36-64">

    Process Payment [↩](#fnref-36-64 "Back to reference 36") [↩<sup>2</sup>](#fnref-36-2)

    </div>

37. <div id="fn-37-64">

    Create Operational Event for Abnormal End [↩](#fnref-37-64 "Back to reference 37")

    </div>

38. <div id="fn-38-64">

    Analyze service quality [↩](#fnref-38-64 "Back to reference 38")

    </div>

39. <div id="fn-39-64">

    Performance & Utilization Analysis [↩](#fnref-39-64 "Back to reference 39")

    </div>

40. <div id="fn-40-64">

    Financial Report / Revenue Analysis [↩](#fnref-40-64 "Back to reference 40")

    </div>

41. <div id="fn-41-64">

    Operator follows up operational event [↩](#fnref-41-64 "Back to reference 41")

    </div>

42. <div id="fn-42-64">

    Send Notification [↩](#fnref-42-64 "Back to reference 42")

    </div>

43. <div id="fn-43-64">

    Store Notification Log [↩](#fnref-43-64 "Back to reference 43")

    </div>

</div>
