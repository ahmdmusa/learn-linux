# 10 — File Ownership and Permissions (ملكية الملفات والصلاحيات)

> **السابق:** [09 - Linux User Accounts](09 - Linux User Accounts.md) | **التالي:** [11 - Pipes and Redirects](11 - Pipes and Redirects.md)

---

## 1. المفهوم الأساسي

كل ملف في Linux له **مالك (Owner)** ومرتبط بـ **مجموعة (Group)**، وله صلاحيات محددة لكل فئة.

---

## 2. قراءة الصلاحيات (ls -l)

```bash
ls -l file.txt
# -rwxr-xr-- 1 ahmed developers 4096 Jan 15 10:00 file.txt
#  
#   Other Permissions (r--)
#   Group Permissions (r-x)
#   Owner Permissions (rwx)
#   File Type (- = regular file, d = directory)
#  
#   نوع الملف
```

### تشريح الصلاحيات:

```
- r w x r - x r - -
         
   
  Owner  Group  Other
 File Type
```

| الرمز | الاسم | المعنى على ملف | المعنى على مجلد |
|-------|-------|---------------|----------------|
| `r` | Read | قراءة الملف | عرض المحتويات |
| `w` | Write | تعديل الملف | إنشاء/حذف داخله |
| `x` | Execute | تنفيذ كبرنامج | الدخول للمجلد |
| `-` | None | لا صلاحية | لا صلاحية |

---

## 3. الفئات الثلاث (Classes)

> [!info] **Three Permission Classes:**
> - **Owner (u):** المالك — من أنشأ الملف.
> - **Group (g):** المجموعة — المستخدمون في نفس مجموعة الملف.
> - **Others (o):** الآخرون — كل من ليس Owner أو في الـ Group.

---

## 4. تغيير الصلاحيات — `chmod`

> [!info] **chmod — Change Mode**
> أمر تغيير صلاحيات الملف.

### الطريقة الرمزية (Symbolic Mode)

```bash
chmod u+x file.txt       # أضف Execute للـ Owner
chmod g-w file.txt       # ازل Write من الـ Group
chmod o+r file.txt       # أضف Read للـ Others
chmod a+x file.txt       # أضف Execute للجميع (a = all)
chmod u+x,g-w file.txt   # تعديلات متعددة
chmod u=rwx file.txt     # عيّن صلاحيات Owner بالكامل
```

**الرموز:**
- `u` = user (owner) | `g` = group | `o` = others | `a` = all
- `+` = أضف | `-` = أزل | `=` = عيّن بالضبط

### الطريقة الرقمية (Numeric/Octal Mode)

> [!info] **Octal Permissions (النظام الثماني):**
> كل صلاحية لها قيمة رقمية:
> - `r` = **4**
> - `w` = **2**  
> - `x` = **1**
> - `-` = **0**
> 
> المجموع يعطيك الرقم للفئة.

```
rwx = 4+2+1 = 7
rw- = 4+2+0 = 6
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
--- = 0+0+0 = 0
```

**جدول سريع:**

| الرقم | الصلاحية |
|-------|---------|
| `7` | rwx (كامل) |
| `6` | rw- |
| `5` | r-x |
| `4` | r-- |
| `0` | --- (لا شيء) |

**أمثلة:**
```bash
chmod 755 file.txt    # Owner: rwx | Group: r-x | Others: r-x
chmod 644 file.txt    # Owner: rw- | Group: r-- | Others: r--
chmod 700 file.txt    # Owner: rwx | Group: --- | Others: ---
chmod 777 file.txt    # الجميع: rwx  (خطير!)
```

> [!warning] ** لا تستخدم 777 إلا لضرورة!**
> `chmod 777` يعطي الجميع صلاحيات كاملة. خطر أمني كبير على السيرفرات.

### الصلاحيات الأكثر شيوعاً:

| الرقم | الاستخدام الشائع |
|-------|----------------|
| `755` | مجلدات، سكريبتات قابلة للتنفيذ |
| `644` | ملفات عادية، ملفات الإعدادات |
| `600` | ملفات حساسة (مثل SSH keys) |
| `700` | مجلد خاص جداً بالـ Owner |

---

## 5. تغيير المالكية — `chown`

> [!info] **chown — Change Owner**
> تغيير مالك الملف و/أو مجموعته.

```bash
sudo chown ahmed file.txt             # تغيير المالك لـ ahmed
sudo chown ahmed:developers file.txt  # تغيير المالك والمجموعة
sudo chown :developers file.txt       # تغيير المجموعة فقط
sudo chown -R ahmed /home/ahmed/      # تغيير تعاودي (Recursive) للمجلد
```

### `chgrp` — تغيير المجموعة فقط
```bash
sudo chgrp developers file.txt
```

---

## 6. مثال عملي شامل

```bash
# إنشاء ملف وفحص صلاحياته
touch myfile.txt
ls -l myfile.txt
# -rw-r--r-- 1 ahmed ahmed 0 Jan 15 myfile.txt
#  Owner: rw- (6) | Group: r-- (4) | Others: r-- (4)

# جعله قابل للتنفيذ من قبل المالك
chmod u+x myfile.txt
# أو: chmod 744 myfile.txt
ls -l myfile.txt
# -rwxr--r-- 1 ahmed ahmed 0 Jan 15 myfile.txt

# تغيير المجموعة
sudo chown ahmed:developers myfile.txt
```

---

## 7. ملخص سريع

| الأمر | الوظيفة |
|-------|---------|
| `ls -l` | عرض الصلاحيات |
| `chmod 755 file` | تغيير الصلاحيات (رقمي) |
| `chmod u+x file` | تغيير الصلاحيات (رمزي) |
| `chown user file` | تغيير المالك |
| `chown user:group file` | تغيير المالك والمجموعة |
| `chgrp group file` | تغيير المجموعة |

---

>  **التالي:** [11 - Pipes and Redirects](11 - Pipes and Redirects.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
