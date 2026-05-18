# 04 — Linux File System (نظام الملفات في Linux)

> **السابق:** [03 - Setup Linux Virtual Machine](03 - Setup Linux Virtual Machine.md) | **التالي:** [05 - GUI Vs Command Line Interface](05 - GUI Vs Command Line Interface.md)

---

## 1. الفكرة الأساسية

> [!info] **Linux File System**
> في Linux، **كل شيء ملف (Everything is a File)** — سواء كان مستنداً، مجلداً، جهازاً (كالطابعة)، أو حتى العمليات الجارية — كلها تُعامَل كملفات.

- الـ File System في Linux يبدأ من نقطة واحدة تسمى **Root** ويُرمز لها بـ `/`.
- لا يوجد `C:\` أو `D:\` كما في Windows. كل شيء تحت `/`.

---

## 2. شجرة نظام الملفات

```
/ (Root — الجذر)
 bin/       ← أوامر أساسية للمستخدمين
 sbin/      ← أوامر للـ System Admin فقط
 etc/       ← ملفات الإعدادات (Config files)
 home/      ← مجلدات المستخدمين الشخصية
    ahmed/ ← مجلد المستخدم "ahmed"
 root/      ← المجلد الشخصي لـ Root User
 var/       ← ملفات متغيرة (Logs, Cache...)
 tmp/       ← ملفات مؤقتة (تُحذف عند الإقلاع)
 usr/       ← البرامج المثبتة للمستخدمين
 lib/       ← مكتبات النظام (Libraries)
 dev/       ← ملفات الأجهزة (Devices)
 proc/      ← معلومات العمليات الجارية (في RAM)
 mnt/       ← نقاط تحميل الأقراص الخارجية
 opt/       ← برامج اختيارية من طرف ثالث
 boot/      ← ملفات الإقلاع (Kernel + GRUB)
```

---

## 3. شرح أهم المجلدات

### `/` — Root
> [!info] **Root Directory**
> أعلى نقطة في شجرة الملفات. **كل شيء** ينبثق منها. لا تخلطها مع `/root` (مجلد مستخدم الـ root).

### `/home` — مجلدات المستخدمين
- كل مستخدم عنده مجلد خاص: `/home/username`
- فيه ملفاته، إعداداته الشخصية، وسطح مكتبه.
- الـ **Tilde `~`** اختصار لمجلد الـ Home الخاص بك.

```bash
cd ~        # = cd /home/ahmed (مثلاً)
echo $HOME  # /home/ahmed
```

### `/etc` — ملفات الإعدادات
> [!lightbulb] **تذكّر:** `etc` = "Editable Text Configuration"
> - `/etc/passwd` ← قائمة المستخدمين.
> - `/etc/fstab` ← إعدادات الـ Disks والـ Mount.
> - `/etc/hosts` ← ملف الـ DNS المحلي.
> - `/etc/apt/` ← إعدادات الـ Package Manager.

### `/var` — البيانات المتغيرة
- `/var/log/` ← ملفات الـ **Logs** (سجلات النظام).
- `/var/www/` ← ملفات مواقع الويب عادةً.

### `/tmp` — الملفات المؤقتة
> [!warning] **تنبيه:** الملفات في `/tmp` تُحذف تلقائياً عند إعادة التشغيل. لا تحفظ فيه شيء مهم!

### `/dev` — الأجهزة
- كل جهاز متصل له ملف هنا.
- `/dev/sda` ← أول Hard Disk.
- `/dev/sda1` ← أول Partition في الـ Disk.
- `/dev/null` ← "سلة المهملات" الافتراضية.

### `/proc` — العمليات الجارية
> [!lightbulb] **مجلد وهمي في الـ RAM!**
> `/proc` مش موجود على الـ Disk فعلياً، بيتولد في الذاكرة. فيه معلومات مباشرة عن الـ Processes الشغّالة.
> ```bash
> cat /proc/cpuinfo   # معلومات الـ CPU
> cat /proc/meminfo   # معلومات الـ RAM
> ```

---

## 4. مفاهيم مهمة

### Absolute Path vs Relative Path

> [!info] **Absolute Path (المسار المطلق)**
> المسار الكامل من الـ Root. **دايماً يبدأ بـ `/`**
> ```
> /home/ahmed/documents/file.txt
> ```

> [!info] **Relative Path (المسار النسبي)**
> المسار نسبةً لمكانك الحالي. **لا يبدأ بـ `/`**
> ```
> documents/file.txt   ← لو أنت في /home/ahmed
> ```

### الرموز الخاصة في المسارات

| الرمز | المعنى |
|-------|--------|
| `/` | Root Directory أو فاصل بين المجلدات |
| `~` | Home Directory الخاص بالمستخدم |
| `.` | المجلد الحالي (Current Directory) |
| `..` | المجلد الأب (Parent Directory) |

---

## 5. أنواع الملفات في Linux

> [!info] **Linux File Types:**

| الرمز | النوع |
|-------|-------|
| `-` | Regular File (ملف عادي) |
| `d` | Directory (مجلد) |
| `l` | Symbolic Link (اختصار/رابط) |
| `b` | Block Device (هارد ديسك...) |
| `c` | Character Device (كيبورد، موس...) |

---

## 6. ملخص سريع

| المجلد | الوظيفة |
|--------|---------|
| `/` | جذر كل شيء |
| `/home` | مجلدات المستخدمين |
| `/etc` | ملفات الإعدادات |
| `/var/log` | السجلات والـ Logs |
| `/tmp` | ملفات مؤقتة |
| `/dev` | الأجهزة |
| `/proc` | معلومات العمليات (في RAM) |

---

>  **التالي:** [05 - GUI Vs Command Line Interface](05 - GUI Vs Command Line Interface.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
