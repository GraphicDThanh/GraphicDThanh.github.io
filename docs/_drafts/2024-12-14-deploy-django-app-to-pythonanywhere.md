---
title: "Deploy Django App to PythonAnywhere"
excerpt_separator: <!--more-->
categories:
  - django
tags:
  - django
  - deployment
---

# Hướng Dẫn Deploy Django App lên PythonAnywhere

## Giới Thiệu

PythonAnywhere là một nền tảng phổ biến để deploy các ứng dụng web Python. Với chi phí từ **5 USD/tháng**, bạn đã có thể khởi chạy một ứng dụng web cơ bản. Nếu bạn sử dụng SQLite hoặc MySQL, bạn có thể sử dụng gói cơ bản. Tuy nhiên, nếu muốn dùng PostgreSQL, bạn cần tối thiểu gói **12 USD/tháng**.

Bài viết này sẽ hướng dẫn bạn từng bước để deploy một ứng dụng Django lên PythonAnywhere, dành cho các lập trình viên từ cấp độ mới bắt đầu đến trung bình.

---

## Bước 1: Pull Code và Cài Đặt Virtual Environment

### Pull Code

- **Với repository công khai**:
git clone https://github.com/<owner>/repo.git

- **Với repository riêng tư**:
git clone https://<token>@github.com/<owner>/repo.git

### Cài Đặt Virtual Environment

PythonAnywhere hỗ trợ lệnh `mkvirtualenv` tích hợp sẵn để tạo môi trường ảo.

1. **Tạo môi trường ảo** (PythonAnywhere chỉ hỗ trợ Python 3.10):
mkvirtualenv --python=/usr/bin/python3.10 django-practice

2. **Cài đặt dependencies**:
pip install -r requirements/production.txt

---

## Bước 2: Thiết Lập Biến Môi Trường

### Tạo Secret Key

Chạy lệnh sau để tạo một Secret Key ngẫu nhiên:
python -c 'import random;import string; print("".join(random.SystemRandom().choice(string.digits + string.ascii_letters) for _ in range(50)))'

### Thêm Biến Môi Trường

- Mở tệp `postactivate` để thêm các biến môi trường. Tệp này được kích hoạt mỗi khi bạn sử dụng virtualenv:
vi $VIRTUAL_ENV/bin/postactivate

Nội dung:
```
export WEB_CONCURRENCY=4
export DJANGO_SETTINGS_MODULE='config.settings.production'
export DJANGO_SECRET_KEY='<your_generate_above>'
export DJANGO_ALLOWED_HOSTS='<account>.pythonanywhere.com'
export DJANGO_ADMIN_URL=''
export DATABASE_URL='sqlite:////home/<account>/path/to/db.sqlite'
export SENDGRID_API_KEY=''
```
---

## Bước 3: Thiết Lập Database

1. Truy cập tab **Database** trên giao diện PythonAnywhere để thiết lập (nếu cần).

2. Đảm bảo bạn đang ở thư mục chứa tệp `manage.py`, sau đó chạy các lệnh:
python manage.py migrate
python manage.py collectstatic

---

## Bước 4: Cấu Hình Ứng Dụng Web

### Tạo Web App Thủ Công

1. Truy cập tab **Web** trên PythonAnywhere và chọn cấu hình thủ công.

2. Thiết lập các đường dẫn:
   - **Source code**: `/home/<account>/django-proj-pocs`
   - **Virtual environment**: `/home/<account>/.virtualenvs/django-practice`

3. Thiết lập static files:
   - URL: `/static/`
   - Thư mục: `/home/<account>/django-practice/src`

### Cập Nhật Tệp WSGI

- Truy cập tệp WSGI tại `/var/www/<account>_pythonanywhere_com_wsgi.py`.
- Cập nhật nội dung như sau:
```
import os
import sys

path = '/home/<account>/mysite'
if path not in sys.path:
    sys.path.append(path)

os.environ['WEB_CONCURRENCY'] = '4'
os.environ['DJANGO_SETTINGS_MODULE'] = 'config.settings.production'
os.environ['DJANGO_SECRET_KEY'] = '<generated_secret_key>'
os.environ['DJANGO_ALLOWED_HOSTS'] = '<account>.pythonanywhere.com'
os.environ['DATABASE_URL'] = 'sqlite:////home/<account>/path/to/db.sqlite'
os.environ['SENDGRID_API_KEY'] = ''

from django.core.wsgi import get_wsgi_application
application = get_wsgi_application
```

### Lưu Ý

1. Sau khi cập nhật biến môi trường, hãy chạy lệnh sau:

```
source $VIRTUAL_ENV/bin/postactivate
python manage.py migrate
```

1. Nếu gặp lỗi "SyntaxError: unicode error", hãy tạo lại secret key và tránh các ký tự đặc biệt.

---

## Kiểm Tra Và Reload Ứng Dụng

- Trở lại tab **Web** và nhấn **Reload**.
- Truy cập URL `<account>.pythonanywhere.com` để kiểm tra ứng dụng.

Nếu gặp sự cố, hãy kiểm tra các tệp log (error, server) trong PythonAnywhere để xác định lỗi.

---

Với các bước trên, bạn đã triển khai thành công ứng dụng Django lên PythonAnywhere. Chúc bạn may mắn và thành công!


----------------------------
Guide ChatGPT:

Intended Audience: Beginners and intermediate developers
Tone: casual, instructional
Length: medium or long
Content Format: step-by-step guide

The guide is similar to this link https://cookiecutter-django.readthedocs.io/en/latest/3-deployment/deployment-on-pythonanywhere.html
Content:
Introduction:
- PythonAnyWhere
- for $5/month, could start a web app
- free for sqlite, mysql. For postgres, minimal to $12/month
Step 1. Pull code and install virtual env with dependencies in PythonAnywhere
- Pull code:
  - public repo: git clone https://github.com/<owner>/repo.git
  - not public repo: git clone https://<token>@github.com/<owner>/repo.git
- Install virtual environment: use built-in mkvirtualenv
  - Create virtual env: `mkvirtualenv --python=/usr/bin/python3.10 django-practice` (pythonanywhere only support 3.10)
  - Install dependencies: `pip install -r requirements/production.txt`

Step 2. Set environment variables in console
- Generate a secret key:
```python -c 'import random;import string; print("".join(random.SystemRandom().choice(string.digits + string.ascii_letters) for _ in range(50)))'```
- Set environment variables via virtualenv "postactivate" script, this will call every time you use the virtualenv in console.
  - Open file with vi editor: `vi $VIRTUAL_ENV/bin/postactivate`
  - Access in Files via dashboard: /home/thanhnguyendiem/.virtualenvs/django-practice/bin/postactivate (image attach)
```
export WEB_CONCURRENCY=4
export DJANGO_SETTINGS_MODULE='config.settings.production'
export DJANGO_SECRET_KEY=<your_generate_above>'
export DJANGO_ALLOWED_HOSTS='<account>.pythonanywhere.com'
export DJANGO_ADMIN_URL=''
export DATABASE_URL='postgres://super:<password>@<account>-4228.postgres.pythonanywhere-services.com:14228/<db_name>'
export SENDGRID_API_KEY=''
```

Step 3: Setup database -> use sqlite for testing
- Go to Database tab and do setup (if any)
- Make sure stand in folder has manage.py, run command:
python manage.py migrate
- python manage.py collectstatic

Step 4: Config web app
- Create and select manual config webapp
- Set path to your side code: `/home/thanhnguyendiem/django-proj-pocs`
- Set path to virtual env code: call `which python` to find the path
`/home/thanhnguyendiem/.virtualenvs/django-practice`
- Set static files: `/static/` and 	/home/thanhnguyendiem/django-practice/src
- In code section, select to file /var/www/thanhnguyendiem_pythonanywhere_com_wsgi.py and update:
comment other code, uncommend Django guide, then add environment variables into to:
```
import os
import sys

path = '/home/thanhnguyendiem/mysite'
if path not in sys.path:
    sys.path.append(path)

os.environ['WEB_CONCURRENCY']='4'
os.environ['DJANGO_SETTINGS_MODULE']='config.settings.production'
os.environ['DJANGO_SECRET_KEY']='xxx'
os.environ['DJANGO_ALLOWED_HOSTS']='<account>.pythonanywhere.com'
os.environ['DJANGO_ADMIN_URL']=''
os.environ['DATABASE_URL']='sqlite:////home/<account>/path/to/db.sqlite'
os.environ['GOOGLE_API_KEY']="test-key"
os.environ['SENDGRID_API_KEY']=''
...

from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
```
Notice 1: Everytime update env, go update it with `source $VIRTUAL_ENV/bin/postactivate`
Note 2: Django secret generate sometime got error "SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes in position 36-37: truncated \uXXXX escape" -> Need to regenerate, usually not have special character

- Back to the Web app, reload app then access your page to see it.

If there are any issue, check the log error.



