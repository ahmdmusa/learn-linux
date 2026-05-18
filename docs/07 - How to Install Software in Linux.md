
# 07 — How to Install Software in Linux (تثبيت البرامج)
> **السابق:** [06 - Basic Linux Commands](06 - Basic Linux Commands.md) | **التالي:** [08 - Vi and Vim Text Editors](08 - Vi and Vim Text Editors.md)

---

## 1. طرق التثبيت في Linux

```
طرق التثبيت

 Package Manager (apt, yum, dnf...)  ← الأسهل والأفضل
 Snap / Flatpak                       ← تنسيقات حديثة
 تثبيت من Source Code                ← للمتقدمين
 تنزيل مباشر (.deb, .rpm)           ← مشابه لـ .exe في Windows
```

---

## 2. Package Manager — المدير الذهبي

> [!info] **Package Manager (مدير الحزم)**
> برنامج يتحكم في تثبيت وتحديث وحذف البرامج تلقائياً. يتعامل مع التبعيات **(Dependencies)** بنفسه.

> [!info] **Dependencies (التبعيات)**
> البرامج التي يحتاجها البرنامج الذي تريد تثبيته ليعمل. الـ Package Manager يثبّتها تلقائياً بدلاً منك.

### الـ Package Managers حسب التوزيعة

| التوزيعة | Package Manager | الأمر الأساسي |
|----------|----------------|---------------|
| Ubuntu / Debian | **APT** | `apt` |
| CentOS / RHEL | **YUM / DNF** | `yum` أو `dnf` |
| Arch Linux | **Pacman** | `pacman` |
| openSUSE | **Zypper** | `zypper` |

---

## 3. APT — Advanced Package Tool (أوامر Ubuntu)

### التحديث أولاً!
```bash
sudo apt update        # تحديث قائمة الـ Packages المتاحة (لا يثبّت شيء)
sudo apt upgrade       # تثبيت التحديثات الفعلية
```

> [!warning] **فرق مهم: `update` vs `upgrade`**
> - `apt update` ← يحدّث **قائمة** البرامج المتاحة فقط. لا يغيّر أي برنامج.
> - `apt upgrade` ← يثبّت **التحديثات** الفعلية.
> **دايماً** افعل `update` قبل `upgrade` أو تثبيت أي برنامج.

### التثبيت والحذف
```bash
sudo apt install nginx         # تثبيت برنامج
sudo apt install git curl wget # تثبيت أكثر من برنامج
sudo apt remove nginx          # حذف برنامج
sudo apt purge nginx           # حذف البرنامج + إعداداته
sudo apt autoremove            # حذف الـ Dependencies غير المستخدمة
```

### البحث والمعلومات
```bash
apt search nginx               # بحث عن برنامج
apt show nginx                 # معلومات تفصيلية عن الـ Package
apt list --installed           # قائمة البرامج المثبتة
```

---

## 4. تثبيت ملف .deb مباشرة

> [!info] **ملف .deb**
> تنسيق الـ Package في Ubuntu/Debian. مشابه لملف `.exe` في Windows لكن يختلف في آلية التشغيل.

```bash
# تحميل ملف .deb ثم تثبيته
sudo dpkg -i package-name.deb

# لو في مشكلة dependencies:
sudo apt install -f
```

---

## 5. Snap Packages

> [!info] **Snap**
> تنسيق حديث من Canonical (شركة Ubuntu). الـ Package يحتوي على كل ما يحتاجه من تبعيات داخله.

**المزايا:**
- يعمل على أي توزيعة Linux.
- التحديث تلقائي.
- آمن (Sandboxed).

**العيوب:**
- أحياناً أبطأ في التشغيل.
- يأخذ مساحة أكبر.

```bash
sudo snap install code         # تثبيت VS Code مثلاً
sudo snap list                 # قائمة الـ Snaps المثبتة
sudo snap remove code          # حذف
```

---

## 6. التثبيت من Source Code

> [!lightbulb] **متى تثبّت من Source Code؟**
> - البرنامج غير متاح في الـ Package Manager.
> - تريد إصداراً محدداً أو مُخصَّص.
> - للتطوير والمساهمة.

```bash
# الخطوات الأساسية:
git clone https://github.com/project/repo.git
cd repo
./configure          # إعداد بيئة التثبيت
make                 # بناء البرنامج (Compile)
sudo make install    # التثبيت
```

> [!warning] **التثبيت من Source أصعب!**
> قد تحتاج تثبيت أدوات البناء أولاً:
> ```bash
> sudo apt install build-essential
> ```

---

## 7. ملخص سريع

| الطريقة | الأمر | متى؟ |
|---------|-------|------|
| APT (الموصى به) | `sudo apt install برنامج` | معظم الوقت |
| Snap | `sudo snap install برنامج` | برامج حديثة |
| .deb | `sudo dpkg -i file.deb` | ملفات محملة يدوياً |
| Source | `make && make install` | حالات خاصة |

---

>  **التالي:** [08 - Vi and Vim Text Editors](08 - Vi and Vim Text Editors.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
