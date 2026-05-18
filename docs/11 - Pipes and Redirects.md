# 11 — Pipes and Redirects (الأنابيب وإعادة التوجيه)

> **السابق:** [10 - File Ownership and Permissions](10 - File Ownership and Permissions.md)

---

## 1. المفهوم الأساسي

في Linux، كل أمر له:
- **Standard Input (stdin):** مصدر البيانات (عادةً الكيبورد).
- **Standard Output (stdout):** وجهة الخروج (عادةً الشاشة).
- **Standard Error (stderr):** وجهة الأخطاء (عادةً الشاشة).

```
[Keyboard] → stdin → [Command] → stdout → [Screen]
                              → stderr → [Screen]
```

الـ **Redirect** يغير هذه الاتجاهات، والـ **Pipe** يربط أوامر ببعضها.

---

## 2. Output Redirect (إعادة توجيه الخرج)

### `>` — كتابة لملف (تستبدل المحتوى)
```bash
echo "Hello World" > file.txt      # إنشاء/استبدال محتوى file.txt
ls -la > listing.txt               # حفظ نتيجة ls في ملف
```

> [!warning] **`>` يحذف المحتوى القديم!**
> إذا كان الملف موجوداً، سيُحذف محتواه ويُستبدل. استخدم `>>` إذا أردت الإضافة.

### `>>` — إضافة لملف (Append)
```bash
echo "New line" >> file.txt        # إضافة سطر بدون حذف القديم
date >> log.txt                    # إضافة التاريخ لنهاية الملف
```

---

## 3. Error Redirect

```bash
command 2> error.log              # توجيه الأخطاء فقط لملف
command 2>> error.log             # إضافة الأخطاء للملف
command > output.txt 2> error.log # الخرج لملف والأخطاء لملف آخر
command > all.txt 2>&1            # الخرج والأخطاء معاً لنفس الملف
command &> all.txt                # نفس الشيء (اختصار)
```

> [!info] **الأرقام:**
> - `0` = stdin | `1` = stdout | `2` = stderr
> - `2>&1` = وجّه stderr لنفس وجهة stdout

---

## 4. Input Redirect (إعادة توجيه الدخل)

```bash
command < input.txt               # الأمر يقرأ من الملف بدلاً من الكيبورد
mysql -u root -p database < dump.sql  # مثال شائع جداً
```

---

## 5. الـ Pipe `|` — ربط الأوامر

> [!info] **Pipe (الأنبوب)**
> يأخذ **خرج (stdout)** أمر ويجعله **دخل (stdin)** للأمر التالي.
> ```
> command1 | command2 | command3
> ```

### أمثلة عملية:

```bash
# عرض الملفات وتصفيتها
ls -la | grep ".txt"

# عرض أول 10 عمليات من الأكثر استهلاكاً للـ CPU
ps aux | sort -k3 -rn | head -10

# عد عدد الملفات في المجلد
ls | wc -l

# البحث في الـ History
history | grep "apt install"

# عرض مستخدمين معينين من /etc/passwd
cat /etc/passwd | grep "/bin/bash"

# فلترة الـ Logs
cat /var/log/syslog | grep "error" | tail -20
```

---

## 6. أوامر مفيدة مع الـ Pipes

### `wc` — Word Count (عداد)
```bash
wc -l file.txt          # عدد الأسطر
wc -w file.txt          # عدد الكلمات
wc -c file.txt          # عدد الأحرف
ls | wc -l              # عدد الملفات في المجلد
```

### `sort` — ترتيب
```bash
sort file.txt           # ترتيب أبجدي
sort -n file.txt        # ترتيب رقمي
sort -r file.txt        # ترتيب عكسي
sort -u file.txt        # ترتيب + حذف المكرر
```

### `uniq` — حذف المكرر
```bash
sort file.txt | uniq           # حذف الأسطر المكررة
sort file.txt | uniq -c        # عداد التكرار
```

### `tee` — الإرسال للشاشة والملف معاً
```bash
ls -la | tee listing.txt       # يعرض على الشاشة ويحفظ في الملف
command | tee -a log.txt       # نفس الشيء مع Append
```

### `/dev/null` — سلة المهملات
```bash
command > /dev/null 2>&1       # تجاهل كل الخرج والأخطاء
command 2> /dev/null           # تجاهل الأخطاء فقط
```

> [!lightbulb] **`/dev/null` ببساطة:**
> ملف خاص يبتلع كل ما يُكتب فيه. مفيد لإخفاء الخرج غير المطلوب.

---

## 7. مثال عملي شامل

```bash
# سيناريو: أريد معرفة أكثر 5 ملفات حجماً في المجلد الحالي
ls -lS | head -6

# سيناريو: البحث عن كلمة "error" في الـ Logs وحفظ النتيجة
grep -i "error" /var/log/syslog | tail -50 > errors.txt

# سيناريو: عدد المستخدمين الذين لديهم /bin/bash
cat /etc/passwd | grep "/bin/bash" | wc -l

# سيناريو: عرض العمليات الجارية وفلترة برنامج معين
ps aux | grep nginx
```

---

## 8. ملخص الـ Redirects والـ Pipes

| الرمز | الوظيفة |
|-------|---------|
| `>` | خرج لملف (يستبدل) |
| `>>` | خرج لملف (يضيف) |
| `<` | دخل من ملف |
| `2>` | أخطاء لملف |
| `2>&1` | أخطاء + خرج معاً |
| `\|` | ربط أمرين (Pipe) |
| `\| tee file` | خرج للشاشة والملف معاً |
| `> /dev/null` | تجاهل الخرج |

---

## 9. ما التالي؟ 

> [!lightbulb] **الخطوات القادمة بعد هذه المحاضرات:**
> - **Shell Scripting (Bash Scripting):** كتابة سكريبتات لأتمتة المهام.
> - **Ansible:** أداة قوية لأتمتة إدارة السيرفرات.
> - **SSH:** الاتصال بالسيرفرات عن بُعد.
> - **Cron Jobs:** جدولة المهام التلقائية.

---



---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
