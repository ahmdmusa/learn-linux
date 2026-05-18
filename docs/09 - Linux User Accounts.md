# 09 — Linux User Accounts (حسابات المستخدمين)

> **السابق:** [08 - Vi and Vim Text Editors](08 - Vi and Vim Text Editors.md) | **التالي:** [10 - File Ownership and Permissions](10 - File Ownership and Permissions.md)

---

## 1. أنواع المستخدمين في Linux

> [!info] **User Types:**
> - **Root User:** المدير العام. صلاحيات مطلقة. UID = 0.
> - **Regular User:** مستخدم عادي. صلاحيات محدودة.
> - **System User:** حسابات للخدمات والبرامج (nginx, mysql...). عادةً بدون تسجيل دخول.

```

  Root User (UID 0)                  
  ← صلاحية على كل شيء               

  Regular Users (UID 1000+)          
  ← صلاحيات محدودة بمجلداتهم        

  System Users (UID 1-999)           
  ← للخدمات (nginx, www-data...)    

```

> [!info] **UID — User ID**
> رقم تعريفي فريد لكل مستخدم في النظام.

---

## 2. ملف `/etc/passwd`

يحتوي على معلومات كل مستخدم:

```bash
cat /etc/passwd
# ahmed:x:1001:1001:Ahmed Mohamed:/home/ahmed:/bin/bash
#                                          
#                                           Default Shell
#                                Home Directory
#                    Full Name (Comment)
#             GID (Group ID)
#         UID (User ID)
#       x = كلمة السر في /etc/shadow
#    Username
```

---

## 3. إدارة المستخدمين (User Management)

### إنشاء مستخدم جديد
```bash
sudo useradd ahmed                    # إنشاء مستخدم بسيط
sudo useradd -m ahmed                 # + إنشاء Home Directory
sudo useradd -m -s /bin/bash ahmed    # + تحديد الـ Shell
sudo adduser ahmed                    # طريقة تفاعلية (أسهل في Ubuntu)
```

> [!lightbulb] **`useradd` vs `adduser`**
> - `useradd`: أمر منخفض المستوى، يحتاج خيارات.
> - `adduser`: واجهة أسهل، يسألك عن كل شيء تفاعلياً. (خاص بـ Debian/Ubuntu)

### تعيين كلمة المرور
```bash
sudo passwd ahmed          # تعيين كلمة مرور للمستخدم ahmed
passwd                     # تغيير كلمة مرورك أنت
```

### حذف مستخدم
```bash
sudo userdel ahmed          # حذف المستخدم (يبقى الـ Home Directory)
sudo userdel -r ahmed       # حذف المستخدم + مجلده الشخصي
```

### تعديل مستخدم
```bash
sudo usermod -l newname ahmed         # تغيير الاسم
sudo usermod -d /home/newhome ahmed   # تغيير الـ Home Directory
sudo usermod -s /bin/zsh ahmed        # تغيير الـ Shell
sudo usermod -aG sudo ahmed           # إضافة لمجموعة sudo
```

---

## 4. إدارة المجموعات (Groups)

> [!info] **Group (المجموعة)**
> مجموعة مستخدمين لهم صلاحيات مشتركة على ملفات أو موارد معينة.

```bash
sudo groupadd developers              # إنشاء مجموعة
sudo groupdel developers              # حذف مجموعة
sudo gpasswd -a ahmed developers      # إضافة ahmed للمجموعة
sudo gpasswd -d ahmed developers      # إزالة ahmed من المجموعة
groups ahmed                          # عرض مجموعات ahmed
```

> [!info] **Primary Group vs Secondary Group**
> - **Primary Group:** المجموعة الافتراضية. كل مستخدم له واحدة فقط.
> - **Secondary Groups:** مجموعات إضافية يمكن أن ينتمي لها.

---

## 5. الـ sudo — صلاحيات Root مؤقتة

> [!info] **sudo — Superuser Do**
> تنفيذ أمر واحد بصلاحيات الـ Root دون تسجيل الدخول كـ Root.

```bash
sudo apt update            # تنفيذ أمر كـ Root
sudo -i                    # الدخول لجلسة Root كاملة
sudo su - ahmed            # التحول لمستخدم ahmed
su - ahmed                 # التحول بكلمة مرور ahmed
```

> [!warning] **لا تعمل كـ Root دائماً!**
> العمل المستمر كـ Root خطير. أمر خاطئ واحد قد يدمر النظام.  
> استخدم `sudo` فقط عند الحاجة.

### ملف `/etc/sudoers`
يحدد من له صلاحية استخدام `sudo`:
```bash
sudo visudo                # الطريقة الآمنة لتعديله
# ahmed ALL=(ALL:ALL) ALL  ← إعطاء ahmed صلاحيات sudo كاملة
```

---

## 6. أوامر مفيدة

```bash
whoami            # اسم المستخدم الحالي
id                # UID, GID ومجموعات المستخدم
id ahmed          # نفس المعلومات لمستخدم معين
w                 # من المتصل بالنظام الآن
last              # سجل تسجيلات الدخول
```

---

## 7. ملخص سريع

| الأمر | الوظيفة |
|-------|---------|
| `adduser name` | إنشاء مستخدم جديد |
| `passwd name` | تعيين كلمة مرور |
| `userdel -r name` | حذف مستخدم ومجلده |
| `usermod -aG group name` | إضافة لمجموعة |
| `sudo command` | تنفيذ أمر كـ Root |
| `groups name` | عرض مجموعات مستخدم |
| `id` | معلومات المستخدم الحالي |

---

>  **التالي:** [10 - File Ownership and Permissions](10 - File Ownership and Permissions.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
