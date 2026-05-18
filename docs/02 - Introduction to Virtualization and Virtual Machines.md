# 02 — Introduction to Virtualization & Virtual Machines

> **السابق:** [01 - Introduction to Operating Systems](01 - Introduction to Operating Systems.md) | **التالي:** [03 - Setup Linux Virtual Machine](03 - Setup Linux Virtual Machine.md)

---

## 1. المشكلة اللي حلّها الـ Virtualization

تخيّل إنك عندك **Server قوي جداً** — RAM 128GB, 32 Core CPU — وعندك تطبيق صغير محتاج 2GB RAM بس.

- **بدون Virtualization:** Server كامل ضايع على تطبيق صغير. 
- **مع Virtualization:** تقسّم الـ Server لـ 20 سيرفر وهمي صغير، كل واحد فيهم يشتغل مستقل. 

---

## 2. تعريف الـ Virtualization

> [!info] **Virtualization (الافتراضية)**
> تقنية تسمح بتشغيل **أنظمة تشغيل متعددة** على نفس الـ Hardware الفيزيائي في نفس الوقت، كل واحد معزول عن الآخر.

---

## 3. المكونات الأساسية

```

         Physical Hardware              
    (CPU + RAM + Storage + Network)     

         Hypervisor (المدير)            

   VM #1         VM #2        VM #3   
  Ubuntu        Windows       CentOS  
  (Guest OS)    (Guest OS)  (Guest OS)

```

> [!info] **Hypervisor**
> هو البرنامج المسؤول عن إنشاء وإدارة الـ Virtual Machines. بيوزع موارد الـ Hardware على الـ VMs.

> [!info] **Virtual Machine — VM (الجهاز الافتراضي)**
> محاكاة كاملة لجهاز حاسوب حقيقي، بيشتغل داخل جهازك الحقيقي. ليه OS خاص بيه وموارد معينة.

> [!info] **Host OS vs Guest OS**
> - **Host OS:** نظام التشغيل الأصلي المثبّت على جهازك الحقيقي.
> - **Guest OS:** نظام التشغيل اللي شغّال داخل الـ VM.

---

## 4. أنواع الـ Hypervisors

### النوع الأول: Type 1 — Bare Metal Hypervisor
- بيتثبّت **مباشرة على الـ Hardware** بدون OS تحته.
- أسرع وأكثر كفاءة.
- للاستخدام في **Servers الإنتاج (Production)**.

> أمثلة: **VMware ESXi**, **Microsoft Hyper-V**, **KVM**

### النوع الثاني: Type 2 — Hosted Hypervisor
- بيشتغل **فوق OS موجود** (Windows أو macOS).
- أبطأ نسبياً لكن **سهل التثبيت والاستخدام**.
- للاستخدام في **التطوير والتعلم (Development/Learning)**.

> أمثلة: **VirtualBox**, **VMware Workstation**

```
Type 1:                    Type 2:
           
   VM | VM                  VM | VM    
           
  Hypervisor               Hypervisor  
           
  Hardware                  Host OS    
           
                             Hardware    
                           
```

> [!warning] **نقطة مهمة في الامتحانات!**
> الفرق بين Type 1 و Type 2:
> - **Type 1:** مباشرة على الـ Hardware — للـ Production — أسرع.
> - **Type 2:** فوق OS — للـ Learning/Dev — أسهل.

---

## 5. فوائد الـ Virtualization

| الفائدة | الشرح |
|---------|-------|
| **Resource Efficiency** (كفاءة الموارد) | استغلال الـ Hardware بشكل أفضل |
| **Isolation** (العزل) | كل VM معزول، لو VM انهار ما يأثرش على الباقي |
| **Snapshot** (لقطة) | تقدر تحفظ حالة الـ VM وترجع إليها وقت ما تريد |
| **Easy Migration** | تقدر تنقل الـ VM من سيرفر لسيرفر بسهولة |
| **Cost Saving** | توفير في الأجهزة والكهرباء |

---

## 6. الـ VM مقابل الـ Container

> [!lightbulb] **VM vs Container — الفرق المهم:**
> - **VM:** محاكاة كاملة للـ Hardware + OS كامل. ثقيل لكن عزل تام.
> - **Container (مثل Docker):** بيشارك نفس الـ OS Kernel. أخف وأسرع.
>
> ```
> VM:                     Container:
> [App]                   [App] [App] [App]
> [Guest OS]              [Container Engine]
> [Hypervisor]            [Host OS]
> [Hardware]              [Hardware]
> ```

---

## 7. ملخص سريع

| المفهوم | المعنى |
|---------|--------|
| **Virtualization** | تشغيل أنظمة متعددة على Hardware واحد |
| **Hypervisor** | المدير الذي يتحكم في الـ VMs |
| **VM** | جهاز افتراضي يعمل كجهاز حقيقي |
| **Type 1** | Hypervisor مباشر على الـ Hardware |
| **Type 2** | Hypervisor فوق Host OS |
| **Host OS** | نظام التشغيل الأصلي |
| **Guest OS** | نظام التشغيل داخل الـ VM |

---

>  **التالي:** [03 - Setup Linux Virtual Machine](03 - Setup Linux Virtual Machine.md)

---

Notes by. Ahmed Mousa  
شكر خاص  
Eng. [Ahmed Eid](https://www.youtube.com/@a0xEid)
