# 05 — GUI vs Command Line Interface

> **السابق:** [04 - Linux File System](04 - Linux File System.md) | **التالي:** [06 - Basic Linux Commands](06 - Basic Linux Commands.md)

---

## 1. التعريفات

> [!info] **GUI — Graphical User Interface (الواجهة الرسومية)**
> التفاعل مع الحاسوب عن طريق **نوافذ وأيقونات وأزرار**. مثل: Windows Explorer، متصفح الإنترنت.

> [!info] **CLI — Command Line Interface (واجهة سطر الأوامر)**
> التفاعل مع الحاسوب عن طريق **كتابة أوامر نصية**.  
> يُسمى أيضاً: **Terminal**, **Shell**, **Console**, **Bash**.

---

## 2. المقارنة

| المعيار | GUI | CLI |
|---------|-----|-----|
| **سهولة الاستخدام** |  سهلة للمبتدئين |  تحتاج تعلم |
| **السرعة** |  أبطأ |  أسرع بكثير |
| **الأتمتة (Automation)** |  صعبة |  سهلة جداً (Scripts) |
| **استهلاك الموارد** |  يستهلك RAM وCPU |  خفيف جداً |
| **الـ Remote Access** |  يحتاج تكوين خاص |  SSH يكفي |
| **الدقة والتحكم** |  محدود |  تحكم كامل |

> [!lightbulb] **ليه نستخدم CLI في Linux؟**
> معظم الـ Linux Servers **ما عندهاش GUI!** لأن الـ GUI:
> - تستهلك موارد (RAM, CPU) بدون فائدة في الـ Server.
> - الـ Servers بتُدار عن بُعد عبر **SSH** (نص فقط).
> لذلك لازم تتعلم الـ CLI.

---

## 3. ما هو الـ Shell؟

> [!info] **Shell**
> هو البرنامج اللي بيستقبل أوامرك النصية ويبعتها للـ Kernel لينفذها. هو الوسيط بينك وبين الـ OS.

```
أنت → [Shell] → [Kernel] → Hardware
         ↑
    (مترجم أوامرك)
```

### أنواع الـ Shell

| الـ Shell | الوصف |
|-----------|-------|
| **Bash** (Bourne Again Shell) | الأكثر شيوعاً في Linux |
| **Zsh** | أحدث، فيه ميزات إضافية |
| **Fish** | سهل الاستخدام، مناسب للمبتدئين |
| **sh** | أقدم Shell، أبسط |

> [!info] **Bash — Bourne Again Shell**
> الـ Shell الافتراضي في معظم توزيعات Linux. هو اللي هنستخدمه في المحاضرات.

---

## 4. فتح الـ Terminal في Ubuntu

- **طريقة 1:** `Ctrl + Alt + T`
- **طريقة 2:** ابحث عن "Terminal" في تطبيقات الـ System.
- **طريقة 3:** Click يمين على سطح المكتب → Open Terminal.

---

## 5. تشريح الـ Prompt (سطر الأوامر)

```bash
ahmed@ubuntu:~$
            
             $ = مستخدم عادي | # = Root
            ~ = المجلد الحالي (Home)
         اسم الجهاز (Hostname)
   اسم المستخدم (Username)
```

> [!warning] **$ vs #**
> - `$` ← مستخدم عادي (محدود الصلاحيات).
> - `#` ← مستخدم الـ **Root** (صلاحيات كاملة — انتبه!).

---

>  **التالي:** [06 - Basic Linux Commands](06 - Basic Linux Commands.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
