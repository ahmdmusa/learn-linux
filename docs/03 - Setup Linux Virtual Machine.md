# 03 — Setup Linux Virtual Machine (تثبيت Linux VM)

> **السابق:** [02 - Introduction to Virtualization and Virtual Machines](02 - Introduction to Virtualization and Virtual Machines.md) | **التالي:** [04 - Linux File System](04 - Linux File System.md)

---

## 1. المتطلبات

> [!info] **الأدوات اللازمة:**
> - **VirtualBox** (مجاني) — [virtualbox.org](https://www.virtualbox.org) — Type 2 Hypervisor
> - **Ubuntu ISO** — [ubuntu.com](https://ubuntu.com/download) — الـ Linux Distro اللي هنثبتها

---

## 2. الخطوات الأساسية للإعداد

### الخطوة 1: تثبيت VirtualBox
- حمّل الـ Installer المناسب لنظامك (Windows / macOS).
- ثبّته بشكل طبيعي (Next → Next → Install).

### الخطوة 2: تحميل Ubuntu ISO
- روح [ubuntu.com/download](https://ubuntu.com/download/desktop)
- حمّل الـ **LTS version** (Long Term Support — دعم طويل الأمد).

> [!info] **LTS — Long Term Support**
> إصدار Ubuntu مدعوم لمدة **5 سنوات**. أكثر استقراراً من الإصدارات العادية. مناسب جداً للتعلم والـ Servers.

### الخطوة 3: إنشاء VM جديد في VirtualBox
1. افتح VirtualBox → اضغط **New**.
2. اختر اسم للـ VM (مثلاً: `Ubuntu-Dev`).
3. اختر النوع: **Linux** → Version: **Ubuntu (64-bit)**.
4. حدد الـ **RAM** المخصصة — يُفضّل **2GB (2048 MB)** على الأقل.
5. أنشئ **Virtual Hard Disk** — يُفضّل **20GB** أو أكثر.

> [!warning] **لا تعطي الـ VM أكثر من نص موارد جهازك!**
> لو جهازك عنده 8GB RAM، ما تعطيش الـ VM أكتر من 4GB، عشان الـ Host OS ما يتجمّدش.

### الخطوة 4: ربط الـ ISO بالـ VM
1. اختر الـ VM المنشأ → Settings → Storage.
2. تحت **Controller: IDE** اضغط على أيقونة الـ Disc.
3. اختر **Choose a disk file** → حدد ملف الـ Ubuntu ISO.

### الخطوة 5: تثبيت Ubuntu
1. شغّل الـ VM (Start).
2. اتبع خطوات تثبيت Ubuntu:
   - اختر اللغة.
   - اختر **Normal Installation**.
   - اختر **Erase disk and install Ubuntu** (داخل الـ VM فقط، مش جهازك الحقيقي!).
   - حدد اسم المستخدم وكلمة السر.
3. انتظر انتهاء التثبيت ثم أعِد التشغيل.

---

## 3. إعدادات مهمة بعد التثبيت

### تثبيت Guest Additions
> [!lightbulb] **ما هي Guest Additions؟**
> مجموعة Drivers إضافية من VirtualBox تحسّن أداء الـ VM:
> - **Shared Clipboard** (نسخ ولصق بين الـ Host و Guest).
> - **Drag & Drop** للملفات.
> - **Auto-resize** للشاشة.
> - أداء رسومي أفضل.

**كيفية التثبيت:**
```bash
# داخل الـ Ubuntu VM، افتح Terminal واكتب:
sudo apt update
sudo apt install virtualbox-guest-additions-iso
```
أو من قائمة VirtualBox: **Devices → Insert Guest Additions CD image**

### ضبط الـ Network
| الوضع | الاستخدام |
|-------|-----------|
| **NAT** (الافتراضي) | الـ VM يوصل للإنترنت عبر الـ Host |
| **Bridged Adapter** | الـ VM يظهر على الشبكة كجهاز مستقل |
| **Host-Only** | تواصل بين الـ VM والـ Host فقط |

> [!info] **NAT — Network Address Translation**
> الـ VM يستخدم IP جهازك للوصول للإنترنت. الوضع الافتراضي ومناسب للتعلم.

---

## 4. أوامر أساسية للتحقق بعد التثبيت

```bash
# التحقق من إصدار Ubuntu
lsb_release -a

# التحقق من الـ RAM المتاحة
free -h

# التحقق من مساحة الـ Disk
df -h

# التحقق من الـ CPU
nproc
```

---

## 5. نصائح مهمة

> [!warning] **نقاط يجب تذكرها:**
> - **Snapshot:** افعلها دايماً قبل أي تجربة! (Machine → Take Snapshot) — تقدر ترجع لأي وقت لو الأمور اتعقدت.
> - لا تحذف الـ ISO بعد التثبيت، ممكن تحتاجه.
> - لو الـ VM بطيء، تأكد إن **VT-x / AMD-V** مفعّل في الـ BIOS.

---

>  **التالي:** [04 - Linux File System](04 - Linux File System.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
