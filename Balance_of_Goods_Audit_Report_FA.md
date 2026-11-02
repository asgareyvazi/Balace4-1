# گزارش ممیزی و مغایرت‌گیری نهایی تراز کالا

**تاریخ:** 2026-11-02  |  **شاخه:** `arena/dc3e69e5-balace4-1`  |  **وضعیت:** مغایرت جمع کل صفر شده؛ چند مورد توصیفی/قراردادی برای تایید انسانی باز است.

## ۱. خلاصه اجرایی

فایل اصلاح‌شده از ۸ شیت تشکیل شده است: یک Master و هفت منبع. جمع نهایی منابع و جمع ردیف‌های Master هر دو **$4,251,805.00** است و سلول اختلاف **`Total Material Balance!AP193 = $0.00`** می‌شود. اختلاف قبلی **$176,505.60** در سطح اقلام و فرمول‌های پشتیبان ریشه‌یابی شد؛ هیچ balancing entry، مقدار/قیمت ساختگی یا دستکاری Grand Total به‌تنهایی استفاده نشد. اصل workbook دست‌نخورده است.

در نسخه نهایی **2,304 فرمول** وجود دارد. نسبت به فایل اصلی 602 سلول مقدار/فرمول تغییر کرده است: 543 فرمول افزوده، 33 فرمول اصلاح و 3 فرمول حذف شده؛ تمام سلول‌های دارای مقدار نهاییِ متفاوت از اصل با زرد روشن `FFFFF2CC` مشخص‌اند (سلول‌های بدون تغییر زرد نشده‌اند). آزمون Python تعداد تغییرات بدون زرد را **0** یافت.

### جمع منابع و Master

| شیت/شناسه | سلول جمع نهایی | جمع محاسبه‌شده (USD) |
|---|---:|---:|
| AZN12 — `Cost Breakdown-Material-12` | `O14` | $175,955.00 |
| AZN075 — `Cost Breakdown-Material-075` | `N29` | $400,970.00 |
| AZN113 — `Material Balance 127-113` | `N19` | $380,720.00 |
| AZN166 — `Material Balance 166` | `N16` | $1,134,280.00 |
| F-20 / 207 — `Cost Breakdown-Material-F-20` | `N69` | $2,073,460.00 |
| AZN075 — مسیر اضافی — `Cost Breakdown-Material-075 (2` | `N21` | $15,940.00 |
| AZN-122 — `Cost Breakdown-Material-122` | `N24` | $70,480.00 |
| **جمع ۷ منبع** | **`AQ193`** | **$4,251,805.00** |
| **جمع Master از subtotalهای رده‌ای** | **`AQ192`** | **$4,251,805.00** |
| **اختلاف: منابع منهای Master** | **`AP193`** | **$0.00** |

### تطبیق رده‌ای

| رده Master | سلول subtotal | مبلغ (USD) |
|---|---:|---:|
| Completion Equipment | `AQ4` | $0.00 |
| Wellhead & Xmas tree Equipment | `AQ10` | $1,027,965.00 |
| Tubular goods | `AQ36` | $2,535,550.00 |
| Casing Accessories | `AQ70` | $224,240.00 |
| Whip stock | `AQ132` | $340,750.00 |
| Liner Hanger | `AQ136` | $8,500.00 |
| Liner Top Packer Assembly | `AQ170` | $0.00 |
| Drilling Bit &mill | `AQ173` | $114,800.00 |

## ۲. ریشه‌یابی اختلاف و اصلاحات اثرگذار

### Tubular goods — افزایش خالص Master به اندازه $30,935.60

- **ردیف 49:** فرمول هزینه قبلی `=-(AP49)*D49` همراه با `AP49=(AM49*9.6)+AL49` ارزش اضافی/کاهشی از موجودی F/PEDEC وارد می‌کرد؛ این مبنا با فرمول هزینه منبع M سازگار نبود. `AQ49` اکنون مستقیماً `M17` از F-20 و `M12` از 127-113 را جمع می‌زند: **$533,280.00 → $570,000.00** (+$36,720.00). مقدار عملیاتی AP دستکاری نشد؛ فرمول هزینه به مبنای مستند source M متصل است.
- **ردیف 51:** همان ناهمخوانی ضریب 9.6؛ `AQ51` اکنون جمع فرمول‌های `F-20!M18` و `127-113!M13` است: **$37,454.40 → $32,400.00** (−$5,054.40).
- **ردیف 62:** `AJ62` از مقدار ثابت 9 به جمع پویای شش سلول L منبع تغییر کرد (مقدار فعلی 10)؛ هزینه از **$2,800.00 به $2,450.00** رسید. قلم اضافی F-20 ردیف 27 به‌دلیل حذف عبارت Type 1 در شرح منبع، جداگانه در ردیف 188 ثبت شد (**$1,750.00**) و با ردیف 62 ادغام نشد.
- **ردیف‌های 64 و 68:** ردیف 64 فقط پنج رکورد Gas Tight را شامل می‌شود؛ ارجاعات اضافی منبع 127-113 ردیف 18 (Premium Conn.) از سلول‌های H/P/W64 حذف و به ردیف مستقل 68 اختصاص یافت. ردیف 64: **$9,500 → $7,600**؛ قیمت ردیف 68 که صفر بود به منبع `127-113!D18` متصل شد و هزینه آن **$1,520** شد.
- **ردیف 66:** شش مقدار قراردادی قبلی hardcode بود؛ منبع برای قلم 4 1/2-inch، 3 m، Premium در F-20 رکورد ندارد. سلول J66 حذف شد و پنج مقدار باقیمانده به sourceها وصل شد: جمع مقدار **30→25** و هزینه **$10,500→$8,750**. قلم مستقل F-20 ردیف 27 جدا نگه داشته شد.

### Casing Accessories — افزایش خالص Master به اندازه $30,770.00

- ردیف 103: `AJ103` از 340 hardcode به `F-20!L47` (34) اصلاح شد؛ هزینه **$1,200→$37,920** (+$36,720).
- ردیف 104: هزینه مستقیماً به `F-20!M48` وصل شد؛ **$0→−$3,120** (−$3,120).
- ردیف 95: هزینه به جمع `F-20!M44` و `075 (2)!M6` وصل شد؛ **$910→$780** (−$130).
- ردیف‌های 124 و 128: هزینه به ردیف‌های منبع هم‌قیمت $900 متصل شد؛ به‌ترتیب **$9,000→$8,100** و **$8,100→$7,200** (هرکدام −$900). ردیف 127 با اتصال `AJ127=075!L20` از تحویل 1 به 2 اصلاح شد و هزینه **$900→$0** (−$900).
- ردیف‌های 88 و 89: مقدار تحویل Float Shoe/Float Collar به سلول L منبع خود وصل شد؛ مقادیر هزینه به‌ترتیب **$7,000→$14,000** و **$7,000→$0** شدند (اثر خالص صفر، اما تخصیص قلمی اصلاح شد).
- ردیف‌های 81 و 82: ارجاعات مقدار قرارداد به‌جای source rows 40/41 (Float Shoe/Collar) اکنون به source rows 49/50 (Cement Plug Top/Bottom) وصل‌اند؛ مقدار جاری برابر بود، اما پیوند پویا و قابل ردیابی اصلاح شد.

### Drilling Bit &mill — جمع Master از $0 به $114,800

۹ ردیف موجود Master (174–182) اکنون قیمت/مقدار/حرکت‌های موجود را به sourceها وصل می‌کنند و `AQ` هر ردیف از فرمول‌های هزینه M منبع جمع می‌شود. پنج ردیف جاافتاده در 183–187 افزوده شد. جمع مستقل ردیف‌های bit/mill در ۷ منبع **$114,800.00** و جمع ردیف‌های 174–187 در Master **$114,800.00** است.

| ردیف Master | قلم | جمع هزینه منبع (USD) |
|---:|---|---:|
| 174 | 12 1/4" Rock Bit | $13,000.00 |
| 175 | 12 1/4" PDC Bit | -$200,000.00 |
| 176 | 8 1/2" Rock Bit | $76,000.00 |
| 177 | 8 1/2" PDC Bit | $52,000.00 |
| 178 | 5 7/8" Rock Bit | $39,000.00 |
| 179 | 6 1/8" PDC Bit | $0.00 |
| 180 | 6" Mill | $71,500.00 |
| 181 | 4 1/8" Mill | $19,500.00 |
| 182 | 3 3/4" Mill | $32,500.00 |
| 183 | 26" Rock Bit | $57,300.00 |
| 184 | 17-1/2" Rock Bit | $0.00 |
| 185 | 17-1/2" PDC Bit | -$72,000.00 |
| 186 | 6 1/8" Rock Bit | $13,000.00 |
| 187 | 3-1/8" Mill | $13,000.00 |

## ۳. ردیف‌های افزوده‌شده و عنوان‌های تطبیق‌داده‌شده

### ۹ ردیف افزوده‌شده در Master

| ردیف | شرح همانند منبع | واحد | منبع پشتیبان | هزینه مانده فعلی (USD) | توضیح |
|---:|---|---|---|---:|---|
| 183 | 26" Rock Bit | each | F-20!B72 | $57,300.00 | قلم Drilling Bit قبلاً در Master بدون هزینه بود. |
| 184 | 17-1/2" Rock Bit | each | F-20!B73 | $0.00 | قلم Drilling Bit منبع؛ نرخ/مانده از source M. |
| 185 | 17-1/2" PDC Bit | each | F-20!B74 | -$72,000.00 | هزینه منفی منبع حفظ شد؛ هیچ تعدیلی اعمال نشد. |
| 186 | 6 1/8" Rock Bit | each | 075!B33 و 075 (2)!B26 | $13,000.00 | دو رکورد 6 1/8 Rock Bit با مشخصات و نرخ $6,500؛ جمع پویای M. |
| 187 | 3-1/8" Mill | each | 122!B34 | $13,000.00 | قلم Mill منبع، بدون ادغام با اندازه دیگر. |
| 188 | Tubing pup joint, 4 1/2", L-80,Gas Tight  Connection 18.9 ppf, seamless,1.5 m long , PSL3 | ea. | F-20!B27 | $1,750.00 | جدا از ردیف 62 تا تایید وجود/عدم وجود L-80 Type 1. |
| 189 | Casing, 7", TP110S, 35 ppf, TPCQ, R3 | Jt. | F-20!B16 | $0.00 | جدا از ردیف 43؛ Casing با Liner یکی فرض نشد. |
| 190 | Centralizer, Bow type, 7" x 8-3/8", Non-welded | ea. | F-20!B46 | $0.00 | جدا از Master row 99؛ شرح/ساختار فنی تایید نشده. |
| 191 | Drift Gauge, API, for 7" 35# casing | ea. | F-20!B59 | $0.00 | جدا از Master row 119؛ 35# با 32# ادغام نشد. |

### جدول تطبیق ۳۱ عنوان منبعِ بدون تطبیق دقیق در مبنای ممیزی پیشین

شرح فنی اصل منبع حفظ شده است؛ ستون آخر وضعیت نگاشت/تایید را نشان می‌دهد. موارد «جدا» عمداً به قلم مشابه ادغام نشدند.

| شیت منبع | ردیف/شرح منبع | Master row | نتیجه بررسی |
|---|---|---:|---|
| `Cost Breakdown-Material-075` | `13` — Centralizer, 5 " x 8 1/2", Non weld, Bow spring type, c/w nails (ea.) | 92 | تطبیق عنوان/واحد؛ تفاوت Non weld و Non0weld صرفاً نگارشی، ابعاد و نوع یکسان. |
| `Cost Breakdown-Material-075` | `33` — 6 1/8" Rock Bit (each) | 186 | ردیف افزوده‌شده؛ 6 1/8 Rock Bit، با همان مشخصه در 075 مسیر اضافی. |
| `Cost Breakdown-Material-F-20` | `15` — Casing, 7", 110S, 32 ppf Premium Conn.,seamless, R3, PLS-3. (m) | 41 | تطبیق بررسی‌شده: 7 اینچ، 110S، 32 ppf، Premium، واحد m؛ PLS-3/PLS03 تفاوت نوشتاری. |
| `Cost Breakdown-Material-F-20` | `16` — Casing, 7", TP110S, 35 ppf, TPCQ, R3 (Jt.) | 189 | ردیف جدید و جدا؛ Casing با ردیف نزدیک Master که Liner است ادغام نشد. |
| `Cost Breakdown-Material-F-20` | `21` — Casing Pup Joint, 9 5/8", 110SS, 53.5 PPF, Gas Tight Conn.,seamless, 1.5m long, PSL3. (ea.) | 55 | پیوند منبع موجود؛ 110SS در برابر 110S نیازمند تایید فنی/تجاری. |
| `Cost Breakdown-Material-F-20` | `22` — Casing Pup Joint, 9 5/8", 110SS, 53.5 PPF,Gas Tight Conn.,seamless, 3m long, PSL3. (ea.) | 56 | پیوند منبع موجود؛ 110SS در برابر 110S نیازمند تایید فنی/تجاری. |
| `Cost Breakdown-Material-F-20` | `24` — Tubing pup joint, 4 1/2", L-80 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3. (ea.) | 62 | تطبیق با مشخصات 4 1/2، L-80 Type 1، 18.9 ppf، Gas Tight، 1.5 m. |
| `Cost Breakdown-Material-F-20` | `25` — Crossover, 4-1/2" 18.9 PPF Box × 3-1/2" 10.2 PPF Pin, Gas Tight Conn, L-80 type1 1.2m long, PSL3. (ea.) | 64 | Gas Tight crossover؛ ردیف 127-113 با Premium Conn از این ردیف جدا شد. |
| `Cost Breakdown-Material-F-20` | `26` — Tubing pup joint, 3 1/2", L-80 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3. (ea.) | 63 | تطبیق با مشخصات 3 1/2، 10.2 ppf، Gas Tight، 1.5 m. |
| `Cost Breakdown-Material-F-20` | `27` — Tubing pup joint, 4 1/2", L-80,Gas Tight  Connection 18.9 ppf, seamless,1.5 m long , PSL3 (ea.) | 188 | ردیف جدید و جدا؛ منبع L-80 را می‌گوید، اما Type 1 را تصریح نمی‌کند؛ تایید هم‌ارزی با ردیف 62 لازم است. |
| `Cost Breakdown-Material-F-20` | `28` — Tubing pup joint, 3 1/2", L-80,premium Connection 10.2 ppf,13CR-1 MO, seamless,3 m long , PSL3 (ea.) | 67 | تطبیق مشخصات؛ 13CR-1 MO/13CR01 MO نگارش‌های متفاوت، مقدار و قیمت منبع مستقیماً پیوند شد. |
| `Cost Breakdown-Material-F-20` | `41` — Float Collar, 9 5/8", 110S, premium connection, 53.5 ppf, Special drift, c/w non-rotating profile, PDC drillable, PSL3. (ea.) | 89 | تطبیق Float Collar؛ اصلاح پیوند مقدار تحویل با ردیف منبع خودش. |
| `Cost Breakdown-Material-F-20` | `42` — Centralizer, 9 5/8" x 12 1/4", Non-weld,Bow-spring type, c/w nails (ea.) | 90 | تطبیق centralizer 9 5/8 x 12 1/4، Non-weld/Bow-spring؛ تفاوت نگارشی. |
| `Cost Breakdown-Material-F-20` | `46` — Centralizer, Bow type, 7" x 8-3/8", Non-welded (ea.) | 190 | ردیف جدید جداگانه؛ احتمال شباهت به ردیف 99 کافی برای ادغام نیست؛ مقدار/هزینه صفر. |
| `Cost Breakdown-Material-F-20` | `51` — Cement Plug, Top, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non- rotating type (ea.) | 109 | تطبیق Cement Plug Top برای 9 5/8؛ تفاوت Non-rotating/Non0 rotating نگارشی. |
| `Cost Breakdown-Material-F-20` | `52` — Cement Plug, Bottom, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non- rotating type (ea.) | 110 | تطبیق Cement Plug Bottom برای 9 5/8؛ تفاوت Non-rotating/Non0 rotating نگارشی. |
| `Cost Breakdown-Material-F-20` | `59` — Drift Gauge, API, for 7" 35# casing (ea.) | 191 | ردیف جدید جدا؛ 7 اینچ، 35# با ردیف Master 119 که 7 اینچ، 32# است ادغام نشد. |
| `Cost Breakdown-Material-F-20` | `63` — Rotating liner hanger, hydraulic set, tandem cone, with integral/split, weight set top packer, 7" 32# x 9 5/8" 47-53.5#, 110S, PREMIUM connection, 10 ft PBR, load capacity 2,000KN, packer seal capacity 10,000 psi, Temperature 150 ºC (set) | 137 | پیوند منبع در فایل موجود است، اما مشخصات فشار منبع 10,000 psi و Master برابر 5,000 psi است؛ تایید فنی الزامی؛ ارزش مانده فعلی صفر. |
| `Cost Breakdown-Material-F-20` | `64` — Float shoe, reamer type, 7", 32#, 110S,PREMIUM connection, PDC drillable (ea.) | 138 | تطبیق منبع 7-inch، 32# در بازه Master 29–32#، 110S، PDC drillable. |
| `Cost Breakdown-Material-F-20` | `65` — Float collar, 7", 32#, 110S, PREMIUM connection, PDC drillable (ea.) | 139 | تطبیق منبع 7-inch، 32# در بازه Master 29–32#، 110S، PDC drillable. |
| `Cost Breakdown-Material-F-20` | `66` — Landing collar c/w setting ball, 7", 32#, 110S,PREMIUM connection, PDC drillable (ea.) | 140 | تطبیق منبع 7-inch، 32# در بازه Master 29–32#، 110S، PDC drillable. |
| `Cost Breakdown-Material-F-20` | `72` — 26" Rock Bit (each) | 183 | ردیف جدید 26-inch Rock Bit. |
| `Cost Breakdown-Material-F-20` | `73` — 17-1/2" Rock Bit (each) | 184 | ردیف جدید 17-1/2-inch Rock Bit. |
| `Cost Breakdown-Material-F-20` | `74` — 17-1/2" PDC Bit (each) | 185 | ردیف جدید 17-1/2-inch PDC Bit. |
| `Cost Breakdown-Material-075 (2` | `26` — 6 1/8" Rock Bit (each) | 186 | تطبیق فنی با ردیف 186: 6 1/8-inch Rock Bit؛ نرخ هر دو منبع 6,500. |
| `Cost Breakdown-Material-122` | `8` — Tubing pup joint, 4 1/2", L-80 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3. (ea.) | 62 | تطبیق 4 1/2، L-80 Type 1، 18.9 ppf، Gas Tight، 1.5 m. |
| `Cost Breakdown-Material-122` | `9` — Tubing pup joint, 3 1/2", L-80 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3. (ea.) | 63 | تطبیق 3 1/2، L-80 Type 1، 10.2 ppf، Gas Tight، 1.5 m. |
| `Cost Breakdown-Material-122` | `10` — Crossover, 4-1/2" 18.9 PPF Box × 3-1/2" 10.2 PPF Pin, Gas Tight Conn, L-80 type1 1.2m long, PSL3. (ea.) | 64 | Gas Tight crossover؛ مشخصات اتصالات/ابعاد در ردیف منبع و Master یکسان. |
| `Cost Breakdown-Material-122` | `11` — Tubing pup joint, 4 1/2", L-80,premium Connection 18.9 ppf,13CR-1 MO, seamless,3 m long , PSL3 (ea.) | 66 | تطبیق مشخصات؛ 13CR-1 MO/13CR01 MO تفاوت نوشتاری. |
| `Cost Breakdown-Material-122` | `12` — Tubing pup joint, 3 1/2", L-80,premium Connection 10.2 ppf,13CR-1 MO, seamless,3 m long , PSL3 (ea.) | 67 | تطبیق مشخصات؛ 13CR-1 MO/13CR01 MO تفاوت نوشتاری. |
| `Cost Breakdown-Material-122` | `34` — 3-1/8" Mill (each) | 187 | ردیف جدید 3-1/8-inch Mill. |

## ۴. موارد باز برای تایید انسانی؛ هیچ‌یک اختلاف کل ایجاد نمی‌کند

1. `Cost Breakdown-Material-075!D16:E16` برای Stop Collar، 4 1/2-inch همچنان خالی است؛ در کل workbook مدرک قراردادی برای ساختن قیمت/مقدار یافت نشد. ردیف حفظ شده و باید مقدار مصوب/تعمدی‌بودن خالی بودن تایید شود.
2. `F-20!B27` (L-80 بدون عبارت Type 1) در Master row 188 مستقل از row 62 نگه داشته شد؛ هم‌ارزی فنی نیازمند تایید است.
3. `F-20!B21:B22` عنوان 110SS دارد، درحالی‌که Master rows 55–56 عنوان 110S دارد؛ پیوند منبع موجود است، اما تفاوت باید توسط کارشناس مواد/قرارداد تایید شود.
4. `F-20!B63` در برابر Master row137: source فشار packer seal برابر 10,000 psi و شرح Master برابر 5,000 psi است؛ این پیوند پیشین تا تایید فنی باز می‌ماند. مانده هزینه source در حال حاضر صفر است.
5. `F-20!B46` و Master row99 ممکن است Centralizer نزدیک باشند، اما row190 تا دریافت مشخصات/شناسه تاییدشده مستقل باقی مانده است. `F-20!B59` نیز 7-inch/35# است و با Master row119، 7-inch/32# ادغام نشده است.
6. منبع 6 1/8-inch PDC Bit در دو شیت، قیمت‌های $26,000 و $16,200 دارد؛ D179 در صورت نبود نرخ یکتا خالی می‌ماند و هیچ نرخ میانگین/ترکیبی ساخته نشده است. مانده هزینه هر دو رکورد اکنون صفر است؛ تفاوت نرخ برای تایید تجاری باقی است.
7. **57 عنوان Master** همچنان در منبع عنوان دقیق ندارند؛ اقلام قراردادی Master صرفاً به دلیل نبود در منابع فعلی حذف نشده‌اند. این‌ها در جمع Master حفظ شده و برای تایید قرارداد/شناسه در صورت نیاز علامت‌گذاری شده‌اند.

## ۵. فرمول‌ها، ردیابی و قالب‌بندی

- جمع کل Master در `AQ192` از subtotalهای رده‌ای `AQ4,AQ10,AQ36,AQ70,AQ132,AQ136,AQ170,AQ173` محاسبه می‌شود. جمع منابع در `AQ193` از هفت جمع نهایی شیت‌های منبع ساخته می‌شود و `AP193=AQ193-AQ192` اختلاف را نشان می‌دهد.
- ردیف‌های bit/mill 174–187 با پیوند مستقیم به مقادیر منبع E/J/G/H/L/F و هزینه M تکمیل شدند؛ جمع هر قلم به جای نرخ/مانده تجمیعی hardcode از فرمول‌های هزینه منبع گرفته می‌شود. هزینه‌ها با تغییر مقدار منبع به‌روزرسانی می‌شوند.
- افزایش 9 ردیف جدید و اصلاحات/ارجاعات در سلول‌های لازم با زرد روشن `FFFFF2CC` مشخص شده است. راهنمای داخل Master در `B194:B196` قرار دارد. سلول‌های خالیِ دست‌نخورده رنگ ردیابی نگرفته‌اند؛ حاشیه/فرمت عددی ردیف‌های داده تا حد ممکن از قالب موجود کپی شده است.
- محدوده چاپ Master تا `A1:AQ196` گسترش یافته تا اقلام تکمیلی، اختلاف و راهنما در خروجی چاپی دیده شوند. اصل workbook `08. Total Material Balance OEOC-31.xlsx` تغییر نکرده است.

## ۶. آزمون و اعتبارسنجی مستقل

- هر ۸ شیت با openpyxl باز شد؛ فرمول‌ها با موتور مستقل Python `formulas` محاسبه شدند؛ فرمول‌های خطادار/نتیجه‌های `#...` در خروجی محاسبه‌شده: **0**.
- جمع‌های هفت منبع مستقل از Master محاسبه شد و با `AQ192` تطبیق دارد. ردیف‌های drilling bit نیز مستقل از سلول subtotal منبع به‌صورت جمع M ردیف‌های جزئی محاسبه شدند: $114,800.00 در برابر $114,800.00.
- آزمون زنده روی نسخه آزمایشی موقت انجام شد: `F-20!E17` یک واحد افزایش یافت و AQ49/$75 افزایش کرد؛ `F-20!E72` یک واحد افزایش یافت و ردیف bit 183/$57,300 افزایش کرد. جمع Master و جمع منبع هر دو به $4,309,180 رسیدند و اختلاف همچنان $0 ماند. فایل آزمایشی تحویل نشده است.
- Microsoft Excel و LibreOffice/soffice در محیط در دسترس نبودند؛ بنابراین محاسبه بومی Excel/LibreOffice انجام نشده است. نتیجه‌های بالا فقط اجرای واقعی Python `formulas` و آزمون زنده Python هستند و به‌عنوان آزمون native Excel گزارش نمی‌شوند.

## ۷. فهرست کامل سلول‌های مقدار/فرمول تغییرکرده نسبت به workbook اصلی

این جدول 602 تفاوت سلولی را با مقدار/فرمول قبل و بعد فهرست می‌کند. نام شیت و آدرس سلول در همان worksheet هستند؛ «∅» یعنی سلول خالی. هر تغییرِ حاوی مقدار نهایی زرد روشن است؛ تغییرهای صرفاً حذف‌شده نیز در جدول ثبت‌اند. این فهرست شامل اصلاحات پیشین جمع شیت‌های منبع و این دور اصلاح Master است.

| شیت | سلول | قبل از اصلاح | بعد از اصلاح |
|---|---|---|---|
| `Total Material Balance` | `AQ36` | `=SUM(AQ40:AQ69)` | `=SUM(AQ40:AQ69,AQ188:AQ189)` |
| `Total Material Balance` | `R40` | `∅` | `='Cost Breakdown-Material-F-20'!J14` |
| `Total Material Balance` | `AQ49` | `=-(AP49)*D49` | `=SUM('Cost Breakdown-Material-F-20'!M17,'Material Balance 127-113'!M12)` |
| `Total Material Balance` | `AQ51` | `=-(AP51)*D51` | `=SUM('Cost Breakdown-Material-F-20'!M18,'Material Balance 127-113'!M13)` |
| `Total Material Balance` | `R53` | `∅` | `='Cost Breakdown-Material-F-20'!J19` |
| `Total Material Balance` | `Y53` | `∅` | `='Cost Breakdown-Material-F-20'!G19` |
| `Total Material Balance` | `R54` | `∅` | `='Cost Breakdown-Material-F-20'!J20` |
| `Total Material Balance` | `Y54` | `∅` | `='Cost Breakdown-Material-F-20'!G20` |
| `Total Material Balance` | `R57` | `∅` | `='Cost Breakdown-Material-F-20'!J23` |
| `Total Material Balance` | `Y57` | `∅` | `='Cost Breakdown-Material-F-20'!G23` |
| `Total Material Balance` | `O59` | `∅` | `='Cost Breakdown-Material-075'!J6` |
| `Total Material Balance` | `V59` | `∅` | `='Cost Breakdown-Material-075'!G6` |
| `Total Material Balance` | `AJ62` | `9` | `=SUM('Cost Breakdown-Material-12'!L9,'Cost Breakdown-Material-075'!L7,'Material Balance 127-113'!L14,'Material Balance 166'!L11,'Cost Breakdown-Material-F-20'!L24,'Cost Breakdown-Material-122'!L8)` |
| `Total Material Balance` | `H64` | `='Material Balance 127-113'!E18` | `∅` |
| `Total Material Balance` | `M64` | `1` | `=SUM('Cost Breakdown-Material-12'!F11,'Cost Breakdown-Material-075'!F9,'Material Balance 166'!F13,'Cost Breakdown-Material-F-20'!F25,'Cost Breakdown-Material-122'!F10)` |
| `Total Material Balance` | `P64` | `='Material Balance 127-113'!J18` | `∅` |
| `Total Material Balance` | `AJ64` | `∅` | `=SUM('Cost Breakdown-Material-12'!L11,'Cost Breakdown-Material-075'!L9,'Material Balance 166'!L13,'Cost Breakdown-Material-F-20'!L25,'Cost Breakdown-Material-122'!L10)` |
| `Total Material Balance` | `AK64` | `∅` | `=SUM('Cost Breakdown-Material-12'!H11,'Cost Breakdown-Material-075'!H9,'Material Balance 166'!H13,'Cost Breakdown-Material-F-20'!H25,'Cost Breakdown-Material-122'!H10)` |
| `Total Material Balance` | `AQ64` | `=-(AP64)*D64` | `=SUM('Cost Breakdown-Material-12'!M11,'Cost Breakdown-Material-075'!M9,'Material Balance 166'!M13,'Cost Breakdown-Material-F-20'!M25,'Cost Breakdown-Material-122'!M10)` |
| `Total Material Balance` | `F66` | `5` | `='Cost Breakdown-Material-12'!E12` |
| `Total Material Balance` | `G66` | `5` | `='Cost Breakdown-Material-075'!E10` |
| `Total Material Balance` | `H66` | `5` | `='Material Balance 127-113'!E16` |
| `Total Material Balance` | `I66` | `5` | `='Material Balance 166'!E14` |
| `Total Material Balance` | `J66` | `5` | `∅` |
| `Total Material Balance` | `L66` | `5` | `='Cost Breakdown-Material-122'!E11` |
| `Total Material Balance` | `F67` | `15` | `='Cost Breakdown-Material-12'!E13` |
| `Total Material Balance` | `G67` | `15` | `='Cost Breakdown-Material-075'!E11` |
| `Total Material Balance` | `H67` | `15` | `='Material Balance 127-113'!E17` |
| `Total Material Balance` | `I67` | `15` | `='Material Balance 166'!E15` |
| `Total Material Balance` | `J67` | `15` | `='Cost Breakdown-Material-F-20'!E28` |
| `Total Material Balance` | `L67` | `15` | `='Cost Breakdown-Material-122'!E12` |
| `Total Material Balance` | `D68` | `0` | `='Material Balance 127-113'!D18` |
| `Total Material Balance` | `H68` | `∅` | `='Material Balance 127-113'!E18` |
| `Total Material Balance` | `P68` | `∅` | `='Material Balance 127-113'!J18` |
| `Total Material Balance` | `W68` | `∅` | `='Material Balance 127-113'!G18` |
| `Total Material Balance` | `AQ70` | `=SUM(AQ71:AQ131)` | `=SUM(AQ71:AQ131,AQ190:AQ191)` |
| `Total Material Balance` | `R71` | `∅` | `='Cost Breakdown-Material-F-20'!J30` |
| `Total Material Balance` | `Y71` | `∅` | `='Cost Breakdown-Material-F-20'!G30` |
| `Total Material Balance` | `R72` | `∅` | `='Cost Breakdown-Material-F-20'!J31` |
| `Total Material Balance` | `R73` | `∅` | `='Cost Breakdown-Material-F-20'!J32` |
| `Total Material Balance` | `R74` | `∅` | `='Cost Breakdown-Material-F-20'!J33` |
| `Total Material Balance` | `Y74` | `∅` | `='Cost Breakdown-Material-F-20'!G33` |
| `Total Material Balance` | `R75` | `∅` | `='Cost Breakdown-Material-F-20'!J34` |
| `Total Material Balance` | `Y76` | `∅` | `='Cost Breakdown-Material-F-20'!G35` |
| `Total Material Balance` | `Y77` | `∅` | `='Cost Breakdown-Material-F-20'!G36` |
| `Total Material Balance` | `R78` | `∅` | `='Cost Breakdown-Material-F-20'!J37` |
| `Total Material Balance` | `Y79` | `∅` | `='Cost Breakdown-Material-F-20'!G38` |
| `Total Material Balance` | `J81` | `='Cost Breakdown-Material-F-20'!E40` | `='Cost Breakdown-Material-F-20'!E49` |
| `Total Material Balance` | `Y81` | `∅` | `='Cost Breakdown-Material-F-20'!G49` |
| `Total Material Balance` | `J82` | `='Cost Breakdown-Material-F-20'!E41` | `='Cost Breakdown-Material-F-20'!E50` |
| `Total Material Balance` | `Y82` | `∅` | `='Cost Breakdown-Material-F-20'!G50` |
| `Total Material Balance` | `R83` | `∅` | `='Cost Breakdown-Material-F-20'!J55` |
| `Total Material Balance` | `Y83` | `∅` | `='Cost Breakdown-Material-F-20'!G55` |
| `Total Material Balance` | `R84` | `∅` | `='Cost Breakdown-Material-F-20'!J56` |
| `Total Material Balance` | `Y84` | `∅` | `='Cost Breakdown-Material-F-20'!G56` |
| `Total Material Balance` | `R88` | `∅` | `='Cost Breakdown-Material-F-20'!J40` |
| `Total Material Balance` | `AJ88` | `1` | `='Cost Breakdown-Material-F-20'!L40` |
| `Total Material Balance` | `AJ89` | `∅` | `='Cost Breakdown-Material-F-20'!L41` |
| `Total Material Balance` | `R94` | `∅` | `='Cost Breakdown-Material-F-20'!J43` |
| `Total Material Balance` | `AQ95` | `=-(AP95)*D95` | `=SUM('Cost Breakdown-Material-F-20'!M44,'Cost Breakdown-Material-075 (2'!M6)` |
| `Total Material Balance` | `V96` | `∅` | `='Cost Breakdown-Material-075'!G14` |
| `Total Material Balance` | `AA97` | `∅` | `='Cost Breakdown-Material-122'!G14` |
| `Total Material Balance` | `AA101` | `∅` | `='Cost Breakdown-Material-122'!G15` |
| `Total Material Balance` | `R103` | `∅` | `='Cost Breakdown-Material-F-20'!J47` |
| `Total Material Balance` | `AJ103` | `340` | `='Cost Breakdown-Material-F-20'!L47` |
| `Total Material Balance` | `AQ104` | `=-(AP104)*D104` | `='Cost Breakdown-Material-F-20'!M48` |
| `Total Material Balance` | `V107` | `∅` | `='Cost Breakdown-Material-075'!G15` |
| `Total Material Balance` | `R118` | `∅` | `='Cost Breakdown-Material-F-20'!J57` |
| `Total Material Balance` | `Y118` | `∅` | `='Cost Breakdown-Material-F-20'!G57` |
| `Total Material Balance` | `R119` | `∅` | `='Cost Breakdown-Material-F-20'!J58` |
| `Total Material Balance` | `Y119` | `∅` | `='Cost Breakdown-Material-F-20'!G58` |
| `Total Material Balance` | `S120` | `∅` | `='Cost Breakdown-Material-075 (2'!J11` |
| `Total Material Balance` | `Z120` | `∅` | `='Cost Breakdown-Material-075 (2'!G11` |
| `Total Material Balance` | `T123` | `∅` | `='Cost Breakdown-Material-122'!J19` |
| `Total Material Balance` | `AA123` | `∅` | `='Cost Breakdown-Material-122'!G19` |
| `Total Material Balance` | `AQ124` | `=-(AP124)*D124` | `=SUM('Cost Breakdown-Material-12'!M17,'Cost Breakdown-Material-075'!M19,'Material Balance 127-113'!M22,'Material Balance 166'!M19,'Cost Breakdown-Material-F-20'!M60)` |
| `Total Material Balance` | `O127` | `∅` | `='Cost Breakdown-Material-075'!J20` |
| `Total Material Balance` | `V127` | `∅` | `='Cost Breakdown-Material-075'!G20` |
| `Total Material Balance` | `AJ127` | `1` | `='Cost Breakdown-Material-075'!L20` |
| `Total Material Balance` | `AQ128` | `=-(AP128)*D128` | `=SUM('Cost Breakdown-Material-12'!M18,'Cost Breakdown-Material-075'!M21,'Material Balance 127-113'!M23,'Material Balance 166'!M20,'Cost Breakdown-Material-F-20'!M61)` |
| `Total Material Balance` | `S133` | `∅` | `='Cost Breakdown-Material-075 (2'!J13` |
| `Total Material Balance` | `Z133` | `∅` | `='Cost Breakdown-Material-075 (2'!G13` |
| `Total Material Balance` | `Z143` | `∅` | `='Cost Breakdown-Material-075 (2'!G15` |
| `Total Material Balance` | `Z144` | `∅` | `='Cost Breakdown-Material-075 (2'!G16` |
| `Total Material Balance` | `Z145` | `∅` | `='Cost Breakdown-Material-075 (2'!G17` |
| `Total Material Balance` | `Z146` | `∅` | `='Cost Breakdown-Material-075 (2'!G18` |
| `Total Material Balance` | `Z148` | `∅` | `='Cost Breakdown-Material-075 (2'!G20` |
| `Total Material Balance` | `J154` | `∅` | `='Cost Breakdown-Material-F-20'!E68` |
| `Total Material Balance` | `R154` | `∅` | `='Cost Breakdown-Material-F-20'!J68` |
| `Total Material Balance` | `Y154` | `∅` | `='Cost Breakdown-Material-F-20'!G68` |
| `Total Material Balance` | `V155` | `∅` | `='Cost Breakdown-Material-075'!G25` |
| `Total Material Balance` | `V156` | `∅` | `='Cost Breakdown-Material-075'!G26` |
| `Total Material Balance` | `V157` | `∅` | `='Cost Breakdown-Material-075'!G27` |
| `Total Material Balance` | `V158` | `∅` | `='Cost Breakdown-Material-075'!G28` |
| `Total Material Balance` | `AA167` | `∅` | `='Cost Breakdown-Material-122'!G25` |
| `Total Material Balance` | `AA168` | `∅` | `='Cost Breakdown-Material-122'!G26` |
| `Total Material Balance` | `AA169` | `∅` | `='Cost Breakdown-Material-122'!G27` |
| `Total Material Balance` | `V172` | `∅` | `='Cost Breakdown-Material-075'!G30` |
| `Total Material Balance` | `AQ173` | `=SUM(AQ174:AQ182)` | `=SUM(AQ174:AQ187)` |
| `Total Material Balance` | `D174` | `∅` | `='Cost Breakdown-Material-F-20'!D75` |
| `Total Material Balance` | `E174` | `∅` | `=SUM(F174:L174)` |
| `Total Material Balance` | `J174` | `∅` | `='Cost Breakdown-Material-F-20'!E75` |
| `Total Material Balance` | `M174` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F75)` |
| `Total Material Balance` | `R174` | `∅` | `='Cost Breakdown-Material-F-20'!J75` |
| `Total Material Balance` | `Y174` | `∅` | `='Cost Breakdown-Material-F-20'!G75` |
| `Total Material Balance` | `AB174` | `∅` | `=SUM(U174:AA174,AK174)-M174` |
| `Total Material Balance` | `AC174` | `∅` | `=N174-F174` |
| `Total Material Balance` | `AD174` | `∅` | `=O174-G174` |
| `Total Material Balance` | `AE174` | `∅` | `=P174-H174` |
| `Total Material Balance` | `AF174` | `∅` | `=Q174-I174` |
| `Total Material Balance` | `AG174` | `∅` | `=R174-J174` |
| `Total Material Balance` | `AH174` | `∅` | `=S174-K174` |
| `Total Material Balance` | `AI174` | `∅` | `=T174-L174` |
| `Total Material Balance` | `AJ174` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L75)` |
| `Total Material Balance` | `AK174` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H75)` |
| `Total Material Balance` | `AL174` | `∅` | `=SUM(N174:T174,AJ174)-E174` |
| `Total Material Balance` | `AM174` | `∅` | `=SUM(U174:AA174,AK174)-M174` |
| `Total Material Balance` | `AP174` | `∅` | `=AL174+AM174` |
| `Total Material Balance` | `AQ174` | `=-(AP174)*D174` | `=SUM('Cost Breakdown-Material-F-20'!M75)` |
| `Total Material Balance` | `D175` | `∅` | `='Cost Breakdown-Material-F-20'!D76` |
| `Total Material Balance` | `E175` | `∅` | `=SUM(F175:L175)` |
| `Total Material Balance` | `J175` | `∅` | `='Cost Breakdown-Material-F-20'!E76` |
| `Total Material Balance` | `M175` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F76)` |
| `Total Material Balance` | `R175` | `∅` | `='Cost Breakdown-Material-F-20'!J76` |
| `Total Material Balance` | `Y175` | `∅` | `='Cost Breakdown-Material-F-20'!G76` |
| `Total Material Balance` | `AB175` | `∅` | `=SUM(U175:AA175,AK175)-M175` |
| `Total Material Balance` | `AC175` | `∅` | `=N175-F175` |
| `Total Material Balance` | `AD175` | `∅` | `=O175-G175` |
| `Total Material Balance` | `AE175` | `∅` | `=P175-H175` |
| `Total Material Balance` | `AF175` | `∅` | `=Q175-I175` |
| `Total Material Balance` | `AG175` | `∅` | `=R175-J175` |
| `Total Material Balance` | `AH175` | `∅` | `=S175-K175` |
| `Total Material Balance` | `AI175` | `∅` | `=T175-L175` |
| `Total Material Balance` | `AJ175` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L76)` |
| `Total Material Balance` | `AK175` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H76)` |
| `Total Material Balance` | `AL175` | `∅` | `=SUM(N175:T175,AJ175)-E175` |
| `Total Material Balance` | `AM175` | `∅` | `=SUM(U175:AA175,AK175)-M175` |
| `Total Material Balance` | `AP175` | `∅` | `=AL175+AM175` |
| `Total Material Balance` | `AQ175` | `=-(AP175)*D175` | `=SUM('Cost Breakdown-Material-F-20'!M76)` |
| `Total Material Balance` | `D176` | `∅` | `=IF(AND('Cost Breakdown-Material-075'!D32='Cost Breakdown-Material-12'!D20,'Material Balance 127-113'!D25='Cost Breakdown-Material-12'!D20,'Material Balance 166'!D22='Cost Breakdown-Material-12'!D20,'Cost Breakdown-Material-F-20'!D77='Cost Breakdown-Material-12'!D20,'Cost Breakdown-Material-075 (2'!D24='Cost Breakdown-Material-12'!D20,'Cost Breakdown-Material-122'!D29='Cost Breakdown-Material-12'!D20),'Cost Breakdown-Material-12'!D20,"")` |
| `Total Material Balance` | `E176` | `∅` | `=SUM(F176:L176)` |
| `Total Material Balance` | `F176` | `∅` | `='Cost Breakdown-Material-12'!E20` |
| `Total Material Balance` | `G176` | `∅` | `='Cost Breakdown-Material-075'!E32` |
| `Total Material Balance` | `H176` | `∅` | `='Material Balance 127-113'!E25` |
| `Total Material Balance` | `I176` | `∅` | `='Material Balance 166'!E22` |
| `Total Material Balance` | `J176` | `∅` | `='Cost Breakdown-Material-F-20'!E77` |
| `Total Material Balance` | `K176` | `∅` | `='Cost Breakdown-Material-075 (2'!E24` |
| `Total Material Balance` | `L176` | `∅` | `='Cost Breakdown-Material-122'!E29` |
| `Total Material Balance` | `M176` | `∅` | `=SUM('Cost Breakdown-Material-12'!F20,'Cost Breakdown-Material-075'!F32,'Material Balance 127-113'!F25,'Material Balance 166'!F22,'Cost Breakdown-Material-F-20'!F77,'Cost Breakdown-Material-075 (2'!F24,'Cost Breakdown-Material-122'!F29)` |
| `Total Material Balance` | `N176` | `∅` | `='Cost Breakdown-Material-12'!J20` |
| `Total Material Balance` | `O176` | `∅` | `='Cost Breakdown-Material-075'!J32` |
| `Total Material Balance` | `P176` | `∅` | `='Material Balance 127-113'!J25` |
| `Total Material Balance` | `Q176` | `∅` | `='Material Balance 166'!J22` |
| `Total Material Balance` | `R176` | `∅` | `='Cost Breakdown-Material-F-20'!J77` |
| `Total Material Balance` | `S176` | `∅` | `='Cost Breakdown-Material-075 (2'!J24` |
| `Total Material Balance` | `T176` | `∅` | `='Cost Breakdown-Material-122'!J29` |
| `Total Material Balance` | `U176` | `∅` | `='Cost Breakdown-Material-12'!G20` |
| `Total Material Balance` | `V176` | `∅` | `='Cost Breakdown-Material-075'!G32` |
| `Total Material Balance` | `W176` | `∅` | `='Material Balance 127-113'!G25` |
| `Total Material Balance` | `X176` | `∅` | `='Material Balance 166'!G22` |
| `Total Material Balance` | `Y176` | `∅` | `='Cost Breakdown-Material-F-20'!G77` |
| `Total Material Balance` | `Z176` | `∅` | `='Cost Breakdown-Material-075 (2'!G24` |
| `Total Material Balance` | `AA176` | `∅` | `='Cost Breakdown-Material-122'!G29` |
| `Total Material Balance` | `AB176` | `∅` | `=SUM(U176:AA176,AK176)-M176` |
| `Total Material Balance` | `AC176` | `∅` | `=N176-F176` |
| `Total Material Balance` | `AD176` | `∅` | `=O176-G176` |
| `Total Material Balance` | `AE176` | `∅` | `=P176-H176` |
| `Total Material Balance` | `AF176` | `∅` | `=Q176-I176` |
| `Total Material Balance` | `AG176` | `∅` | `=R176-J176` |
| `Total Material Balance` | `AH176` | `∅` | `=S176-K176` |
| `Total Material Balance` | `AI176` | `∅` | `=T176-L176` |
| `Total Material Balance` | `AJ176` | `∅` | `=SUM('Cost Breakdown-Material-12'!L20,'Cost Breakdown-Material-075'!L32,'Material Balance 127-113'!L25,'Material Balance 166'!L22,'Cost Breakdown-Material-F-20'!L77,'Cost Breakdown-Material-075 (2'!L24,'Cost Breakdown-Material-122'!L29)` |
| `Total Material Balance` | `AK176` | `∅` | `=SUM('Cost Breakdown-Material-12'!H20,'Cost Breakdown-Material-075'!H32,'Material Balance 127-113'!H25,'Material Balance 166'!H22,'Cost Breakdown-Material-F-20'!H77,'Cost Breakdown-Material-075 (2'!H24,'Cost Breakdown-Material-122'!H29)` |
| `Total Material Balance` | `AL176` | `∅` | `=SUM(N176:T176,AJ176)-E176` |
| `Total Material Balance` | `AM176` | `∅` | `=SUM(U176:AA176,AK176)-M176` |
| `Total Material Balance` | `AP176` | `∅` | `=AL176+AM176` |
| `Total Material Balance` | `AQ176` | `=-(AP176)*D176` | `=SUM('Cost Breakdown-Material-12'!M20,'Cost Breakdown-Material-075'!M32,'Material Balance 127-113'!M25,'Material Balance 166'!M22,'Cost Breakdown-Material-F-20'!M77,'Cost Breakdown-Material-075 (2'!M24,'Cost Breakdown-Material-122'!M29)` |
| `Total Material Balance` | `D177` | `∅` | `=IF(AND('Cost Breakdown-Material-075 (2'!D25='Cost Breakdown-Material-F-20'!D78),'Cost Breakdown-Material-F-20'!D78,"")` |
| `Total Material Balance` | `E177` | `∅` | `=SUM(F177:L177)` |
| `Total Material Balance` | `J177` | `∅` | `='Cost Breakdown-Material-F-20'!E78` |
| `Total Material Balance` | `K177` | `∅` | `='Cost Breakdown-Material-075 (2'!E25` |
| `Total Material Balance` | `M177` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F78,'Cost Breakdown-Material-075 (2'!F25)` |
| `Total Material Balance` | `R177` | `∅` | `='Cost Breakdown-Material-F-20'!J78` |
| `Total Material Balance` | `S177` | `∅` | `='Cost Breakdown-Material-075 (2'!J25` |
| `Total Material Balance` | `Y177` | `∅` | `='Cost Breakdown-Material-F-20'!G78` |
| `Total Material Balance` | `Z177` | `∅` | `='Cost Breakdown-Material-075 (2'!G25` |
| `Total Material Balance` | `AB177` | `∅` | `=SUM(U177:AA177,AK177)-M177` |
| `Total Material Balance` | `AC177` | `∅` | `=N177-F177` |
| `Total Material Balance` | `AD177` | `∅` | `=O177-G177` |
| `Total Material Balance` | `AE177` | `∅` | `=P177-H177` |
| `Total Material Balance` | `AF177` | `∅` | `=Q177-I177` |
| `Total Material Balance` | `AG177` | `∅` | `=R177-J177` |
| `Total Material Balance` | `AH177` | `∅` | `=S177-K177` |
| `Total Material Balance` | `AI177` | `∅` | `=T177-L177` |
| `Total Material Balance` | `AJ177` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L78,'Cost Breakdown-Material-075 (2'!L25)` |
| `Total Material Balance` | `AK177` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H78,'Cost Breakdown-Material-075 (2'!H25)` |
| `Total Material Balance` | `AL177` | `∅` | `=SUM(N177:T177,AJ177)-E177` |
| `Total Material Balance` | `AM177` | `∅` | `=SUM(U177:AA177,AK177)-M177` |
| `Total Material Balance` | `AP177` | `∅` | `=AL177+AM177` |
| `Total Material Balance` | `AQ177` | `=-(AP177)*D177` | `=SUM('Cost Breakdown-Material-F-20'!M78,'Cost Breakdown-Material-075 (2'!M25)` |
| `Total Material Balance` | `D178` | `∅` | `=IF(AND('Material Balance 166'!D23='Material Balance 127-113'!D26,'Cost Breakdown-Material-F-20'!D79='Material Balance 127-113'!D26,'Cost Breakdown-Material-122'!D30='Material Balance 127-113'!D26),'Material Balance 127-113'!D26,"")` |
| `Total Material Balance` | `E178` | `∅` | `=SUM(F178:L178)` |
| `Total Material Balance` | `H178` | `∅` | `='Material Balance 127-113'!E26` |
| `Total Material Balance` | `I178` | `∅` | `='Material Balance 166'!E23` |
| `Total Material Balance` | `J178` | `∅` | `='Cost Breakdown-Material-F-20'!E79` |
| `Total Material Balance` | `L178` | `∅` | `='Cost Breakdown-Material-122'!E30` |
| `Total Material Balance` | `M178` | `∅` | `=SUM('Material Balance 127-113'!F26,'Material Balance 166'!F23,'Cost Breakdown-Material-F-20'!F79,'Cost Breakdown-Material-122'!F30)` |
| `Total Material Balance` | `P178` | `∅` | `='Material Balance 127-113'!J26` |
| `Total Material Balance` | `Q178` | `∅` | `='Material Balance 166'!J23` |
| `Total Material Balance` | `R178` | `∅` | `='Cost Breakdown-Material-F-20'!J79` |
| `Total Material Balance` | `T178` | `∅` | `='Cost Breakdown-Material-122'!J30` |
| `Total Material Balance` | `W178` | `∅` | `='Material Balance 127-113'!G26` |
| `Total Material Balance` | `X178` | `∅` | `='Material Balance 166'!G23` |
| `Total Material Balance` | `Y178` | `∅` | `='Cost Breakdown-Material-F-20'!G79` |
| `Total Material Balance` | `AA178` | `∅` | `='Cost Breakdown-Material-122'!G30` |
| `Total Material Balance` | `AB178` | `∅` | `=SUM(U178:AA178,AK178)-M178` |
| `Total Material Balance` | `AC178` | `∅` | `=N178-F178` |
| `Total Material Balance` | `AD178` | `∅` | `=O178-G178` |
| `Total Material Balance` | `AE178` | `∅` | `=P178-H178` |
| `Total Material Balance` | `AF178` | `∅` | `=Q178-I178` |
| `Total Material Balance` | `AG178` | `∅` | `=R178-J178` |
| `Total Material Balance` | `AH178` | `∅` | `=S178-K178` |
| `Total Material Balance` | `AI178` | `∅` | `=T178-L178` |
| `Total Material Balance` | `AJ178` | `∅` | `=SUM('Material Balance 127-113'!L26,'Material Balance 166'!L23,'Cost Breakdown-Material-F-20'!L79,'Cost Breakdown-Material-122'!L30)` |
| `Total Material Balance` | `AK178` | `∅` | `=SUM('Material Balance 127-113'!H26,'Material Balance 166'!H23,'Cost Breakdown-Material-F-20'!H79,'Cost Breakdown-Material-122'!H30)` |
| `Total Material Balance` | `AL178` | `∅` | `=SUM(N178:T178,AJ178)-E178` |
| `Total Material Balance` | `AM178` | `∅` | `=SUM(U178:AA178,AK178)-M178` |
| `Total Material Balance` | `AP178` | `∅` | `=AL178+AM178` |
| `Total Material Balance` | `AQ178` | `=-(AP178)*D178` | `=SUM('Material Balance 127-113'!M26,'Material Balance 166'!M23,'Cost Breakdown-Material-F-20'!M79,'Cost Breakdown-Material-122'!M30)` |
| `Total Material Balance` | `D179` | `∅` | `=IF(AND('Cost Breakdown-Material-122'!D31='Cost Breakdown-Material-075'!D34),'Cost Breakdown-Material-075'!D34,"")` |
| `Total Material Balance` | `E179` | `∅` | `=SUM(F179:L179)` |
| `Total Material Balance` | `G179` | `∅` | `='Cost Breakdown-Material-075'!E34` |
| `Total Material Balance` | `L179` | `∅` | `='Cost Breakdown-Material-122'!E31` |
| `Total Material Balance` | `M179` | `∅` | `=SUM('Cost Breakdown-Material-075'!F34,'Cost Breakdown-Material-122'!F31)` |
| `Total Material Balance` | `O179` | `∅` | `='Cost Breakdown-Material-075'!J34` |
| `Total Material Balance` | `T179` | `∅` | `='Cost Breakdown-Material-122'!J31` |
| `Total Material Balance` | `V179` | `∅` | `='Cost Breakdown-Material-075'!G34` |
| `Total Material Balance` | `AA179` | `∅` | `='Cost Breakdown-Material-122'!G31` |
| `Total Material Balance` | `AB179` | `∅` | `=SUM(U179:AA179,AK179)-M179` |
| `Total Material Balance` | `AC179` | `∅` | `=N179-F179` |
| `Total Material Balance` | `AD179` | `∅` | `=O179-G179` |
| `Total Material Balance` | `AE179` | `∅` | `=P179-H179` |
| `Total Material Balance` | `AF179` | `∅` | `=Q179-I179` |
| `Total Material Balance` | `AG179` | `∅` | `=R179-J179` |
| `Total Material Balance` | `AH179` | `∅` | `=S179-K179` |
| `Total Material Balance` | `AI179` | `∅` | `=T179-L179` |
| `Total Material Balance` | `AJ179` | `∅` | `=SUM('Cost Breakdown-Material-075'!L34,'Cost Breakdown-Material-122'!L31)` |
| `Total Material Balance` | `AK179` | `∅` | `=SUM('Cost Breakdown-Material-075'!H34,'Cost Breakdown-Material-122'!H31)` |
| `Total Material Balance` | `AL179` | `∅` | `=SUM(N179:T179,AJ179)-E179` |
| `Total Material Balance` | `AM179` | `∅` | `=SUM(U179:AA179,AK179)-M179` |
| `Total Material Balance` | `AP179` | `∅` | `=AL179+AM179` |
| `Total Material Balance` | `AQ179` | `=-(AP179)*D179` | `=SUM('Cost Breakdown-Material-075'!M34,'Cost Breakdown-Material-122'!M31)` |
| `Total Material Balance` | `D180` | `∅` | `=IF(AND('Cost Breakdown-Material-075'!D35='Cost Breakdown-Material-12'!D21,'Material Balance 127-113'!D27='Cost Breakdown-Material-12'!D21,'Material Balance 166'!D24='Cost Breakdown-Material-12'!D21,'Cost Breakdown-Material-F-20'!D80='Cost Breakdown-Material-12'!D21,'Cost Breakdown-Material-122'!D32='Cost Breakdown-Material-12'!D21),'Cost Breakdown-Material-12'!D21,"")` |
| `Total Material Balance` | `E180` | `∅` | `=SUM(F180:L180)` |
| `Total Material Balance` | `F180` | `∅` | `='Cost Breakdown-Material-12'!E21` |
| `Total Material Balance` | `G180` | `∅` | `='Cost Breakdown-Material-075'!E35` |
| `Total Material Balance` | `H180` | `∅` | `='Material Balance 127-113'!E27` |
| `Total Material Balance` | `I180` | `∅` | `='Material Balance 166'!E24` |
| `Total Material Balance` | `J180` | `∅` | `='Cost Breakdown-Material-F-20'!E80` |
| `Total Material Balance` | `L180` | `∅` | `='Cost Breakdown-Material-122'!E32` |
| `Total Material Balance` | `M180` | `∅` | `=SUM('Cost Breakdown-Material-12'!F21,'Cost Breakdown-Material-075'!F35,'Material Balance 127-113'!F27,'Material Balance 166'!F24,'Cost Breakdown-Material-F-20'!F80,'Cost Breakdown-Material-122'!F32)` |
| `Total Material Balance` | `N180` | `∅` | `='Cost Breakdown-Material-12'!J21` |
| `Total Material Balance` | `O180` | `∅` | `='Cost Breakdown-Material-075'!J35` |
| `Total Material Balance` | `P180` | `∅` | `='Material Balance 127-113'!J27` |
| `Total Material Balance` | `Q180` | `∅` | `='Material Balance 166'!J24` |
| `Total Material Balance` | `R180` | `∅` | `='Cost Breakdown-Material-F-20'!J80` |
| `Total Material Balance` | `T180` | `∅` | `='Cost Breakdown-Material-122'!J32` |
| `Total Material Balance` | `U180` | `∅` | `='Cost Breakdown-Material-12'!G21` |
| `Total Material Balance` | `V180` | `∅` | `='Cost Breakdown-Material-075'!G35` |
| `Total Material Balance` | `W180` | `∅` | `='Material Balance 127-113'!G27` |
| `Total Material Balance` | `X180` | `∅` | `='Material Balance 166'!G24` |
| `Total Material Balance` | `Y180` | `∅` | `='Cost Breakdown-Material-F-20'!G80` |
| `Total Material Balance` | `AA180` | `∅` | `='Cost Breakdown-Material-122'!G32` |
| `Total Material Balance` | `AB180` | `∅` | `=SUM(U180:AA180,AK180)-M180` |
| `Total Material Balance` | `AC180` | `∅` | `=N180-F180` |
| `Total Material Balance` | `AD180` | `∅` | `=O180-G180` |
| `Total Material Balance` | `AE180` | `∅` | `=P180-H180` |
| `Total Material Balance` | `AF180` | `∅` | `=Q180-I180` |
| `Total Material Balance` | `AG180` | `∅` | `=R180-J180` |
| `Total Material Balance` | `AH180` | `∅` | `=S180-K180` |
| `Total Material Balance` | `AI180` | `∅` | `=T180-L180` |
| `Total Material Balance` | `AJ180` | `∅` | `=SUM('Cost Breakdown-Material-12'!L21,'Cost Breakdown-Material-075'!L35,'Material Balance 127-113'!L27,'Material Balance 166'!L24,'Cost Breakdown-Material-F-20'!L80,'Cost Breakdown-Material-122'!L32)` |
| `Total Material Balance` | `AK180` | `∅` | `=SUM('Cost Breakdown-Material-12'!H21,'Cost Breakdown-Material-075'!H35,'Material Balance 127-113'!H27,'Material Balance 166'!H24,'Cost Breakdown-Material-F-20'!H80,'Cost Breakdown-Material-122'!H32)` |
| `Total Material Balance` | `AL180` | `∅` | `=SUM(N180:T180,AJ180)-E180` |
| `Total Material Balance` | `AM180` | `∅` | `=SUM(U180:AA180,AK180)-M180` |
| `Total Material Balance` | `AP180` | `∅` | `=AL180+AM180` |
| `Total Material Balance` | `AQ180` | `=-(AP180)*D180` | `=SUM('Cost Breakdown-Material-12'!M21,'Cost Breakdown-Material-075'!M35,'Material Balance 127-113'!M27,'Material Balance 166'!M24,'Cost Breakdown-Material-F-20'!M80,'Cost Breakdown-Material-122'!M32)` |
| `Total Material Balance` | `D181` | `∅` | `=IF(AND('Cost Breakdown-Material-122'!D33='Cost Breakdown-Material-12'!D22),'Cost Breakdown-Material-12'!D22,"")` |
| `Total Material Balance` | `E181` | `∅` | `=SUM(F181:L181)` |
| `Total Material Balance` | `F181` | `∅` | `='Cost Breakdown-Material-12'!E22` |
| `Total Material Balance` | `L181` | `∅` | `='Cost Breakdown-Material-122'!E33` |
| `Total Material Balance` | `M181` | `∅` | `=SUM('Cost Breakdown-Material-12'!F22,'Cost Breakdown-Material-122'!F33)` |
| `Total Material Balance` | `N181` | `∅` | `='Cost Breakdown-Material-12'!J22` |
| `Total Material Balance` | `T181` | `∅` | `='Cost Breakdown-Material-122'!J33` |
| `Total Material Balance` | `U181` | `∅` | `='Cost Breakdown-Material-12'!G22` |
| `Total Material Balance` | `AA181` | `∅` | `='Cost Breakdown-Material-122'!G33` |
| `Total Material Balance` | `AB181` | `∅` | `=SUM(U181:AA181,AK181)-M181` |
| `Total Material Balance` | `AC181` | `∅` | `=N181-F181` |
| `Total Material Balance` | `AD181` | `∅` | `=O181-G181` |
| `Total Material Balance` | `AE181` | `∅` | `=P181-H181` |
| `Total Material Balance` | `AF181` | `∅` | `=Q181-I181` |
| `Total Material Balance` | `AG181` | `∅` | `=R181-J181` |
| `Total Material Balance` | `AH181` | `∅` | `=S181-K181` |
| `Total Material Balance` | `AI181` | `∅` | `=T181-L181` |
| `Total Material Balance` | `AJ181` | `∅` | `=SUM('Cost Breakdown-Material-12'!L22,'Cost Breakdown-Material-122'!L33)` |
| `Total Material Balance` | `AK181` | `∅` | `=SUM('Cost Breakdown-Material-12'!H22,'Cost Breakdown-Material-122'!H33)` |
| `Total Material Balance` | `AL181` | `∅` | `=SUM(N181:T181,AJ181)-E181` |
| `Total Material Balance` | `AM181` | `∅` | `=SUM(U181:AA181,AK181)-M181` |
| `Total Material Balance` | `AP181` | `∅` | `=AL181+AM181` |
| `Total Material Balance` | `AQ181` | `=-(AP181)*D181` | `=SUM('Cost Breakdown-Material-12'!M22,'Cost Breakdown-Material-122'!M33)` |
| `Total Material Balance` | `D182` | `∅` | `=IF(AND('Cost Breakdown-Material-075'!D36='Cost Breakdown-Material-12'!D23,'Material Balance 127-113'!D28='Cost Breakdown-Material-12'!D23,'Material Balance 166'!D25='Cost Breakdown-Material-12'!D23),'Cost Breakdown-Material-12'!D23,"")` |
| `Total Material Balance` | `E182` | `∅` | `=SUM(F182:L182)` |
| `Total Material Balance` | `F182` | `∅` | `='Cost Breakdown-Material-12'!E23` |
| `Total Material Balance` | `G182` | `∅` | `='Cost Breakdown-Material-075'!E36` |
| `Total Material Balance` | `H182` | `∅` | `='Material Balance 127-113'!E28` |
| `Total Material Balance` | `I182` | `∅` | `='Material Balance 166'!E25` |
| `Total Material Balance` | `M182` | `∅` | `=SUM('Cost Breakdown-Material-12'!F23,'Cost Breakdown-Material-075'!F36,'Material Balance 127-113'!F28,'Material Balance 166'!F25)` |
| `Total Material Balance` | `N182` | `∅` | `='Cost Breakdown-Material-12'!J23` |
| `Total Material Balance` | `O182` | `∅` | `='Cost Breakdown-Material-075'!J36` |
| `Total Material Balance` | `P182` | `∅` | `='Material Balance 127-113'!J28` |
| `Total Material Balance` | `Q182` | `∅` | `='Material Balance 166'!J25` |
| `Total Material Balance` | `U182` | `∅` | `='Cost Breakdown-Material-12'!G23` |
| `Total Material Balance` | `V182` | `∅` | `='Cost Breakdown-Material-075'!G36` |
| `Total Material Balance` | `W182` | `∅` | `='Material Balance 127-113'!G28` |
| `Total Material Balance` | `X182` | `∅` | `='Material Balance 166'!G25` |
| `Total Material Balance` | `AB182` | `∅` | `=SUM(U182:AA182,AK182)-M182` |
| `Total Material Balance` | `AC182` | `∅` | `=N182-F182` |
| `Total Material Balance` | `AD182` | `∅` | `=O182-G182` |
| `Total Material Balance` | `AE182` | `∅` | `=P182-H182` |
| `Total Material Balance` | `AF182` | `∅` | `=Q182-I182` |
| `Total Material Balance` | `AG182` | `∅` | `=R182-J182` |
| `Total Material Balance` | `AH182` | `∅` | `=S182-K182` |
| `Total Material Balance` | `AI182` | `∅` | `=T182-L182` |
| `Total Material Balance` | `AJ182` | `∅` | `=SUM('Cost Breakdown-Material-12'!L23,'Cost Breakdown-Material-075'!L36,'Material Balance 127-113'!L28,'Material Balance 166'!L25)` |
| `Total Material Balance` | `AK182` | `∅` | `=SUM('Cost Breakdown-Material-12'!H23,'Cost Breakdown-Material-075'!H36,'Material Balance 127-113'!H28,'Material Balance 166'!H25)` |
| `Total Material Balance` | `AL182` | `∅` | `=SUM(N182:T182,AJ182)-E182` |
| `Total Material Balance` | `AM182` | `∅` | `=SUM(U182:AA182,AK182)-M182` |
| `Total Material Balance` | `AP182` | `∅` | `=AL182+AM182` |
| `Total Material Balance` | `AQ182` | `=-(AP182)*D182` | `=SUM('Cost Breakdown-Material-12'!M23,'Cost Breakdown-Material-075'!M36,'Material Balance 127-113'!M28,'Material Balance 166'!M25)` |
| `Total Material Balance` | `B183` | `∅` | `26" Rock Bit` |
| `Total Material Balance` | `C183` | `∅` | `each` |
| `Total Material Balance` | `D183` | `∅` | `='Cost Breakdown-Material-F-20'!D72` |
| `Total Material Balance` | `E183` | `∅` | `=SUM(F183:L183)` |
| `Total Material Balance` | `J183` | `∅` | `='Cost Breakdown-Material-F-20'!E72` |
| `Total Material Balance` | `M183` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F72)` |
| `Total Material Balance` | `R183` | `∅` | `='Cost Breakdown-Material-F-20'!J72` |
| `Total Material Balance` | `Y183` | `∅` | `='Cost Breakdown-Material-F-20'!G72` |
| `Total Material Balance` | `AB183` | `∅` | `=SUM(U183:AA183,AK183)-M183` |
| `Total Material Balance` | `AC183` | `∅` | `=N183-F183` |
| `Total Material Balance` | `AD183` | `∅` | `=O183-G183` |
| `Total Material Balance` | `AE183` | `∅` | `=P183-H183` |
| `Total Material Balance` | `AF183` | `∅` | `=Q183-I183` |
| `Total Material Balance` | `AG183` | `∅` | `=R183-J183` |
| `Total Material Balance` | `AH183` | `∅` | `=S183-K183` |
| `Total Material Balance` | `AI183` | `∅` | `=T183-L183` |
| `Total Material Balance` | `AJ183` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L72)` |
| `Total Material Balance` | `AK183` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H72)` |
| `Total Material Balance` | `AL183` | `∅` | `=SUM(N183:T183,AJ183)-E183` |
| `Total Material Balance` | `AM183` | `∅` | `=SUM(U183:AA183,AK183)-M183` |
| `Total Material Balance` | `AP183` | `∅` | `=AL183+AM183` |
| `Total Material Balance` | `AQ183` | `=SUM(AQ173,AQ170,AQ136,AQ132,AQ70,AQ36,AQ10,AQ4)` | `=SUM('Cost Breakdown-Material-F-20'!M72)` |
| `Total Material Balance` | `B184` | `∅` | `17-1/2" Rock Bit` |
| `Total Material Balance` | `C184` | `∅` | `each` |
| `Total Material Balance` | `D184` | `∅` | `='Cost Breakdown-Material-F-20'!D73` |
| `Total Material Balance` | `E184` | `∅` | `=SUM(F184:L184)` |
| `Total Material Balance` | `J184` | `∅` | `='Cost Breakdown-Material-F-20'!E73` |
| `Total Material Balance` | `M184` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F73)` |
| `Total Material Balance` | `R184` | `∅` | `='Cost Breakdown-Material-F-20'!J73` |
| `Total Material Balance` | `Y184` | `∅` | `='Cost Breakdown-Material-F-20'!G73` |
| `Total Material Balance` | `AB184` | `∅` | `=SUM(U184:AA184,AK184)-M184` |
| `Total Material Balance` | `AC184` | `∅` | `=N184-F184` |
| `Total Material Balance` | `AD184` | `∅` | `=O184-G184` |
| `Total Material Balance` | `AE184` | `∅` | `=P184-H184` |
| `Total Material Balance` | `AF184` | `∅` | `=Q184-I184` |
| `Total Material Balance` | `AG184` | `∅` | `=R184-J184` |
| `Total Material Balance` | `AH184` | `∅` | `=S184-K184` |
| `Total Material Balance` | `AI184` | `∅` | `=T184-L184` |
| `Total Material Balance` | `AJ184` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L73)` |
| `Total Material Balance` | `AK184` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H73)` |
| `Total Material Balance` | `AL184` | `∅` | `=SUM(N184:T184,AJ184)-E184` |
| `Total Material Balance` | `AM184` | `∅` | `=SUM(U184:AA184,AK184)-M184` |
| `Total Material Balance` | `AP184` | `=AQ184-AQ183` | `=AL184+AM184` |
| `Total Material Balance` | `AQ184` | `='Cost Breakdown-Material-12'!O14+'Cost Breakdown-Material-075'!N29+'Material Balance 127-113'!N19+'Material Balance 166'!N16+'Cost Breakdown-Material-F-20'!N69+'Cost Breakdown-Material-075 (2'!N21+'Cost Breakdown-Material-122'!N24` | `=SUM('Cost Breakdown-Material-F-20'!M73)` |
| `Total Material Balance` | `B185` | `∅` | `17-1/2" PDC Bit` |
| `Total Material Balance` | `C185` | `∅` | `each` |
| `Total Material Balance` | `D185` | `∅` | `='Cost Breakdown-Material-F-20'!D74` |
| `Total Material Balance` | `E185` | `∅` | `=SUM(F185:L185)` |
| `Total Material Balance` | `J185` | `∅` | `='Cost Breakdown-Material-F-20'!E74` |
| `Total Material Balance` | `M185` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!F74)` |
| `Total Material Balance` | `R185` | `∅` | `='Cost Breakdown-Material-F-20'!J74` |
| `Total Material Balance` | `Y185` | `∅` | `='Cost Breakdown-Material-F-20'!G74` |
| `Total Material Balance` | `AB185` | `∅` | `=SUM(U185:AA185,AK185)-M185` |
| `Total Material Balance` | `AC185` | `∅` | `=N185-F185` |
| `Total Material Balance` | `AD185` | `∅` | `=O185-G185` |
| `Total Material Balance` | `AE185` | `∅` | `=P185-H185` |
| `Total Material Balance` | `AF185` | `∅` | `=Q185-I185` |
| `Total Material Balance` | `AG185` | `∅` | `=R185-J185` |
| `Total Material Balance` | `AH185` | `∅` | `=S185-K185` |
| `Total Material Balance` | `AI185` | `∅` | `=T185-L185` |
| `Total Material Balance` | `AJ185` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!L74)` |
| `Total Material Balance` | `AK185` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!H74)` |
| `Total Material Balance` | `AL185` | `∅` | `=SUM(N185:T185,AJ185)-E185` |
| `Total Material Balance` | `AM185` | `∅` | `=SUM(U185:AA185,AK185)-M185` |
| `Total Material Balance` | `AP185` | `∅` | `=AL185+AM185` |
| `Total Material Balance` | `AQ185` | `∅` | `=SUM('Cost Breakdown-Material-F-20'!M74)` |
| `Total Material Balance` | `B186` | `∅` | `6 1/8" Rock Bit` |
| `Total Material Balance` | `C186` | `∅` | `each` |
| `Total Material Balance` | `D186` | `∅` | `=IF(AND('Cost Breakdown-Material-075 (2'!D26='Cost Breakdown-Material-075'!D33),'Cost Breakdown-Material-075'!D33,"")` |
| `Total Material Balance` | `E186` | `∅` | `=SUM(F186:L186)` |
| `Total Material Balance` | `G186` | `∅` | `='Cost Breakdown-Material-075'!E33` |
| `Total Material Balance` | `K186` | `∅` | `='Cost Breakdown-Material-075 (2'!E26` |
| `Total Material Balance` | `M186` | `∅` | `=SUM('Cost Breakdown-Material-075'!F33,'Cost Breakdown-Material-075 (2'!F26)` |
| `Total Material Balance` | `O186` | `∅` | `='Cost Breakdown-Material-075'!J33` |
| `Total Material Balance` | `S186` | `∅` | `='Cost Breakdown-Material-075 (2'!J26` |
| `Total Material Balance` | `V186` | `∅` | `='Cost Breakdown-Material-075'!G33` |
| `Total Material Balance` | `Z186` | `∅` | `='Cost Breakdown-Material-075 (2'!G26` |
| `Total Material Balance` | `AB186` | `∅` | `=SUM(U186:AA186,AK186)-M186` |
| `Total Material Balance` | `AC186` | `∅` | `=N186-F186` |
| `Total Material Balance` | `AD186` | `∅` | `=O186-G186` |
| `Total Material Balance` | `AE186` | `∅` | `=P186-H186` |
| `Total Material Balance` | `AF186` | `∅` | `=Q186-I186` |
| `Total Material Balance` | `AG186` | `∅` | `=R186-J186` |
| `Total Material Balance` | `AH186` | `∅` | `=S186-K186` |
| `Total Material Balance` | `AI186` | `∅` | `=T186-L186` |
| `Total Material Balance` | `AJ186` | `∅` | `=SUM('Cost Breakdown-Material-075'!L33,'Cost Breakdown-Material-075 (2'!L26)` |
| `Total Material Balance` | `AK186` | `∅` | `=SUM('Cost Breakdown-Material-075'!H33,'Cost Breakdown-Material-075 (2'!H26)` |
| `Total Material Balance` | `AL186` | `∅` | `=SUM(N186:T186,AJ186)-E186` |
| `Total Material Balance` | `AM186` | `∅` | `=SUM(U186:AA186,AK186)-M186` |
| `Total Material Balance` | `AP186` | `∅` | `=AL186+AM186` |
| `Total Material Balance` | `AQ186` | `∅` | `=SUM('Cost Breakdown-Material-075'!M33,'Cost Breakdown-Material-075 (2'!M26)` |
| `Total Material Balance` | `B187` | `∅` | `3-1/8" Mill` |
| `Total Material Balance` | `C187` | `∅` | `each` |
| `Total Material Balance` | `D187` | `∅` | `='Cost Breakdown-Material-122'!D34` |
| `Total Material Balance` | `E187` | `∅` | `=SUM(F187:L187)` |
| `Total Material Balance` | `L187` | `∅` | `='Cost Breakdown-Material-122'!E34` |
| `Total Material Balance` | `M187` | `∅` | `=SUM('Cost Breakdown-Material-122'!F34)` |
| `Total Material Balance` | `T187` | `∅` | `='Cost Breakdown-Material-122'!J34` |
| `Total Material Balance` | `AA187` | `∅` | `='Cost Breakdown-Material-122'!G34` |
| `Total Material Balance` | `AB187` | `∅` | `=SUM(U187:AA187,AK187)-M187` |
| `Total Material Balance` | `AC187` | `∅` | `=N187-F187` |
| `Total Material Balance` | `AD187` | `∅` | `=O187-G187` |
| `Total Material Balance` | `AE187` | `∅` | `=P187-H187` |
| `Total Material Balance` | `AF187` | `∅` | `=Q187-I187` |
| `Total Material Balance` | `AG187` | `∅` | `=R187-J187` |
| `Total Material Balance` | `AH187` | `∅` | `=S187-K187` |
| `Total Material Balance` | `AI187` | `∅` | `=T187-L187` |
| `Total Material Balance` | `AJ187` | `∅` | `=SUM('Cost Breakdown-Material-122'!L34)` |
| `Total Material Balance` | `AK187` | `∅` | `=SUM('Cost Breakdown-Material-122'!H34)` |
| `Total Material Balance` | `AL187` | `∅` | `=SUM(N187:T187,AJ187)-E187` |
| `Total Material Balance` | `AM187` | `∅` | `=SUM(U187:AA187,AK187)-M187` |
| `Total Material Balance` | `AP187` | `∅` | `=AL187+AM187` |
| `Total Material Balance` | `AQ187` | `∅` | `=SUM('Cost Breakdown-Material-122'!M34)` |
| `Total Material Balance` | `B188` | `∅` | `Tubing pup joint, 4 1/2", L-80,Gas Tight  Connection 18.9 ppf, seamless,1.5 m long , PSL3` |
| `Total Material Balance` | `C188` | `∅` | `ea.` |
| `Total Material Balance` | `D188` | `∅` | `='Cost Breakdown-Material-F-20'!D27` |
| `Total Material Balance` | `E188` | `∅` | `=SUM(F188:L188)` |
| `Total Material Balance` | `J188` | `∅` | `='Cost Breakdown-Material-F-20'!E27` |
| `Total Material Balance` | `M188` | `∅` | `='Cost Breakdown-Material-F-20'!F27` |
| `Total Material Balance` | `R188` | `∅` | `='Cost Breakdown-Material-F-20'!J27` |
| `Total Material Balance` | `Y188` | `∅` | `='Cost Breakdown-Material-F-20'!G27` |
| `Total Material Balance` | `AB188` | `∅` | `=SUM(U188:AA188,AK188)-M188` |
| `Total Material Balance` | `AG188` | `∅` | `=R188-J188` |
| `Total Material Balance` | `AJ188` | `∅` | `='Cost Breakdown-Material-F-20'!L27` |
| `Total Material Balance` | `AK188` | `∅` | `='Cost Breakdown-Material-F-20'!H27` |
| `Total Material Balance` | `AL188` | `∅` | `=SUM(N188:T188,AJ188)-E188` |
| `Total Material Balance` | `AM188` | `∅` | `=SUM(U188:AA188,AK188)-M188` |
| `Total Material Balance` | `AP188` | `∅` | `=AL188+AM188` |
| `Total Material Balance` | `AQ188` | `∅` | `='Cost Breakdown-Material-F-20'!M27` |
| `Total Material Balance` | `B189` | `∅` | `Casing, 7", TP110S, 35 ppf, TPCQ, R3` |
| `Total Material Balance` | `C189` | `∅` | `Jt.` |
| `Total Material Balance` | `D189` | `∅` | `='Cost Breakdown-Material-F-20'!D16` |
| `Total Material Balance` | `E189` | `∅` | `=SUM(F189:L189)` |
| `Total Material Balance` | `J189` | `∅` | `='Cost Breakdown-Material-F-20'!E16` |
| `Total Material Balance` | `M189` | `∅` | `='Cost Breakdown-Material-F-20'!F16` |
| `Total Material Balance` | `N189` | `∅` | `=0` |
| `Total Material Balance` | `O189` | `∅` | `=0` |
| `Total Material Balance` | `P189` | `∅` | `=0` |
| `Total Material Balance` | `Q189` | `∅` | `=0` |
| `Total Material Balance` | `R189` | `∅` | `='Cost Breakdown-Material-F-20'!J16` |
| `Total Material Balance` | `S189` | `∅` | `=0` |
| `Total Material Balance` | `T189` | `∅` | `=0` |
| `Total Material Balance` | `U189` | `∅` | `=0` |
| `Total Material Balance` | `V189` | `∅` | `=0` |
| `Total Material Balance` | `W189` | `∅` | `=0` |
| `Total Material Balance` | `X189` | `∅` | `=0` |
| `Total Material Balance` | `Y189` | `∅` | `='Cost Breakdown-Material-F-20'!G16` |
| `Total Material Balance` | `Z189` | `∅` | `=0` |
| `Total Material Balance` | `AA189` | `∅` | `=0` |
| `Total Material Balance` | `AB189` | `∅` | `=SUM(U189:AA189,AK189)-M189` |
| `Total Material Balance` | `AC189` | `∅` | `=N189-F189` |
| `Total Material Balance` | `AD189` | `∅` | `=O189-G189` |
| `Total Material Balance` | `AE189` | `∅` | `=P189-H189` |
| `Total Material Balance` | `AF189` | `∅` | `=Q189-I189` |
| `Total Material Balance` | `AG189` | `∅` | `=R189-J189` |
| `Total Material Balance` | `AH189` | `∅` | `=S189-K189` |
| `Total Material Balance` | `AI189` | `∅` | `=T189-L189` |
| `Total Material Balance` | `AJ189` | `∅` | `='Cost Breakdown-Material-F-20'!L16` |
| `Total Material Balance` | `AK189` | `∅` | `='Cost Breakdown-Material-F-20'!H16` |
| `Total Material Balance` | `AL189` | `∅` | `=SUM(N189:T189,AJ189)-E189` |
| `Total Material Balance` | `AM189` | `∅` | `=SUM(U189:AA189,AK189)-M189` |
| `Total Material Balance` | `AP189` | `∅` | `=AL189+AM189` |
| `Total Material Balance` | `AQ189` | `∅` | `='Cost Breakdown-Material-F-20'!M16` |
| `Total Material Balance` | `B190` | `∅` | `Centralizer, Bow type, 7" x 8-3/8", Non-welded` |
| `Total Material Balance` | `C190` | `∅` | `ea.` |
| `Total Material Balance` | `D190` | `∅` | `='Cost Breakdown-Material-F-20'!D46` |
| `Total Material Balance` | `E190` | `∅` | `=SUM(F190:L190)` |
| `Total Material Balance` | `J190` | `∅` | `='Cost Breakdown-Material-F-20'!E46` |
| `Total Material Balance` | `M190` | `∅` | `='Cost Breakdown-Material-F-20'!F46` |
| `Total Material Balance` | `N190` | `∅` | `=0` |
| `Total Material Balance` | `O190` | `∅` | `=0` |
| `Total Material Balance` | `P190` | `∅` | `=0` |
| `Total Material Balance` | `Q190` | `∅` | `=0` |
| `Total Material Balance` | `R190` | `∅` | `='Cost Breakdown-Material-F-20'!J46` |
| `Total Material Balance` | `S190` | `∅` | `=0` |
| `Total Material Balance` | `T190` | `∅` | `=0` |
| `Total Material Balance` | `U190` | `∅` | `=0` |
| `Total Material Balance` | `V190` | `∅` | `=0` |
| `Total Material Balance` | `W190` | `∅` | `=0` |
| `Total Material Balance` | `X190` | `∅` | `=0` |
| `Total Material Balance` | `Y190` | `∅` | `='Cost Breakdown-Material-F-20'!G46` |
| `Total Material Balance` | `Z190` | `∅` | `=0` |
| `Total Material Balance` | `AA190` | `∅` | `=0` |
| `Total Material Balance` | `AB190` | `∅` | `=SUM(U190:AA190,AK190)-M190` |
| `Total Material Balance` | `AC190` | `∅` | `=N190-F190` |
| `Total Material Balance` | `AD190` | `∅` | `=O190-G190` |
| `Total Material Balance` | `AE190` | `∅` | `=P190-H190` |
| `Total Material Balance` | `AF190` | `∅` | `=Q190-I190` |
| `Total Material Balance` | `AG190` | `∅` | `=R190-J190` |
| `Total Material Balance` | `AH190` | `∅` | `=S190-K190` |
| `Total Material Balance` | `AI190` | `∅` | `=T190-L190` |
| `Total Material Balance` | `AJ190` | `∅` | `='Cost Breakdown-Material-F-20'!L46` |
| `Total Material Balance` | `AK190` | `∅` | `='Cost Breakdown-Material-F-20'!H46` |
| `Total Material Balance` | `AL190` | `∅` | `=SUM(N190:T190,AJ190)-E190` |
| `Total Material Balance` | `AM190` | `∅` | `=SUM(U190:AA190,AK190)-M190` |
| `Total Material Balance` | `AP190` | `∅` | `=AL190+AM190` |
| `Total Material Balance` | `AQ190` | `∅` | `='Cost Breakdown-Material-F-20'!M46` |
| `Total Material Balance` | `B191` | `∅` | `Drift Gauge, API, for 7" 35# casing` |
| `Total Material Balance` | `C191` | `∅` | `ea.` |
| `Total Material Balance` | `D191` | `∅` | `='Cost Breakdown-Material-F-20'!D59` |
| `Total Material Balance` | `E191` | `∅` | `=SUM(F191:L191)` |
| `Total Material Balance` | `J191` | `∅` | `='Cost Breakdown-Material-F-20'!E59` |
| `Total Material Balance` | `M191` | `∅` | `='Cost Breakdown-Material-F-20'!F59` |
| `Total Material Balance` | `N191` | `∅` | `=0` |
| `Total Material Balance` | `O191` | `∅` | `=0` |
| `Total Material Balance` | `P191` | `∅` | `=0` |
| `Total Material Balance` | `Q191` | `∅` | `=0` |
| `Total Material Balance` | `R191` | `∅` | `='Cost Breakdown-Material-F-20'!J59` |
| `Total Material Balance` | `S191` | `∅` | `=0` |
| `Total Material Balance` | `T191` | `∅` | `=0` |
| `Total Material Balance` | `U191` | `∅` | `=0` |
| `Total Material Balance` | `V191` | `∅` | `=0` |
| `Total Material Balance` | `W191` | `∅` | `=0` |
| `Total Material Balance` | `X191` | `∅` | `=0` |
| `Total Material Balance` | `Y191` | `∅` | `='Cost Breakdown-Material-F-20'!G59` |
| `Total Material Balance` | `Z191` | `∅` | `=0` |
| `Total Material Balance` | `AA191` | `∅` | `=0` |
| `Total Material Balance` | `AB191` | `∅` | `=SUM(U191:AA191,AK191)-M191` |
| `Total Material Balance` | `AC191` | `∅` | `=N191-F191` |
| `Total Material Balance` | `AD191` | `∅` | `=O191-G191` |
| `Total Material Balance` | `AE191` | `∅` | `=P191-H191` |
| `Total Material Balance` | `AF191` | `∅` | `=Q191-I191` |
| `Total Material Balance` | `AG191` | `∅` | `=R191-J191` |
| `Total Material Balance` | `AH191` | `∅` | `=S191-K191` |
| `Total Material Balance` | `AI191` | `∅` | `=T191-L191` |
| `Total Material Balance` | `AJ191` | `∅` | `='Cost Breakdown-Material-F-20'!L59` |
| `Total Material Balance` | `AK191` | `∅` | `='Cost Breakdown-Material-F-20'!H59` |
| `Total Material Balance` | `AL191` | `∅` | `=SUM(N191:T191,AJ191)-E191` |
| `Total Material Balance` | `AM191` | `∅` | `=SUM(U191:AA191,AK191)-M191` |
| `Total Material Balance` | `AP191` | `∅` | `=AL191+AM191` |
| `Total Material Balance` | `AQ191` | `∅` | `='Cost Breakdown-Material-F-20'!M59` |
| `Total Material Balance` | `AP192` | `∅` | `Variance: source total less item rollup` |
| `Total Material Balance` | `AQ192` | `∅` | `=SUM(AQ173,AQ170,AQ136,AQ132,AQ70,AQ36,AQ10,AQ4)` |
| `Total Material Balance` | `AP193` | `∅` | `=AQ193-AQ192` |
| `Total Material Balance` | `AQ193` | `∅` | `='Cost Breakdown-Material-12'!O14+'Cost Breakdown-Material-075'!N29+'Material Balance 127-113'!N19+'Material Balance 166'!N16+'Cost Breakdown-Material-F-20'!N69+'Cost Breakdown-Material-075 (2'!N21+'Cost Breakdown-Material-122'!N24` |
| `Total Material Balance` | `B194` | `∅` | `Change Tracking Legend` |
| `Total Material Balance` | `B195` | `∅` | `Light yellow fill = Corrected or modified cell` |
| `Total Material Balance` | `B196` | `∅` | `No light-yellow tracking fill = Original, unchanged data cell` |
| `Cost Breakdown-Material-12` | `O14` | `=SUM(M5,M8,M14)` | `=M24` |
| `Cost Breakdown-Material-075` | `N29` | `=SUM(M5,M12,M22,M24,M29)` | `=M37` |
| `Material Balance 127-113` | `N19` | `=SUM(M5,M7,M11,M19)` | `=M29` |
| `Material Balance 166` | `N16` | `=SUM(M5,M8,M16)` | `=M26` |
| `Cost Breakdown-Material-F-20` | `I6` | `=G6-F6` | `=(H6+G6)-F6` |
| `Cost Breakdown-Material-F-20` | `K6` | `=J6-E6` | `=(J6+L6)-E6` |
| `Cost Breakdown-Material-F-20` | `M6` | `0` | `=-(K6)*D6` |
| `Cost Breakdown-Material-F-20` | `I9` | `0` | `=(H9+G9)-F9` |
| `Cost Breakdown-Material-F-20` | `I10` | `0` | `=(H10+G10)-F10` |
| `Cost Breakdown-Material-F-20` | `I11` | `0` | `=(H11+G11)-F11` |
| `Cost Breakdown-Material-F-20` | `I12` | `0` | `=(H12+G12)-F12` |
| `Cost Breakdown-Material-F-20` | `I14` | `0` | `=(H14+G14)-F14` |
| `Cost Breakdown-Material-F-20` | `I15` | `0` | `=(H15+G15)-F15` |
| `Cost Breakdown-Material-F-20` | `I16` | `0` | `=(H16+G16)-F16` |
| `Cost Breakdown-Material-F-20` | `K16` | `0` | `=(J16+L16)-E16` |
| `Cost Breakdown-Material-F-20` | `M16` | `0` | `=-(K16)*D16` |
| `Cost Breakdown-Material-F-20` | `K46` | `0` | `=(J46+L46)-E46` |
| `Cost Breakdown-Material-F-20` | `M46` | `0` | `=-(K46)*D46` |
| `Cost Breakdown-Material-F-20` | `K59` | `0` | `=(J59+L59)-E59` |
| `Cost Breakdown-Material-F-20` | `M59` | `0` | `=-(K59)*D59` |
| `Cost Breakdown-Material-F-20` | `N69` | `=SUM(M69,M62,M29,M13,M7)` | `=M81` |
| `Cost Breakdown-Material-075 (2` | `N21` | `=SUM(M5,M12,M14,M21)` | `=M27` |
| `Cost Breakdown-Material-075 (2` | `K112` | `='Cost Breakdown-Material-075 (2'!E17q` | `∅` |
| `Cost Breakdown-Material-122` | `N24` | `=SUM(M5,M7,M13,M22,M24)` | `=M35` |
| `Cost Breakdown-Material-122` | `I30` | `0` | `=(H30+G30)-F30` |

## ۸. فایل‌های تحویل و وضعیت مخزن

- فایل اصلی، دست‌نخورده: `08. Total Material Balance OEOC-31.xlsx` (blob اصلی Git: `fe9757e5961290390e64837179f9944212c33566`).
- Workbook اصلاح‌شده: `Balance_of_Goods_Audited_and_Corrected.xlsx`.
- این گزارش: `Balance_of_Goods_Audit_Report_FA.md`.
- شاخه کاری: `arena/dc3e69e5-balace4-1`.
