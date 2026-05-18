# 06 — Basic Linux Commands (الأوامر الأساسية)

> **السابق:** [05 - GUI Vs Command Line Interface](05 - GUI Vs Command Line Interface.md) | **التالي:** [07 - How to Install Software in Linux](07 - How to Install Software in Linux.md)

---

## 1. هيكل الأمر (Command Structure)

```
command   [options]   [arguments]
                         
                          على ماذا؟ (الملف أو المجلد)
              كيف؟ (تعديل السلوك)
    ماذا تفعل؟
```

**مثال:**
```bash
ls   -la   /home/ahmed
             
              المجلد المستهدف
      خيارات: l=تفاصيل, a=الملفات المخفية
  أمر: اعرض محتويات المجلد
```

---

## 2. أوامر التنقل (Navigation)

### `pwd` — Print Working Directory
```bash
pwd
# Output: /home/ahmed
```
> اعرف فين أنت الآن في شجرة الملفات.

### `ls` — List (عرض المحتويات)
```bash
ls              # عرض المحتويات بشكل بسيط
ls -l           # عرض تفصيلي (long format)
ls -a           # عرض الملفات المخفية (المبدوءة بنقطة)
ls -la          # تفصيلي + المخفية معاً
ls -lh          # مع أحجام مقروءة (K, M, G)
ls /etc         # عرض محتويات مجلد معين
```

> [!lightbulb] **الملفات المخفية في Linux**
> أي ملف اسمه يبدأ بـ `.` يكون مخفياً. مثل: `.bashrc`, `.ssh`  
> لا علاقة له بـ "مخفي" في Windows. ببساطة يبدأ اسمه بنقطة.

### `cd` — Change Directory
```bash
cd /home/ahmed        # انتقل لمسار محدد (Absolute)
cd Documents          # انتقل لمجلد داخل الحالي (Relative)
cd ..                 # ارجع للمجلد الأب
cd ~                  # اذهب للـ Home
cd -                  # ارجع للمجلد السابق
```

---

## 3. أوامر الملفات والمجلدات

### `mkdir` — Make Directory
```bash
mkdir myfolder                    # إنشاء مجلد
mkdir -p parent/child/grandchild  # إنشاء مجلدات متداخلة دفعة واحدة
```

### `touch` — إنشاء ملف فارغ / تحديث timestamp
```bash
touch file.txt          # إنشاء ملف فارغ
touch file1 file2 file3 # إنشاء أكثر من ملف
```

### `cp` — Copy
```bash
cp file.txt /home/ahmed/backup/       # نسخ ملف
cp -r myfolder/ /home/ahmed/backup/   # نسخ مجلد كامل (-r = recursive)
```

### `mv` — Move / Rename
```bash
mv file.txt /home/ahmed/Documents/   # نقل ملف
mv oldname.txt newname.txt           # تغيير الاسم
```

### `rm` — Remove
```bash
rm file.txt         # حذف ملف
rm -r myfolder/     # حذف مجلد وكل محتوياته
rm -f file.txt      # حذف قسري بدون تأكيد (-f = force)
rm -rf myfolder/    # حذف مجلد كامل بدون تأكيد 
```

> [!warning] ** `rm -rf` خطير جداً!**
> لا يوجد "سلة محذوفات" في CLI! الحذف نهائي فوري.  
> `rm -rf /` = حذف كل شيء في النظام! لا تجرّبها أبداً.

---

## 4. أوامر عرض محتوى الملفات

### `cat` — Concatenate (عرض المحتوى)
```bash
cat file.txt          # عرض المحتوى كامل
cat file1 file2       # عرض ملفين متتاليين
```

### `less` — عرض الملفات الطويلة (صفحة بصفحة)
```bash
less /var/log/syslog
# التنقل: Space للأمام | b للخلف | q للخروج | /كلمة للبحث
```

### `head` و `tail` — أول وآخر سطور
```bash
head -n 10 file.txt    # أول 10 أسطر
tail -n 10 file.txt    # آخر 10 أسطر
tail -f /var/log/syslog # متابعة الـ Log مباشرة (مفيد!)
```

> [!lightbulb] **`tail -f` مفيد جداً للـ Monitoring!**
> بيعرض آخر أسطر الـ Log ويتحدث لحظة بلحظة. مفيد لمتابعة الـ Logs في الـ Production.

---

## 5. أوامر البحث

### `find` — البحث عن الملفات
```bash
find /home -name "file.txt"           # بحث بالاسم
find /home -name "*.txt"              # بحث بالامتداد
find / -type d -name "config"         # بحث عن مجلد اسمه config
find /home -size +100M                # ملفات أكبر من 100MB
```

### `grep` — البحث داخل الملفات
```bash
grep "error" /var/log/syslog          # ابحث عن كلمة error
grep -i "error" file.txt              # بحث غير حساس لحالة الأحرف
grep -r "TODO" /home/ahmed/projects/  # بحث في كل الملفات (recursive)
grep -n "error" file.txt              # اعرض رقم السطر
```

---

## 6. أوامر النظام المفيدة

```bash
clear           # تنظيف الشاشة (أو Ctrl+L)
history         # عرض سجل الأوامر السابقة
!!              # إعادة آخر أمر
!n              # تشغيل الأمر رقم n من الـ history
whoami          # من أنا؟ (اسم المستخدم الحالي)
hostname        # اسم الجهاز
date            # التاريخ والوقت الحالي
uptime          # منذ متى الجهاز شغّال
uname -a        # معلومات النظام والـ Kernel
```

---

## 7. اختصارات الـ Terminal المهمة

| الاختصار | الوظيفة |
|----------|---------|
| `Tab` | إكمال الأمر أو اسم الملف تلقائياً |
| `Ctrl + C` | إيقاف الأمر الجاري |
| `Ctrl + Z` | إيقاف مؤقت (Background) |
| `Ctrl + L` | مسح الشاشة |
| `Ctrl + A` | الذهاب لأول السطر |
| `Ctrl + E` | الذهاب لآخر السطر |
| `↑ / ↓` | التنقل في سجل الأوامر |

---

## 8. الـ Manual (دليل الأوامر)

```bash
man ls          # دليل أمر ls الكامل
man grep
# التنقل: مثل less — Space, b, q
```

> [!lightbulb] **`man` = مرجعك الأول!**
> أي أمر مش عارف خياراته؟ اكتب `man command` وهتلاقي كل شيء.

---

## 9. ملخص الأوامر

| الأمر | الوظيفة |
|-------|---------|
| `pwd` | مكانك الحالي |
| `ls` | محتويات المجلد |
| `cd` | التنقل |
| `mkdir` | إنشاء مجلد |
| `touch` | إنشاء ملف |
| `cp` | نسخ |
| `mv` | نقل / إعادة تسمية |
| `rm` | حذف |
| `cat` | عرض ملف |
| `grep` | بحث في ملفات |
| `find` | بحث عن ملفات |
| `man` | دليل الأوامر |

---

>  **التالي:** [07 - How to Install Software in Linux](07 - How to Install Software in Linux.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
