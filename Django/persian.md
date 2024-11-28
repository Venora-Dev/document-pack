# 🐍🌐 راهنمای جامع راه‌اندازی و توسعه با Django

به راهنمای پیشرفته تنظیم و توسعه با Django، یک فریم‌ورک وب سطح بالا برای پایتون که به توسعه سریع و طراحی تمیز و عملی کمک می‌کند، خوش آمدید. بیایید به دنیای Django بپردازیم! 🚀

## 📋 فهرست مطالب
1. [مقدمه](#مقدمه)
2. [پیش‌نیازها](#پیش‌نیازها)
3. [تنظیم محیط](#تنظیم-محیط)
    - نصب پایتون
    - محیط‌های مجازی
    - نصب Django
4. [ایجاد پروژه Django](#ایجاد-پروژه-django)
5. [اپلیکیشن‌های Django](#اپلیکیشن‌های-django)
    - ایجاد اپلیکیشن
    - پیکربندی اپلیکیشن
6. [مدل‌ها و پایگاه‌داده‌ها](#مدل‌ها-و-پایگاه‌داده‌ها)
    - تعریف مدل‌ها
    - مهاجرت‌ها
    - پرس‌وجوهای ORM
7. [نمایش‌ها و URLها](#نمایش‌ها-و-urlها)
    - نمایش‌های مبتنی بر تابع
    - نمایش‌های مبتنی بر کلاس
    - مسیریابی URL
8. [قالب‌ها](#قالب‌ها)
    - زبان قالب
    - وراثت قالب‌ها
9. [فایل‌های استاتیک و رسانه‌ای](#فایل‌های-استاتیک-و-رسانه‌ای)
10. [فرم‌ها و اعتبارسنجی](#فرم‌ها-و-اعتبارسنجی)
11. [احراز هویت و مجوز](#احراز-هویت-و-مجوز)
12. [میان‌افزار](#میان‌افزار)
13. [بین‌المللی‌سازی و بومی‌سازی](#بین‌المللی‌سازی-و-بومی‌سازی)
14. [تست](#تست)
15. [راه‌اندازی](#راه‌اندازی)
16. [موضوعات پیشرفته](#موضوعات-پیشرفته)
17. [نتیجه‌گیری](#نتیجه‌گیری)
18. [منابع](#منابع)

### 1️⃣ مقدمه
Django یک فریم‌ورک وب قدرتمند نوشته شده به زبان پایتون است که از الگوی معماری Model-View-Template (MVT) پیروی می‌کند. این فریم‌ورک بر قابلیت استفاده مجدد و "پلاگین‌پذیری" اجزا، توسعه سریع و اصل "خودت را تکرار نکن" (DRY) تاکید دارد.

### 2️⃣ پیش‌نیازها
قبل از شروع، اطمینان حاصل کنید که:
- دانش پایه‌ای از برنامه‌نویسی پایتون 🐍 دارید.
- با مفاهیم توسعه وب (HTTP، HTML، CSS) آشنا هستید.
- پایتون نسخه 3.8 یا بالاتر روی سیستم شما نصب شده است.

### 3️⃣ تنظیم محیط
#### نصب پایتون
پایتون را از وب‌سایت رسمی دانلود و نصب کنید. نصب را بررسی کنید:
```bash
python --version
```
#### محیط‌های مجازی
بهترین روش استفاده از محیط‌های مجازی برای مدیریت وابستگی‌هاست. یک محیط مجازی با استفاده از `venv` ایجاد کنید:
```bash
python -m venv env
```
محیط مجازی را فعال کنید:
- **ویندوز**:
  ```bash
  env\Scripts\activate
  ```
- **macOS/Linux**:
  ```bash
  source env/bin/activate
  ```

#### نصب Django
با فعال بودن محیط مجازی، Django را نصب کنید:
```bash
pip install django
```
نصب را بررسی کنید:
```bash
django-admin --version
```

### 4️⃣ ایجاد پروژه Django
یک پروژه جدید Django با استفاده از دستور `django-admin` ایجاد کنید:
```bash
django-admin startproject myproject
```
به دایرکتوری پروژه بروید:
```bash
cd myproject
```
ساختار پروژه شما باید به شکل زیر باشد:
```
myproject/
├── manage.py
└── myproject/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```
- **manage.py**: ابزار خط فرمان برای وظایف مدیریتی.
- **settings.py**: تنظیمات پیکربندی برای پروژه.
- **urls.py**: تعاریف URL.
- **wsgi.py** و **asgi.py**: نقاط ورودی برای سرورهای وب سازگار با WSGI/ASGI.

### 5️⃣ اپلیکیشن‌های Django
#### ایجاد اپلیکیشن
یک اپلیکیشن در پروژه خود ایجاد کنید:
```bash
python manage.py startapp myapp
```
`myapp` را به لیست `INSTALLED_APPS` در `settings.py` اضافه کنید:
```python
# myproject/settings.py

INSTALLED_APPS = [
    # ...
    'myapp.apps.MyappConfig',
]
```

### 6️⃣ مدل‌ها و پایگاه‌داده‌ها
#### تعریف مدل‌ها
مدل‌های داده خود را در `models.py` تعریف کنید:
```python
# myapp/models.py

from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)  # 📝
    content = models.TextField()
    published_date = models.DateTimeField(auto_now_add=True)  # 🗓️

    def __str__(self):
        return self.title
```

#### مهاجرت‌ها
برای همگام‌سازی مدل‌ها با پایگاه‌داده، مهاجرت‌ها را ایجاد و اعمال کنید:
```bash
python manage.py makemigrations
python manage.py migrate
```

#### پرس‌وجوهای ORM
از ORM Django برای تعامل با پایگاه‌داده استفاده کنید:
```python
# دسترسی به شل
python manage.py shell

# در شل
from myapp.models import Post
Post.objects.create(title='اولین پست', content='سلام، دنیا!')
posts = Post.objects.all()
```

### 7️⃣ نمایش‌ها و URLها
#### نمایش‌های مبتنی بر تابع
نمایش‌ها را در `views.py` تعریف کنید:
```python
# myapp/views.py

from django.shortcuts import render
from .models import Post

def home(request):
    posts = Post.objects.all()
    return render(request, 'myapp/home.html', {'posts': posts})
```

#### مسیریابی URL
نمایش‌ها را به URLها در `urls.py` متصل کنید:
```python
# myproject/urls.py

from django.contrib import admin
from django.urls import path, include  # 🛣️

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```
`urls.py` را در `myapp` ایجاد کنید:
```python
# myapp/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### 8️⃣ قالب‌ها
#### زبان قالب
قالب‌ها را با استفاده از زبان قالب Django ایجاد کنید:
```html
<!-- myapp/templates/myapp/home.html -->

{% extends "myapp/base.html" %}

{% block content %}
<h1>🏠 صفحه اصلی</h1>
<ul>
    {% for post in posts %}
    <li>{{ post.title }} - {{ post.published_date|date:"F j, Y" }}</li>
    {% empty %}
    <li>پستی موجود نیست.</li>
    {% endfor %}
</ul>
{% endblock %}
```

### 9️⃣ فایل‌های استاتیک و رسانه‌ای
فایل‌های استاتیک را در `settings.py` پیکربندی کنید:
```python
# myproject/settings.py

STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']  # 📁
```
فایل‌های استاتیک را در قالب‌ها لینک دهید:
```html
<!-- myapp/templates/myapp/base.html -->

{% load static %}

<link rel="stylesheet" href="{% static 'css/styles.css' %}">
```

### 🔟 فرم‌ها و اعتبارسنجی
فرم‌ها را با استفاده از کلاس‌های فرم Django ایجاد کنید:
```python
# myapp/forms.py

from django import forms
from .models import Post

class PostForm(forms.ModelForm):  # 📝
    class Meta:
        model = Post
        fields = ['title', 'content']
```

### 1️⃣5️⃣ راه‌اندازی
پروژه خود را برای راه‌اندازی آماده کنید:
- مقدار `DEBUG = False` را در `settings.py` تنظیم کنید و `ALLOWED_HOSTS` را پیکربندی کنید.
- فایل‌های استاتیک را جمع‌آوری کنید:
  ```bash
  python manage.py collectstatic
  ```
- از سرور WSGI تولیدی مانند Gunicorn استفاده کنید:
  ```bash
  pip install gunicorn
  gunicorn myproject.wsgi:application
  ```

### 1️⃣7️⃣ نتیجه‌گیری
شما با راه‌اندازی و توسعه با Django آشنا شدید و مفاهیم پیشرفته‌ای را مرور کردید که به شما در ایجاد برنامه‌های وب مقیاس‌پذیر و قابل اعتماد کمک می‌کنند. به آزمایش و بررسی اکوسیستم وسیع Django ادامه دهید! 🎉

### 1️⃣8️⃣ منابع
- 📚 [مستندات رسمی](https://docs.djangoproject.com)
- 🛠️ [پکیج‌های Django](https://djangopackages.org)
- 🎓 آموزش‌ها:
  - [آموزش Django Girls](https://tutorial.djangogirls.org/)
  - [Django برای حرفه‌ای‌ها](https://djangoforprofessionals.com/)
- 🌐 جامعه:
  - [انجمن Django](https://forum.djangoproject.com/)
  - [Stack Overflow](https://stackoverflow.com/)

برنامه‌نویسی خوش با Django! 🚀🐍
