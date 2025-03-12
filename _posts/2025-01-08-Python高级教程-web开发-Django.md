---
title: Python高级教程-web开发-Django.md
author: 老章 mlpy
date: 2025-01-08 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

[toc]

# Python Web 开发教程：Django 全栈开发指南

## 1. Django 简介与环境搭建
### 1.1 Django 框架介绍
#### Django 的历史与发展
Django 框架诞生于 2003 年，最初是由堪萨斯州 Lawrence Journal-World 报纸的网络开发人员 Adrian Holovaty 和 Simon Willison 开发的。他们需要开发新闻网站，并且需要满足快速开发和严格的新闻编辑部最后期限的要求。2005 年，他们将框架开源，并以著名的吉他手 Django Reinhardt 的名字命名。

Django 的版本发展：
- Django 1.0（2008 年）：第一个正式版本
- Django 2.0（2017 年）：完全支持 Python 3
- Django 3.0（2019 年）：引入 ASGI 支持
- Django 4.0（2021 年）：增强异步功能
- Django 5.0（2023 年）：现代化改进和性能优化

#### Django 的特点和优势
1. **快速开发**
   - 内置 Admin 管理界面
   - 丰富的内置功能组件
   - 完善的项目模板
   - 自动化的配置系统

2. **安全可靠**
   - 内置防御 XSS 攻击
   - CSRF 保护机制
   - SQL 注入防护
   - 密码哈希系统
   - 安全会话管理

3. **可扩展性**
   - 组件化的应用结构
   - 灵活的中间件系统
   - 丰富的第三方包生态
   - 可自定义的配置系统

4. **完善的文档**
   - 详细的官方文档
   - 活跃的社区支持
   - 丰富的教程资源
   - 完整的 API 参考

#### Django vs 其他 Web 框架
1. **Django vs Flask**
   - Django：全能型框架，内置功能丰富
   - Flask：轻量级框架，更加灵活
   - 选择建议：大型项目选 Django，小型项目选 Flask

2. **Django vs FastAPI**
   - Django：同步框架，成熟稳定
   - FastAPI：异步框架，性能出色
   - 选择建议：传统 Web 应用选 Django，API 服务选 FastAPI

3. **Django vs Spring Boot**
   - Django：Python 生态，开发速度快
   - Spring Boot：Java 生态，企业级特性多
   - 选择建议：根据团队技术栈和项目需求选择

#### Django 的应用场景
1. **内容管理系统（CMS）**
   - 新闻网站
   - 博客平台
   - 文档管理系统
   - 企业官网

2. **电子商务平台**
   - 在线商城
   - 订单管理系统
   - 支付系统
   - 库存管理

3. **社交网络应用**
   - 社交平台
   - 论坛系统
   - 评论系统
   - 用户管理

4. **企业应用系统**
   - ERP 系统
   - CRM 系统
   - 办公自动化
   - 数据分析平台

### 1.2 开发环境搭建
#### Python 环境配置
1. **安装 Python**
```bash
# macOS安装
brew install python

# 验证安装
python3 --version
```

2. **配置 PATH 环境变量**
```bash
# 在~/.zshrc或~/.bash_profile中添加
export PATH="/usr/local/bin:$PATH"
```

#### Django 安装与版本选择
1. **使用 pip 安装 Django**
```bash
# 安装最新版Django
pip install django

# 安装特定版本
pip install django==5.0.1

# 验证安装
python -m django --version
```

2. **版本选择建议**
- 新项目推荐使用 Django 5.0+
- 需要长期支持选择 LTS 版本
- 考虑项目依赖包的兼容性

#### 开发工具推荐
1. **PyCharm 专业版**
   - 完整的 Django 支持
   - 智能代码补全
   - 调试工具
   - 数据库工具
   - Git 集成

2. **VS Code + 插件**
   - Python 插件
   - Django 插件
   - Git 插件
   - SQLite 插件
   - 代码格式化插件

3. **配置建议**
   - 启用代码检查
   - 配置代码风格
   - 设置自动保存
   - 配置版本控制

#### 虚拟环境配置
1. **创建虚拟环境**
```bash
# 使用venv
python -m venv myproject_env

# 使用virtualenv
pip install virtualenv
virtualenv myproject_env
```

2. **激活虚拟环境**
```bash
# macOS/Linux
source myproject_env/bin/activate

# Windows
myproject_env\Scripts\activate
```

3. **管理依赖**
```bash
# 安装依赖
pip install -r requirements.txt

# 导出依赖
pip freeze > requirements.txt
```

### 1.3 第一个 Django 项目
#### 项目创建
1. **创建新项目**
```bash
django-admin startproject myproject
cd myproject
```

2. **项目结构说明**
```
myproject/
    ├── manage.py           # 项目管理脚本
    └── myproject/
        ├── __init__.py
        ├── settings.py     # 项目配置文件
        ├── urls.py         # URL配置文件
        ├── asgi.py         # ASGI配置
        └── wsgi.py         # WSGI配置
```

#### 基本配置
1. **settings.py 关键配置**
```python
# 数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# 时区和语言设置
LANGUAGE_CODE = 'zh-hans'
TIME_ZONE = 'Asia/Shanghai'
USE_I18N = True
USE_TZ = True

# 静态文件配置
STATIC_URL = 'static/'
STATIC_ROOT = BASE_DIR / 'static'
```

2. **创建应用**
```bash
python manage.py startapp myapp
```

3. **注册应用**
```python
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',  # 添加新创建的应用
]
```

#### 启动开发服务器
1. **运行迁移**
```bash
python manage.py migrate
```

2. **创建超级用户**
```bash
python manage.py createsuperuser
```

3. **启动服务器**
```bash
python manage.py runserver
```

#### Django Admin 初体验
1. **访问 Admin 界面**
- 打开浏览器访问：http://127.0.0.1:8000/admin/
- 使用超级用户账号登录

2. **创建模型**
```python
# myapp/models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    pub_date = models.DateTimeField('发布日期')

    def __str__(self):
        return self.title
```

3. **注册模型到 Admin**
```python
# myapp/admin.py
from django.contrib import admin
from .models import Article

admin.site.register(Article)
```

4. **应用数据库变更**
```bash
python manage.py makemigrations
python manage.py migrate
```

## 2. Django 核心概念
### 2.1 MVT 架构详解
Django 采用 MVT（Model-View-Template）架构模式，这是 MVC 模式的 Django 特色变体。

#### Model（模型）：数据库设计
1. **模型定义基础**
```python
from django.db import models

class User(models.Model):
    username = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        db_table = 'users'
        ordering = ['-created_at']
    
    def __str__(self):
        return self.username
```

2. **常用字段类型**
```python
class Product(models.Model):
    # 字符串字段
    name = models.CharField(max_length=200)
    description = models.TextField()
    
    # 数字字段
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField(default=0)
    
    # 日期时间字段
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    # 布尔字段
    is_active = models.BooleanField(default=True)
    
    # 文件字段
    image = models.ImageField(upload_to='products/')
    
    # 关系字段
    category = models.ForeignKey('Category', on_delete=models.CASCADE)
    tags = models.ManyToManyField('Tag')
```

3. **字段选项**
```python
class Article(models.Model):
    title = models.CharField(
        max_length=200,
        unique=True,           # 唯一性约束
        db_index=True,         # 创建数据库索引
        blank=True,            # 表单可以为空
        null=True,             # 数据库可以为空
        help_text='文章标题',   # 帮助文本
        verbose_name='标题'     # 人性化字段名
    )
```

4. **模型关系**
```python
# 一对多关系
class Category(models.Model):
    name = models.CharField(max_length=100)

class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE,
        related_name='products'
    )

# 多对多关系
class Tag(models.Model):
    name = models.CharField(max_length=50)

class Article(models.Model):
    tags = models.ManyToManyField(
        Tag,
        related_name='articles',
        through='ArticleTag'
    )

# 一对一关系
class UserProfile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name='profile'
    )
```

#### View（视图）：业务逻辑
1. **函数视图（FBV）**
```python
from django.shortcuts import render, redirect
from django.http import HttpResponse
from .models import Article

def article_list(request):
    articles = Article.objects.all()
    return render(request, 'articles/list.html', {'articles': articles})

def article_detail(request, pk):
    try:
        article = Article.objects.get(pk=pk)
    except Article.DoesNotExist:
        return HttpResponse("文章不存在", status=404)
    return render(request, 'articles/detail.html', {'article': article})

def article_create(request):
    if request.method == 'POST':
        # 处理表单提交
        title = request.POST.get('title')
        content = request.POST.get('content')
        Article.objects.create(title=title, content=content)
        return redirect('article_list')
    return render(request, 'articles/create.html')
```

2. **类视图（CBV）**
```python
from django.views.generic import ListView, DetailView, CreateView
from django.urls import reverse_lazy

class ArticleListView(ListView):
    model = Article
    template_name = 'articles/list.html'
    context_object_name = 'articles'
    paginate_by = 10
    
    def get_queryset(self):
        return Article.objects.filter(status='published')

class ArticleDetailView(DetailView):
    model = Article
    template_name = 'articles/detail.html'
    context_object_name = 'article'

class ArticleCreateView(CreateView):
    model = Article
    template_name = 'articles/create.html'
    fields = ['title', 'content']
    success_url = reverse_lazy('article_list')
```

3. **通用视图**
```python
from django.views.generic import (
    ListView, DetailView, CreateView,
    UpdateView, DeleteView
)

# 列表视图
class ProductListView(ListView):
    model = Product
    template_name = 'products/list.html'
    context_object_name = 'products'
    paginate_by = 12
    ordering = ['-created_at']

# 详情视图
class ProductDetailView(DetailView):
    model = Product
    template_name = 'products/detail.html'
    context_object_name = 'product'

# 创建视图
class ProductCreateView(CreateView):
    model = Product
    template_name = 'products/form.html'
    fields = ['name', 'price', 'description']
    success_url = reverse_lazy('product_list')

# 更新视图
class ProductUpdateView(UpdateView):
    model = Product
    template_name = 'products/form.html'
    fields = ['name', 'price', 'description']
    success_url = reverse_lazy('product_list')

# 删除视图
class ProductDeleteView(DeleteView):
    model = Product
    template_name = 'products/confirm_delete.html'
    success_url = reverse_lazy('product_list')
```

#### Template（模板）：前端展示
1. **基础模板语法**
```html
<!-- base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}默认标题{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <header>
        {% include 'includes/nav.html' %}
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        {% include 'includes/footer.html' %}
    </footer>
</body>
</html>
```

2. **模板继承**
```html
<!-- articles/list.html -->
{% extends 'base.html' %}

{% block title %}文章列表{% endblock %}

{% block content %}
<div class="articles">
    {% for article in articles %}
        <article class="article-item">
            <h2>{{ article.title }}</h2>
            <p>{{ article.content|truncatewords:30 }}</p>
            <span>发布时间：{{ article.created_at|date:"Y-m-d H:i" }}</span>
        </article>
    {% empty %}
        <p>暂无文章</p>
    {% endfor %}
</div>
{% endblock %}
```

3. **模板过滤器**
```html
<!-- 内置过滤器使用示例 -->
{{ value|length }}
{{ value|default:"暂无数据" }}
{{ value|date:"Y-m-d" }}
{{ value|truncatewords:100 }}
{{ value|safe }}
{{ value|striptags }}
```

4. **自定义模板标签和过滤器**
```python
# templatetags/custom_tags.py
from django import template
from datetime import datetime

register = template.Library()

@register.simple_tag
def current_time(format_string):
    return datetime.now().strftime(format_string)

@register.filter(name='cut')
def cut(value, arg):
    return value.replace(arg, '')
```

```html
<!-- 使用自定义标签和过滤器 -->
{% load custom_tags %}

<p>当前时间：{% current_time "%Y-%m-%d %H:%M:%S" %}</p>
<p>{{ text|cut:" " }}</p>
```

#### URL 配置：路由系统
1. **基本 URL 配置**
```python
# urls.py
from django.urls import path, include
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('articles/', views.article_list, name='article_list'),
    path('articles/<int:pk>/', views.article_detail, name='article_detail'),
    path('articles/create/', views.article_create, name='article_create'),
]
```

2. **URL 命名和命名空间**
```python
# myproject/urls.py
from django.urls import path, include

urlpatterns = [
    path('blog/', include('blog.urls', namespace='blog')),
    path('shop/', include('shop.urls', namespace='shop')),
]

# blog/urls.py
app_name = 'blog'  # 设置命名空间

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('<slug:slug>/', views.post_detail, name='post_detail'),
]
```

3. **URL 模式和转换器**
```python
from django.urls import path, register_converter

# 自定义 URL 转换器
class YearConverter:
    regex = '[0-9]{4}'
    
    def to_python(self, value):
        return int(value)
    
    def to_url(self, value):
        return str(value)

register_converter(YearConverter, 'yyyy')

urlpatterns = [
    path('articles/<yyyy:year>/', views.year_archive),
    path('articles/<yyyy:year>/<int:month>/', views.month_archive),
    path('articles/<slug:slug>/', views.article_detail),
]
```

4. **URL 反向解析**
```python
# 在视图中使用
from django.urls import reverse
from django.shortcuts import redirect

def my_view(request):
    return redirect(reverse('blog:post_detail', kwargs={'slug': 'hello-world'}))

# 在模板中使用
<a href="{% url 'blog:post_detail' slug='hello-world' %}">查看文章</a>
```

### 2.2 Django ORM 系统
1. **基本查询操作**
```python
# 创建对象
user = User.objects.create(
    username='john',
    email='john@example.com'
)

# 查询对象
users = User.objects.all()  # 查询所有
user = User.objects.get(id=1)  # 查询单个
users = User.objects.filter(age__gt=18)  # 条件查询

# 更新对象
User.objects.filter(id=1).update(username='john_doe')

# 删除对象
User.objects.filter(id=1).delete()
```

2. **高级查询**
```python
from django.db.models import Q, F, Count, Sum

# Q 对象 - 复杂查询
User.objects.filter(
    Q(age__gte=18) & Q(age__lte=65)
)

# F 对象 - 字段比较
Product.objects.filter(
    stock__lt=F('min_stock')
)

# 聚合查询
orders = Order.objects.annotate(
    total_items=Count('items'),
    total_amount=Sum('items__price')
)
```

3. **查询优化**
```python
# 使用 select_related 减少数据库查询
articles = Article.objects.select_related('author').all()

# 使用 prefetch_related 处理多对多关系
articles = Article.objects.prefetch_related('tags').all()

# 只获取需要的字段
users = User.objects.only('username', 'email')

# 延迟加载字段
users = User.objects.defer('biography')
```

4. **事务管理**
```python
from django.db import transaction

# 使用装饰器
@transaction.atomic
def transfer_money(from_account, to_account, amount):
    from_account.balance -= amount
    from_account.save()
    
    to_account.balance += amount
    to_account.save()

# 使用上下文管理器
def complex_operation():
    with transaction.atomic():
        # 执行多个数据库操作
        pass
```

## 3. Django 高级特性
### 3.1 表单处理
#### Form 类使用
1. **基础表单**
```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
    subscribe = forms.BooleanField(required=False)
    
    def clean_email(self):
        email = self.cleaned_data['email']
        if not email.endswith('@example.com'):
            raise forms.ValidationError('必须使用 example.com 邮箱')
        return email
```

2. **在视图中使用表单**
```python
def contact_view(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # 处理表单数据
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            # 发送邮件或保存到数据库
            return redirect('success_page')
    else:
        form = ContactForm()
    return render(request, 'contact.html', {'form': form})
```

3. **表单模板**
```html
<form method="post">
    {% csrf_token %}
    {{ form.non_field_errors }}
    
    <div class="form-group">
        {{ form.name.label_tag }}
        {{ form.name }}
        {{ form.name.errors }}
    </div>
    
    <div class="form-group">
        {{ form.email.label_tag }}
        {{ form.email }}
        {{ form.email.errors }}
    </div>
    
    <div class="form-group">
        {{ form.message.label_tag }}
        {{ form.message }}
        {{ form.message.errors }}
    </div>
    
    <button type="submit">提交</button>
</form>
```

#### ModelForm
1. **创建 ModelForm**
```python
from django.forms import ModelForm
from .models import Article

class ArticleForm(ModelForm):
    class Meta:
        model = Article
        fields = ['title', 'content', 'category', 'tags']
        # 或者使用 exclude 排除字段
        # exclude = ['author', 'created_at']
        
        widgets = {
            'title': forms.TextInput(attrs={'class': 'form-control'}),
            'content': forms.Textarea(attrs={'class': 'form-control'}),
            'category': forms.Select(attrs={'class': 'form-control'}),
            'tags': forms.SelectMultiple(attrs={'class': 'form-control'}),
        }
        
        labels = {
            'title': '标题',
            'content': '内容',
            'category': '分类',
            'tags': '标签',
        }
        
        help_texts = {
            'title': '请输入文章标题',
            'content': '请输入文章内容',
        }
```

2. **在视图中使用 ModelForm**
```python
def article_create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES)
        if form.is_valid():
            article = form.save(commit=False)
            article.author = request.user
            article.save()
            form.save_m2m()  # 保存多对多关系
            return redirect('article_detail', pk=article.pk)
    else:
        form = ArticleForm()
    return render(request, 'article_form.html', {'form': form})

def article_update(request, pk):
    article = get_object_or_404(Article, pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES, instance=article)
        if form.is_valid():
            form.save()
            return redirect('article_detail', pk=article.pk)
    else:
        form = ArticleForm(instance=article)
    return render(request, 'article_form.html', {'form': form})
```

#### 表单验证
1. **字段级验证**
```python
from django import forms

class UserRegistrationForm(forms.Form):
    username = forms.CharField(max_length=100)
    email = forms.EmailField()
    password = forms.CharField(widget=forms.PasswordInput)
    confirm_password = forms.CharField(widget=forms.PasswordInput)
    
    def clean_username(self):
        username = self.cleaned_data['username']
        if User.objects.filter(username=username).exists():
            raise forms.ValidationError('用户名已存在')
        return username
    
    def clean_email(self):
        email = self.cleaned_data['email']
        if User.objects.filter(email=email).exists():
            raise forms.ValidationError('邮箱已被注册')
        return email
```

2. **表单级验证**
```python
def clean(self):
    cleaned_data = super().clean()
    password = cleaned_data.get('password')
    confirm_password = cleaned_data.get('confirm_password')
    
    if password and confirm_password and password != confirm_password:
        raise forms.ValidationError('两次输入的密码不一致')
    
    return cleaned_data
```

3. **自定义验证器**
```python
from django.core.validators import RegexValidator, MinLengthValidator

class ProfileForm(forms.ModelForm):
    phone = forms.CharField(
        validators=[
            RegexValidator(
                regex=r'^\d{11}$',
                message='请输入 11 位手机号码'
            )
        ]
    )
    bio = forms.CharField(
        widget=forms.Textarea,
        validators=[
            MinLengthValidator(10, '简介至少需要 10 个字符')
        ]
    )
```

#### 文件上传
1. **文件上传配置**
```python
# settings.py
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... 其他 URL 配置
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

2. **文件上传表单**
```python
class DocumentForm(forms.ModelForm):
    class Meta:
        model = Document
        fields = ['title', 'file']
        
    def clean_file(self):
        file = self.cleaned_data['file']
        # 检查文件大小
        if file.size > 5 * 1024 * 1024:  # 5MB
            raise forms.ValidationError('文件大小不能超过 5MB')
        # 检查文件类型
        ext = file.name.split('.')[-1].lower()
        if ext not in ['pdf', 'doc', 'docx']:
            raise forms.ValidationError('只允许上传 PDF 和 Word 文档')
        return file
```

3. **处理文件上传**
```python
def upload_document(request):
    if request.method == 'POST':
        form = DocumentForm(request.POST, request.FILES)
        if form.is_valid():
            document = form.save()
            return redirect('document_detail', pk=document.pk)
    else:
        form = DocumentForm()
    return render(request, 'upload_document.html', {'form': form})
```

### 3.2 用户认证与授权
#### 用户认证系统
1. **配置认证后端**
```python
# settings.py
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    'myapp.backends.EmailAuthBackend',  # 自定义认证后端
]
```

2. **自定义用户模型**
```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class CustomUser(AbstractUser):
    phone = models.CharField(max_length=11, unique=True)
    avatar = models.ImageField(upload_to='avatars/', null=True, blank=True)
    bio = models.TextField(max_length=500, blank=True)
    following = models.ManyToManyField(
        'self', 
        symmetrical=False,
        related_name='followers'
    )
    
    def get_followers_count(self):
        return self.followers.count()
```

3. **认证视图**
```python
# views.py
from django.contrib.auth import login, authenticate
from django.contrib.auth.decorators import login_required

def login_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('home')
    return render(request, 'login.html')

@login_required
def profile_view(request):
    return render(request, 'profile.html', {'user': request.user})
```

#### 权限管理
1. **自定义权限**
```python
class Article(models.Model):
    # ... 其他字段
    
    class Meta:
        permissions = [
            ("publish_article", "Can publish article"),
            ("review_article", "Can review article"),
        ]
```

2. **权限检查**
```python
from django.contrib.auth.decorators import permission_required
from django.contrib.auth.mixins import PermissionRequiredMixin

@permission_required('myapp.publish_article')
def publish_article(request):
    # ... 发布文章的逻辑

class ArticleUpdateView(PermissionRequiredMixin, UpdateView):
    model = Article
    permission_required = 'myapp.change_article'
    template_name = 'article_update.html'
```

3. **组权限**
```python
from django.contrib.auth.models import Group, Permission

# 创建权限组
editors_group = Group.objects.create(name='editors')

# 添加权限到组
permissions = Permission.objects.filter(
    codename__in=['add_article', 'change_article', 'delete_article']
)
editors_group.permissions.add(*permissions)

# 将用户添加到组
user.groups.add(editors_group)
```

### 3.3 缓存机制
#### 缓存配置
1. **缓存后端设置**
```python
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    }
}

# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
        'LOCATION': '127.0.0.1:11211',
    }
}
```

2. **缓存中间件**
```python
MIDDLEWARE = [
    'django.middleware.cache.UpdateCacheMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.cache.FetchFromCacheMiddleware',
]

CACHE_MIDDLEWARE_SECONDS = 300  # 缓存时间
```

#### 视图缓存
1. **装饰器方式**
```python
from django.views.decorators.cache import cache_page
from django.core.cache import cache

@cache_page(60 * 15)  # 缓存 15 分钟
def article_list(request):
    articles = Article.objects.all()
    return render(request, 'article_list.html', {'articles': articles})

def get_article(request, article_id):
    cache_key = f'article_{article_id}'
    article = cache.get(cache_key)
    
    if article is None:
        article = Article.objects.get(id=article_id)
        cache.set(cache_key, article, 3600)
    
    return article
```

2. **模板片段缓存**
```html
{% load cache %}

{% cache 300 sidebar request.user.id %}
    {# 侧边栏内容 #}
{% endcache %}
```

#### 底层缓存 API
```python
from django.core.cache import cache

# 设置缓存
cache.set('my_key', 'my_value', 300)  # 缓存 5 分钟

# 获取缓存
value = cache.get('my_key')

# 删除缓存
cache.delete('my_key')

# 清空所有缓存
cache.clear()

# 获取或设置
value = cache.get_or_set('my_key', 'my_value', 300)

# 递增/递减
cache.incr('my_counter')
cache.decr('my_counter')
```

#### RESTful API 开发
1. **REST 框架配置**
```python
# settings.py
INSTALLED_APPS = [
    # ...
    'rest_framework',
]

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}
```

2. **序列化器**
```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    author = serializers.ReadOnlyField(source='author.username')
    
    class Meta:
        model = Article
        fields = ['id', 'title', 'content', 'author', 'created_at']
        read_only_fields = ['created_at']
    
    def validate_title(self, value):
        if len(value) < 10:
            raise serializers.ValidationError('标题长度不能少于 10 个字符')
        return value

class CategorySerializer(serializers.ModelSerializer):
    articles = ArticleSerializer(many=True, read_only=True)
    
    class Meta:
        model = Category
        fields = ['id', 'name', 'articles']
```

3. **API 视图**
```python
from rest_framework import viewsets, permissions
from rest_framework.decorators import action
from rest_framework.response import Response

class ArticleViewSet(viewsets.ModelViewSet):
    queryset = Article.objects.all()
    serializer_class = ArticleSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                        IsAuthorOrReadOnly]
    
    def perform_create(self, serializer):
        serializer.save(author=self.request.user)
    
    def get_queryset(self):
        queryset = Article.objects.all()
        category = self.request.query_params.get('category', None)
        if category:
            queryset = queryset.filter(category_id=category)
        return queryset

    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        article = self.get_object()
        article.status = 'published'
        article.save()
        return Response({'status': 'published'})
```

4. **URL 配置**
```python
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register(r'articles', views.ArticleViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
```

5. **API 文档**
```python
# urls.py
from rest_framework.documentation import include_docs_urls

urlpatterns = [
    path('docs/', include_docs_urls(title='API 文档')),
]

# 使用 Swagger 文档
from drf_yasg.views import get_schema_view
from drf_yasg import openapi

schema_view = get_schema_view(
    openapi.Info(
        title="API 文档",
        default_version='v1',
        description="API 接口文档",
    ),
    public=True,
)

urlpatterns = [
    path('swagger/', schema_view.with_ui('swagger', cache_timeout=0)),
]
```

## 4. Django 最佳实践
### 4.1 项目结构优化
#### 标准项目结构
```
myproject/
├── manage.py
├── requirements/
│   ├── base.txt
│   ├── development.txt
│   └── production.txt
├── config/
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   ├── __init__.py
│   ├── accounts/
│   │   ├── __init__.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── urls.py
│   │   └── views.py
│   └── core/
│       ├── __init__.py
│       ├── apps.py
│       ├── models.py
│       └── utils.py
├── static/
├── media/
├── templates/
├── docs/
└── .env
```

#### 配置管理
1. **环境变量管理**
```python
# .env
DEBUG=True
SECRET_KEY=your-secret-key
DATABASE_URL=postgres://user:password@localhost:5432/dbname
REDIS_URL=redis://localhost:6379/1

# settings/base.py
from pathlib import Path
from decouple import config

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST', default='localhost'),
        'PORT': config('DB_PORT', default='5432'),
    }
}
```

2. **多环境配置**
```python
# settings/development.py
from .base import *

DEBUG = True
ALLOWED_HOSTS = ['localhost', '127.0.0.1']

INSTALLED_APPS += [
    'debug_toolbar',
]

MIDDLEWARE += [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]

# settings/production.py
from .base import *

DEBUG = False
ALLOWED_HOSTS = ['.example.com']

SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

### 4.2 性能优化
#### 数据库优化
1. **索引优化**
```python
class Article(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    slug = models.SlugField(unique=True)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    
    class Meta:
        indexes = [
            models.Index(fields=['title', 'created_at']),
            models.Index(fields=['author', '-created_at']),
        ]
```

2. **查询优化**
```python
# 使用 select_related 减少数据库查询
articles = Article.objects.select_related('author').all()

# 使用 prefetch_related 处理多对多关系
articles = Article.objects.prefetch_related('tags').all()

# 只获取需要的字段
users = User.objects.only('username', 'email')

# 延迟加载字段
users = User.objects.defer('biography')
```

#### 缓存策略
1. **多级缓存**
```python
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    },
    'local': {
        'BACKEND': 'django.core.cache.backends.locmem.LocMemCache',
        'LOCATION': 'unique-snowflake'
    }
}

# views.py
from django.core.cache import caches

def get_article(request, article_id):
    # 先查本地缓存
    local_cache = caches['local']
    article = local_cache.get(f'article_{article_id}')
    
    if article is None:
        # 查 Redis 缓存
        redis_cache = caches['default']
        article = redis_cache.get(f'article_{article_id}')
        
        if article is None:
            # 查数据库
            article = Article.objects.get(id=article_id)
            # 设置缓存
            redis_cache.set(f'article_{article_id}', article, 3600)
            local_cache.set(f'article_{article_id}', article, 300)
    
    return article
```

2. **缓存键管理**
```python
class CacheKeyManager:
    @staticmethod
    def get_article_key(article_id):
        return f'article:{article_id}'
    
    @staticmethod
    def get_user_articles_key(user_id):
        return f'user:{user_id}:articles'
    
    @staticmethod
    def invalidate_article_cache(article_id):
        cache.delete(CacheKeyManager.get_article_key(article_id))
```

#### 异步任务处理
1. **Celery 配置**
```python
# celery.py
from celery import Celery
import os

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings.production')

app = Celery('myproject')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()

# tasks.py
from celery import shared_task
from django.core.mail import send_mail

@shared_task
def send_notification_email(user_id, subject, message):
    user = User.objects.get(id=user_id)
    send_mail(
        subject,
        message,
        'from@example.com',
        [user.email],
        fail_silently=False,
    )
```

2. **异步任务使用**
```python
# views.py
from .tasks import send_notification_email

def article_publish(request, article_id):
    article = Article.objects.get(id=article_id)
    article.status = 'published'
    article.save()
    
    # 异步发送通知邮件
    send_notification_email.delay(
        article.author.id,
        '文章已发布',
        f'您的文章 {article.title} 已成功发布'
    )
```

### 4.3 安全防护
#### XSS 防护
1. **模板转义**
```html
<!-- 自动转义 -->
{{ user_input }}

<!-- 关闭转义 -->
{{ user_input|safe }}

<!-- 自定义过滤器 -->
{% load html_filters %}
{{ user_input|sanitize_html }}
```

2. **内容安全策略**
```python
# settings.py
CSP_DEFAULT_SRC = ("'self'",)
CSP_STYLE_SRC = ("'self'", "'unsafe-inline'")
CSP_SCRIPT_SRC = ("'self'", "'unsafe-inline'", "'unsafe-eval'")
CSP_IMG_SRC = ("'self'", "data:", "https:")
```

#### SQL 注入防护
1. **使用 ORM**
```python
# 安全的查询
User.objects.filter(username=username)

# 不安全的查询
User.objects.raw("SELECT * FROM auth_user WHERE username = '%s'" % username)

# 使用参数化查询
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute(
        "SELECT * FROM auth_user WHERE username = %s",
        [username]
    )
```

2. **表单验证**
```python
from django import forms

class UserSearchForm(forms.Form):
    username = forms.CharField(
        validators=[
            RegexValidator(
                r'^[a-zA-Z0-9_]+$',
                '用户名只能包含字母、数字和下划线'
            )
        ]
    )
```

#### 密码安全
1. **密码哈希**
```python
from django.contrib.auth.hashers import make_password, check_password

# 密码哈希
password = make_password('user_password')

# 密码验证
is_valid = check_password('user_password', hashed_password)
```

2. **密码策略**
```python
# settings.py
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        'OPTIONS': {
            'min_length': 8,
        }
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```

### 4.4 测试与部署
#### 单元测试
1. **模型测试**
```python
from django.test import TestCase
from .models import Article

class ArticleTests(TestCase):
    def setUp(self):
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def test_article_creation(self):
        self.assertEqual(self.article.title, 'Test Article')
        self.assertEqual(self.article.content, 'Test Content')
    
    def test_article_str_representation(self):
        self.assertEqual(str(self.article), 'Test Article')
```

2. **视图测试**
```python
from django.test import Client, TestCase
from django.urls import reverse

class ArticleViewTests(TestCase):
    def setUp(self):
        self.client = Client()
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def test_article_list_view(self):
        response = self.client.get(reverse('article_list'))
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'articles/list.html')
        self.assertContains(response, 'Test Article')
    
    def test_article_detail_view(self):
        response = self.client.get(
            reverse('article_detail', args=[self.article.id])
        )
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'articles/detail.html')
```

#### 集成测试
```python
from django.test import LiveServerTestCase
from selenium import webdriver
from selenium.webdriver.common.by import By

class ArticleIntegrationTest(LiveServerTestCase):
    def setUp(self):
        self.browser = webdriver.Chrome()
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def tearDown(self):
        self.browser.quit()
    
    def test_article_creation_flow(self):
        # 访问文章创建页面
        self.browser.get(f'{self.live_server_url}/articles/create/')
        
        # 填写表单
        title_input = self.browser.find_element(By.NAME, 'title')
        content_input = self.browser.find_element(By.NAME, 'content')
        submit_button = self.browser.find_element(By.CSS_SELECTOR, 'button[type="submit"]')
        
        title_input.send_keys('New Test Article')
        content_input.send_keys('New Test Content')
        submit_button.click()
        
        # 验证结果
        self.assertIn('New Test Article', self.browser.page_source)
```

#### 部署流程
1. **生产环境配置**
```python
# production.py
DEBUG = False
ALLOWED_HOSTS = ['.example.com']

# 静态文件配置
STATIC_ROOT = '/var/www/example.com/static/'
MEDIA_ROOT = '/var/www/example.com/media/'

# 数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST'),
        'PORT': config('DB_PORT'),
    }
}

# 缓存配置
CACHES = {
    'default': {
        'BACKEND': 'django_redis.cache.RedisCache',
        'LOCATION': config('REDIS_URL'),
        'OPTIONS': {
            'CLIENT_CLASS': 'django_redis.client.DefaultClient',
        }
    }
}
```

2. **Nginx 配置**
```nginx
upstream django {
    server unix:///run/gunicorn.sock;
}

server {
    listen 80;
    server_name example.com;
    
    location /static/ {
        alias /var/www/example.com/static/;
    }
    
    location /media/ {
        alias /var/www/example.com/media/;
    }
    
    location / {
        proxy_pass http://django;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_redirect off;
    }
}
```

3. **Gunicorn 配置**
```python
# gunicorn.conf.py
bind = 'unix:/run/gunicorn.sock'
workers = 4
worker_class = 'gevent'
max_requests = 1000
max_requests_jitter = 50
timeout = 30
keepalive = 2

# 日志配置
accesslog = '/var/log/gunicorn/access.log'
errorlog = '/var/log/gunicorn/error.log'
loglevel = 'info'
```

4. **部署脚本**
```bash
#!/bin/bash

# 更新代码
git pull origin main

# 安装依赖
pip install -r requirements/production.txt

# 收集静态文件
python manage.py collectstatic --noinput

# 数据库迁移
python manage.py migrate

# 重启服务
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```

#### 监控与维护
1. **日志配置**
```python
# settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {process:d} {thread:d} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/debug.log',
            'formatter': 'verbose',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
    },
}
```

2. **性能监控**
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start_time = time.time()
        response = self.get_response(request)
        duration = time.time() - start_time
        
        if duration > 1.0:  # 记录响应时间超过 1 秒的请求
            logger.warning(
                f'Slow request: {request.path} ({duration:.2f}s)'
            )
        
        return response
```

## 5. 实战项目开发
### 5.1 项目规划与设计
#### 需求分析
1. **用户需求收集**
```python
# 需求文档示例
"""
1. 用户功能
   - 用户注册与登录
   - 个人信息管理
   - 密码重置

2. 内容管理
   - 文章发布和编辑
   - 评论系统
   - 标签和分类

3. 社交功能
   - 关注用户
   - 点赞和收藏
   - 消息通知

4. 其他功能
   - 搜索功能
   - 数据统计
   - 后台管理
"""
```

2. **功能模块划分**
```python
# apps/users/models.py
class User(AbstractUser):
    nickname = models.CharField(max_length=50, blank=True)
    avatar = models.ImageField(upload_to='avatars/', blank=True)
    bio = models.TextField(max_length=500, blank=True)
    following = models.ManyToManyField(
        'self', 
        symmetrical=False,
        related_name='followers'
    )
    
    def get_followers_count(self):
        return self.followers.count()
```

#### 数据库设计
1. **ER 图设计**
```
用户表 (users_user)
+------------+--------------+
| id         | INT         |
| username   | VARCHAR     |
| email      | VARCHAR     |
| password   | VARCHAR     |
| nickname   | VARCHAR     |
| avatar     | VARCHAR     |
| created_at | DATETIME    |
+------------+--------------+

文章表 (articles_article)
+------------+--------------+
| id         | INT         |
| title      | VARCHAR     |
| content    | TEXT        |
| author_id  | INT (FK)    |
| created_at | DATETIME    |
| updated_at | DATETIME    |
+------------+--------------+

评论表 (comments_comment)
+------------+--------------+
| id         | INT         |
| content    | TEXT        |
| article_id | INT (FK)    |
| author_id  | INT (FK)    |
| created_at | DATETIME    |
+------------+--------------+
```

2. **索引设计**
```python
class Article(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    slug = models.SlugField(unique=True)
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    
    class Meta:
        indexes = [
            models.Index(fields=['title', 'created_at']),
            models.Index(fields=['author', '-created_at']),
        ]

class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        indexes = [
            models.Index(fields=['article', '-created_at']),
        ]
```

#### API 设计
1. **RESTful API 规范**
```python
# api/urls.py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register(r'articles', views.ArticleViewSet)
router.register(r'comments', views.CommentViewSet)

urlpatterns = [
    path('', include(router.urls)),
    path('users/profile/', views.UserProfileView.as_view()),
    path('articles/<int:pk>/like/', views.ArticleLikeView.as_view()),
]
```

2. **API 文档设计**
```python
from drf_yasg.utils import swagger_auto_schema
from rest_framework import viewsets

class ArticleViewSet(viewsets.ModelViewSet):
    @swagger_auto_schema(
        operation_description="获取文章列表",
        responses={
            200: ArticleSerializer(many=True),
            400: "请求参数错误",
            403: "没有权限访问"
        }
    )
    def list(self, request):
        """
        获取文章列表
        
        参数：
            page：页码
            size：每页数量
            category：分类 ID
            tag：标签 ID
        """
        pass
```

### 5.2 功能实现
#### 用户认证模块
1. **用户模型**
```python
# users/models.py
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    nickname = models.CharField(max_length=50, blank=True)
    avatar = models.ImageField(upload_to='avatars/', blank=True)
    bio = models.TextField(max_length=500, blank=True)
    following = models.ManyToManyField(
        'self', 
        symmetrical=False,
        related_name='followers'
    )
    
    def get_followers_count(self):
        return self.followers.count()
```

2. **认证视图**
```python
# users/views.py
from rest_framework import generics, permissions
from rest_framework.response import Response
from .serializers import UserSerializer

class UserRegistrationView(generics.CreateAPIView):
    permission_classes = (permissions.AllowAny,)
    serializer_class = UserSerializer
    
    def perform_create(self, serializer):
        user = serializer.save()
        # 发送欢迎邮件
        send_welcome_email.delay(user.id)

class UserProfileView(generics.RetrieveUpdateAPIView):
    permission_classes = (permissions.IsAuthenticated,)
    serializer_class = UserSerializer
    
    def get_object(self):
        return self.request.user
```

#### 文章管理模块
1. **文章模型**
```python
# articles/models.py
from django.db import models
from django.utils.text import slugify

class Article(models.Model):
    STATUS_CHOICES = (
        ('draft', '草稿'),
        ('published', '已发布'),
    )
    
    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    content = models.TextField()
    author = models.ForeignKey('users.User', on_delete=models.CASCADE)
    status = models.CharField(max_length=10, choices=STATUS_CHOICES)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(self.title)
        super().save(*args, **kwargs)
```

2. **文章视图**
```python
# articles/views.py
from rest_framework import viewsets, permissions
from rest_framework.decorators import action
from rest_framework.response import Response

class ArticleViewSet(viewsets.ModelViewSet):
    queryset = Article.objects.all()
    serializer_class = ArticleSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                        IsAuthorOrReadOnly]
    
    def perform_create(self, serializer):
        serializer.save(author=self.request.user)
    
    def get_queryset(self):
        queryset = Article.objects.all()
        category = self.request.query_params.get('category', None)
        if category:
            queryset = queryset.filter(category_id=category)
        return queryset

    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        article = self.get_object()
        article.status = 'published'
        article.save()
        return Response({'status': 'published'})
```

#### 评论系统
1. **评论模型**
```python
# comments/models.py
from django.db import models

class Comment(models.Model):
    article = models.ForeignKey(
        'articles.Article',
        on_delete=models.CASCADE,
        related_name='comments'
    )
    author = models.ForeignKey(
        'users.User',
        on_delete=models.CASCADE
    )
    parent = models.ForeignKey(
        'self',
        null=True,
        blank=True,
        on_delete=models.CASCADE,
        related_name='replies'
    )
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        ordering = ['-created_at']
```

2. **评论视图**
```python
# comments/views.py
from rest_framework import generics, permissions
from rest_framework.response import Response

class CommentCreateView(generics.CreateAPIView):
    queryset = Comment.objects.all()
    serializer_class = CommentSerializer
    permission_classes = [permissions.IsAuthenticated]
    
    def perform_create(self, serializer):
        article_id = self.kwargs.get('article_id')
        serializer.save(
            author=self.request.user,
            article_id=article_id
        )

class CommentListView(generics.ListAPIView):
    serializer_class = CommentSerializer
    
    def get_queryset(self):
        article_id = self.kwargs.get('article_id')
        return Comment.objects.filter(
            article_id=article_id,
            parent=None
        )
```

### 5.3 前端开发
#### 模板设计
1. **基础模板**
```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
    {% block extra_css %}{% endblock %}
</head>
<body>
    <header>
        {% include 'includes/header.html' %}
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        {% include 'includes/footer.html' %}
    </footer>
    
    <script src="{% static 'js/main.js' %}"></script>
    {% block extra_js %}{% endblock %}
</body>
</html>
```

2. **文章列表模板**
```html
<!-- templates/articles/list.html -->
{% extends 'base.html' %}

{% block content %}
<div class="article-list">
    {% for article in articles %}
    <article class="article-item">
        <h2><a href="{% url 'article_detail' article.slug %}">
            {{ article.title }}
        </a></h2>
        <div class="article-meta">
            <span>{{ article.author.nickname }}</span>
            <span>{{ article.created_at|date:"Y-m-d" }}</span>
        </div>
        <div class="article-excerpt">
            {{ article.content|truncatewords:50 }}
        </div>
    </article>
    {% empty %}
        <p>暂无文章</p>
    {% endfor %}
    
    {% include 'includes/pagination.html' %}
</div>
{% endblock %}
```

#### 静态文件管理
1. **CSS 组织**
```scss
// static/scss/main.scss
// 变量定义
$primary-color: #007bff;
$secondary-color: #6c757d;
$success-color: #28a745;

// 混合器
@mixin button-variant($color, $background) {
    color: $color;
    background-color: $background;
    &:hover {
        background-color: darken($background, 10%);
    }
}

// 组件样式
.button {
    padding: 8px 16px;
    border-radius: 4px;
    border: none;
    cursor: pointer;
    
    &.primary {
        @include button-variant(white, $primary-color);
    }
    
    &.secondary {
        @include button-variant(white, $secondary-color);
    }
}

// 布局样式
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 15px;
}

// 响应式设计
@media (max-width: 768px) {
    .container {
        padding: 0 10px;
    }
}
```

2. **JavaScript 模块化**
```javascript
// static/js/modules/api.js
import axios from 'axios';

const api = axios.create({
    baseURL: '/api/',
    headers: {
        'Content-Type': 'application/json',
    },
});

export default api;

// static/js/main.js
import api from './modules/api.js';

document.addEventListener('DOMContentLoaded', () => {
    // 评论提交处理
    const commentForm = document.querySelector('#comment-form');
    if (commentForm) {
        commentForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const content = e.target.content.value;
            const articleId = e.target.dataset.articleId;
            
            try {
                const comment = await api.createComment(articleId, content);
                // 更新评论列表
                updateCommentList(comment.data);
            } catch (error) {
                console.error('评论提交失败：', error);
            }
        });
    }
});
```

### 5.4 测试与部署
#### 单元测试
```python
# articles/tests.py
from django.test import TestCase
from django.urls import reverse
from rest_framework.test import APIClient
from .models import Article

class ArticleTests(TestCase):
    def setUp(self):
        self.user = User.objects.create_user(
            username='testuser',
            password='testpass123'
        )
        self.client = APIClient()
        self.client.force_authenticate(user=self.user)
        
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content',
            author=self.user
        )
    
    def test_create_article(self):
        url = reverse('article-list')
        data = {
            'title': 'New Article',
            'content': 'New Content',
        }
        response = self.client.post(url, data)
        self.assertEqual(response.status_code, 201)
        self.assertEqual(Article.objects.count(), 2)
    
    def test_update_article(self):
        url = reverse('article-detail', args=[self.article.id])
        data = {
            'title': 'Updated Title',
            'content': 'Updated Content',
        }
        response = self.client.patch(url, data)
        self.assertEqual(response.status_code, 200)
        self.article.refresh_from_db()
        self.assertEqual(self.article.title, 'Updated Title')
```

#### 性能测试
```python
# performance_tests.py
import locust
from locust import HttpUser, task, between

class BlogUser(HttpUser):
    wait_time = between(1, 2)
    
    def on_start(self):
        # 用户登录
        self.client.post("/api/auth/login/", {
            "username": "testuser",
            "password": "testpass123"
        })
    
    @task(3)
    def view_articles(self):
        self.client.get("/api/articles/")
    
    @task(1)
    def view_article_detail(self):
        article_id = 1  # 假设存在的文章 ID
        self.client.get(
            f"/api/articles/{article_id}/"
        )
    
    @task(1)
    def create_comment(self):
        article_id = 1
        self.client.post(
            f"/api/articles/{article_id}/comments/",
            {"content": "Test comment"}
        )
```

#### 部署配置
1. **Docker 配置**
```dockerfile
# Dockerfile
FROM python:3.9-slim

# 设置工作目录
WORKDIR /app

# 安装依赖
COPY requirements.txt .
RUN pip install -r requirements.txt

# 复制项目文件
COPY . .

# 收集静态文件
RUN python manage.py collectstatic --noinput

# 暴露端口
EXPOSE 8000

# 启动命令
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "config.wsgi:application"]
```

2. **Docker Compose**
```yaml
# docker-compose.yml
version: '3'

services:
  web:
    build: .
    command: gunicorn config.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - .:/app
      - static_volume:/app/static
      - media_volume:/app/media
    expose:
      - 8000
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://user:password@localhost:5432/dbname
      - REDIS_URL=redis://localhost:6379/1
  
  db:
    image: postgres:13
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=dbname
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
  
  redis:
    image: redis:6
    volumes:
      - redis_data:/data
  
  nginx:
    image: nginx:1.19
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
      - static_volume:/app/static
      - media_volume:/app/media
    ports:
      - "80:80"
    depends_on:
      - web

volumes:
  postgres_data:
  redis_data:
  static_volume:
  media_volume:
```

3. **CI/CD 配置**
```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script:
    - pip install -r requirements.txt
    - python manage.py test
  
build:
  stage: build
  script:
    - docker build -t blog-app .
  only:
    - master
    
deploy:
  stage: deploy
  script:
    - docker-compose up -d
  environment:
    name: production
  only:
    - master

```

#### 监控与维护
1. **日志配置**
```python
# settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {process:d} {thread:d} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/debug.log',
            'formatter': 'verbose',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
    },
}

```

2. **性能监控**
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start_time = time.time()
        response = self.get_response(request)
        duration = time.time() - start_time
        
        if duration > 1.0:  # 记录响应时间超过 1 秒的请求
            logger.warning(
                f'Slow request: {request.path} ({duration:.2f}s)'
            )
        
        return response
```

## 6. Django 进阶话题
### 6.1 Django 扩展应用
#### 常用第三方包
1. **Django REST framework**
```python
# settings.py
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'rest_framework.authtoken',
]

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}
```

2. **Django Channels**
```python
# settings.py
INSTALLED_APPS = [
    'channels',
    # ...
]

ASGI_APPLICATION = 'myproject.asgi.application'
CHANNEL_LAYERS = {
    'default': {
        'BACKEND': 'channels_redis.core.RedisChannelLayer',
        'CONFIG': {
            "hosts": [('127.0.0.1', 6379)],
        }
    }
}

# consumers.py
from channels.generic.websocket import AsyncWebsocketConsumer
import json

class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.room_name = self.scope['url_route']['kwargs']['room_name']
        self.room_group_name = f'chat_{self.room_name}'

        await self.channel_layer.group_add(
            self.room_group_name,
            self.channel_name
        )
        await self.accept()

    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(
            self.room_group_name,
            self.channel_name
        )
```

3. **Django Celery**
```python
# celery.py
from celery import Celery
import os

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

app = Celery('myproject')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()

# tasks.py
from celery import shared_task
from django.core.mail import send_mail

@shared_task
def send_notification_email(user_id, subject, message):
    user = User.objects.get(id=user_id)
    send_mail(
        subject,
        message,
        'from@example.com',
        [user.email],
        fail_silently=False,
    )
```

#### 自定义中间件
1. **请求处理中间件**
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start_time = time.time()
        response = self.get_response(request)
        duration = time.time() - start_time
        
        if duration > 1.0:  # 记录响应时间超过 1 秒的请求
            logger.warning(
                f'Slow request: {request.path} ({duration:.2f}s)'
            )
        
        return response

class APIAuthMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        if request.path.startswith('/api/'):
            api_key = request.headers.get('X-API-Key')
            if not api_key:
                return HttpResponse("API key is required", status=401)
            
            # 验证 API key
            if not self.validate_api_key(api_key):
                return HttpResponse("Invalid API key", status=403)
        
        return self.get_response(request)
    
    def validate_api_key(self, api_key):
        # 实现 API key 验证逻辑
        return APIKey.objects.filter(key=api_key, is_active=True).exists()
```

2. **响应处理中间件**
```python
class ResponseFormatterMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        response = self.get_response(request)
        
        if hasattr(response, 'data') and isinstance(response.data, dict):
            response.data = {
                'code': response.status_code,
                'data': response.data,
                'message': 'success'
            }
        
        return response

# settings.py
MIDDLEWARE = [
    # ...
    'myapp.middleware.RequestTimeMiddleware',
    'myapp.middleware.APIAuthMiddleware',
    'myapp.middleware.ResponseFormatterMiddleware',
]
```

#### 信号系统
1. **自定义信号**
```python
# signals.py
from django.dispatch import Signal, receiver
from django.db.models.signals import post_save
from django.contrib.auth import get_user_model

# 定义自定义信号
article_published = Signal()
user_profile_updated = Signal()

# 信号接收器
@receiver(article_published)
def handle_article_published(sender, article, **kwargs):
    # 发送通知给作者的关注者
    followers = article.author.followers.all()
    for follower in followers:
        Notification.objects.create(
            user=follower,
            message=f'新文章发布：{article.title}'
        )

@receiver(post_save, sender=get_user_model())
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)

# 在视图中触发信号
def publish_article(request, article_id):
    article = Article.objects.get(id=article_id)
    article.status = 'published'
    article.save()
    
    # 触发信号
    article_published.send(
        sender=Article,
        article=article
    )
```

2. **内置信号使用**
```python
from django.db.models.signals import pre_save, post_delete
from django.dispatch import receiver

@receiver(pre_save, sender=Article)
def handle_article_pre_save(sender, instance, **kwargs):
    # 在保存文章前进行处理
    if not instance.slug:
        instance.slug = slugify(instance.title)

@receiver(post_delete, sender=Article)
def handle_article_post_delete(sender, instance, **kwargs):
    # 在删除文章后清理相关资源
    if instance.image:
        instance.image.delete(save=False)
```

#### 自定义命令
1. **基本命令**
```python
# management/commands/cleanup_sessions.py
from django.core.management.base import BaseCommand
from django.contrib.sessions.models import Session
from django.utils import timezone

class Command(BaseCommand):
    help = '清理过期的会话数据'

    def add_arguments(self, parser):
        parser.add_argument(
            '--days',
            type=int,
            default=30,
            help='清理指定天数之前的会话'
        )

    def handle(self, *args, **options):
        days = options['days']
        deadline = timezone.now() - timezone.timedelta(days=days)
        
        count, _ = Session.objects.filter(
            expire_date__lt=deadline
        ).delete()
        
        self.stdout.write(
            self.style.SUCCESS(f'成功删除 {count} 个过期会话')
        )
```

2. **数据处理命令**
```python
# management/commands/import_data.py
import csv
from django.core.management.base import BaseCommand
from myapp.models import Article

class Command(BaseCommand):
    help = '从 CSV 文件导入文章数据'

    def add_arguments(self, parser):
        parser.add_argument('csv_file', type=str, help='CSV 文件路径')
        parser.add_argument(
            '--update',
            action='store_true',
            help='更新已存在的记录'
        )

    def handle(self, *args, **options):
        csv_file = options['csv_file']
        update = options['update']
        
        with open(csv_file, 'r') as f:
            reader = csv.DictReader(f)
            for row in reader:
                try:
                    if update:
                        article, created = Article.objects.update_or_create(
                            title=row['title'],
                            defaults={
                                'content': row['content'],
                                'author_id': row['author_id']
                            }
                        )
                    else:
                        Article.objects.create(
                            title=row['title'],
                            content=row['content'],
                            author_id=row['author_id']
                        )
                    self.stdout.write(
                        self.style.SUCCESS(f'导入文章：{row["title"]}')
                    )
                except Exception as e:
                    self.stdout.write(
                        self.style.ERROR(f'导入失败：{row["title"]} - {str(e)}')
                    )
```

### 6.2 高级特性应用
#### 自定义模板标签和过滤器
1. **自定义模板标签**
```python
# templatetags/custom_tags.py
from django import template
from django.utils.safestring import mark_safe
import markdown

register = template.Library()

@register.simple_tag
def get_popular_articles(count=5):
    """获取热门文章列表"""
    from blog.models import Article
    return Article.objects.order_by('-views')[:count]

@register.filter(name='markdown')
def markdown_format(text):
    """将 Markdown 文本转换为 HTML"""
    return mark_safe(markdown.markdown(
        text,
        extensions=[
            'markdown.extensions.fenced_code',
            'markdown.extensions.tables',
            'markdown.extensions.toc'
        ]
    ))

@register.inclusion_tag('components/pagination.html')
def show_pagination(page_obj):
    """显示分页组件"""
    return {
        'page_obj': page_obj,
        'has_previous': page_obj.has_previous(),
        'has_next': page_obj.has_next(),
        'previous_page_number': page_obj.previous_page_number(),
        'next_page_number': page_obj.next_page_number(),
        'number': page_obj.number,
        'paginator': page_obj.paginator
    }
```

2. **自定义过滤器**
```python
@register.filter(name='time_since')
def time_since_filter(value):
    """显示时间差"""
    now = timezone.now()
    diff = now - value
    
    if diff.days > 365:
        return f'{diff.days // 365} 年前'
    elif diff.days > 30:
        return f'{diff.days // 30} 个月前'
    elif diff.days > 0:
        return f'{diff.days} 天前'
    elif diff.seconds > 3600:
        return f'{diff.seconds // 3600} 小时前'
    elif diff.seconds > 60:
        return f'{diff.seconds // 60} 分钟前'
    else:
        return '刚刚'
```

#### 自定义字段和管理器
1. **自定义字段**
```python
# fields.py
from django.db import models
import json

class JSONField(models.TextField):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)

    def from_db_value(self, value, expression, connection):
        if value is None:
            return None
        return json.loads(value)

    def to_python(self, value):
        if isinstance(value, dict):
            return value
        if value is None:
            return None
        return json.loads(value)

    def get_prep_value(self, value):
        if value is None:
            return None
        return json.dumps(value)

# models.py
class Article(models.Model):
    # ... 字段定义
    
    metadata = JSONField(default=dict)
```

2. **自定义管理器**
```python
class ArticleManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(status='published')
    
    def popular(self):
        return self.get_queryset().annotate(
            likes_count=Count('likes')
        ).order_by('-likes_count')
    
    def with_comments_count(self):
        return self.get_queryset().annotate(
            comments_count=Count('comments')
        )

class Article(models.Model):
    # ... 字段定义

    objects = models.Manager()
    published = ArticleManager()
```

#### 高级查询技巧
1. **复杂查询**
```python
from django.db.models import Q, F, Count, Avg, Max, Min, Sum

# Q 对象组合查询
Article.objects.filter(
    Q(status='published') &
    (Q(title__icontains='django') | Q(content__icontains='django'))
)

# F 对象字段比较
Article.objects.filter(likes_count__gt=F('comments_count') * 2)

# 聚合和注解
articles = Article.objects.annotate(
    year=ExtractYear('created_at')
).values('year').annotate(
    count=Count('id'),
    avg_likes=Avg('likes_count')
).order_by('year')
```

2. **原生 SQL**
```python
from django.db import connection

def get_article_stats():
    with connection.cursor() as cursor:
        cursor.execute("""
            SELECT 
                EXTRACT(YEAR FROM created_at) as year,
                COUNT(*) as total,
                AVG(likes_count) as avg_likes
            FROM blog_article
            WHERE status = 'published'
            GROUP BY EXTRACT(YEAR FROM created_at)
            ORDER BY year DESC
        """)
        columns = [col[0] for col in cursor.description]
        return [
            dict(zip(columns, row))
            for row in cursor.fetchall()
        ]
```

#### 高级视图技巧
1. **视图装饰器**
```python
from django.contrib.auth.decorators import login_required
from django.utils.decorators import method_decorator

@method_decorator(login_required, name='dispatch')
class ArticleCreateView(CreateView):
    model = Article
    template_name = 'article_form.html'
    fields = ['title', 'content']
    
    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)
```

2. **视图基类**
```python
class BaseView(View):
    def get_template(self):
        return 'base.html'
    
    def get_context_data(self):
        return {}
    
    def render(self, request, template_name=None, context=None):
        template_name = template_name or self.get_template()
        context = context or self.get_context_data()
        return HttpResponse(
            self.render_to_string(template_name, context),
            content_type='text/html'
        )
```

3. **视图组合**
```python
class ArticleView(View):
    def get(self, request, pk):
        article = Article.objects.get(id=pk)
        return HttpResponse(f'文章标题：{article.title}')
    
    def post(self, request, pk):
        article = Article.objects.get(id=pk)
        # 处理文章更新
        return HttpResponse('文章更新成功')

class CommentView(View):
    def get(self, request, pk):
        comment = Comment.objects.get(id=pk)
        return HttpResponse(f'评论内容：{comment.content}')
    
    def post(self, request, pk):
        comment = Comment.objects.get(id=pk)
        # 处理评论更新
        return HttpResponse('评论更新成功')
```

### 6.3 性能优化
#### 数据库优化
1. **索引优化**
```python
class Article(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    slug = models.SlugField(unique=True)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    
    class Meta:
        indexes = [
            models.Index(fields=['title', 'created_at']),
            models.Index(fields=['author', '-created_at']),
        ]
```

2. **缓存优化**
```python
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    }
}

# views.py
from django.core.cache import cache

def get_article(request, article_id):
    cache_key = f'article_{article_id}'
    article = cache.get(cache_key)
    
    if article is None:
        article = Article.objects.get(id=article_id)
        cache.set(cache_key, article, 3600)
    
    return article
```

3. **异步处理**
```python
# tasks.py
from celery import shared_task
from django.core.mail import send_mail

@shared_task
def send_notification_email(user_id, subject, message):
    user = User.objects.get(id=user_id)
    send_mail(
        subject,
        message,
        'from@example.com',
        [user.email],
        fail_silently=False,
    )
```

#### 前端优化
1. **静态文件优化**
```python
# settings.py
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

# urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... 其他 URL 配置
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

2. **模板优化**
```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
    {% block extra_css %}{% endblock %}
</head>
<body>
    <header>
        {% include 'includes/header.html' %}
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        {% include 'includes/footer.html' %}
    </footer>
    
    <script src="{% static 'js/main.js' %}"></script>
    {% block extra_js %}{% endblock %}
</body>
</html>
```

3. **JavaScript 优化**
```javascript
// static/js/main.js
import api from './modules/api.js';

document.addEventListener('DOMContentLoaded', () => {
    // 评论提交处理
    const commentForm = document.querySelector('#comment-form');
    if (commentForm) {
        commentForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const content = e.target.content.value;
            const articleId = e.target.dataset.articleId;
            
            try {
                const comment = await api.createComment(articleId, content);
                // 更新评论列表
                updateCommentList(comment.data);
            } catch (error) {
                console.error('评论提交失败：', error);
            }
        });
    }
});
```

### 6.4 安全防护
#### XSS 防护
1. **模板转义**
```html
<!-- 自动转义 -->
{{ user_input }}

<!-- 关闭转义 -->
{{ user_input|safe }}

<!-- 自定义过滤器 -->
{% load html_filters %}
{{ user_input|sanitize_html }}
```

2. **内容安全策略**
```python
# settings.py
CSP_DEFAULT_SRC = ("'self'",)
CSP_STYLE_SRC = ("'self'", "'unsafe-inline'")
CSP_SCRIPT_SRC = ("'self'", "'unsafe-inline'", "'unsafe-eval'")
CSP_IMG_SRC = ("'self'", "data:", "https:")
```

#### SQL 注入防护
1. **使用 ORM**
```python
# 安全的查询
User.objects.filter(username=username)

# 不安全的查询
User.objects.raw("SELECT * FROM auth_user WHERE username = '%s'" % username)

# 使用参数化查询
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute(
        "SELECT * FROM auth_user WHERE username = %s",
        [username]
    )
```

2. **表单验证**
```python
from django import forms

class UserSearchForm(forms.Form):
    username = forms.CharField(
        validators=[
            RegexValidator(
                r'^[a-zA-Z0-9_]+$',
                '用户名只能包含字母、数字和下划线'
            )
        ]
    )
```

#### 密码安全
1. **密码哈希**
```python
from django.contrib.auth.hashers import make_password, check_password

# 密码哈希
password = make_password('user_password')

# 密码验证
is_valid = check_password('user_password', hashed_password)
```

2. **密码策略**
```python
# settings.py
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        'OPTIONS': {
            'min_length': 8,
        }
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```

### 6.5 测试与部署
#### 单元测试
1. **模型测试**
```python
from django.test import TestCase
from .models import Article

class ArticleTests(TestCase):
    def setUp(self):
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def test_article_creation(self):
        self.assertEqual(self.article.title, 'Test Article')
        self.assertEqual(self.article.content, 'Test Content')
    
    def test_article_str_representation(self):
        self.assertEqual(str(self.article), 'Test Article')
```

2. **视图测试**
```python
from django.test import Client, TestCase
from django.urls import reverse

class ArticleViewTests(TestCase):
    def setUp(self):
        self.client = Client()
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def test_article_list_view(self):
        response = self.client.get(reverse('article_list'))
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'articles/list.html')
        self.assertContains(response, 'Test Article')
    
    def test_article_detail_view(self):
        response = self.client.get(
            reverse('article_detail', args=[self.article.id])
        )
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'articles/detail.html')
```

#### 集成测试
```python
from django.test import LiveServerTestCase
from selenium import webdriver
from selenium.webdriver.common.by import By

class ArticleIntegrationTest(LiveServerTestCase):
    def setUp(self):
        self.browser = webdriver.Chrome()
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )
    
    def tearDown(self):
        self.browser.quit()
    
    def test_article_creation_flow(self):
        # 访问文章创建页面
        self.browser.get(f'{self.live_server_url}/articles/create/')
        
        # 填写表单
        title_input = self.browser.find_element(By.NAME, 'title')
        content_input = self.browser.find_element(By.NAME, 'content')
        submit_button = self.browser.find_element(By.CSS_SELECTOR, 'button[type="submit"]')
        
        title_input.send_keys('New Test Article')
        content_input.send_keys('New Test Content')
        submit_button.click()
        
        # 验证结果
        self.assertIn('New Test Article', self.browser.page_source)
```

#### 部署流程
1. **生产环境配置**
```python
# production.py
DEBUG = False
ALLOWED_HOSTS = ['.example.com']

# 静态文件配置
STATIC_ROOT = '/var/www/example.com/static/'
MEDIA_ROOT = '/var/www/example.com/media/'

# 数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST'),
        'PORT': config('DB_PORT'),
    }
}

# 缓存配置
CACHES = {
    'default': {
        'BACKEND': 'django_redis.cache.RedisCache',
        'LOCATION': config('REDIS_URL'),
        'OPTIONS': {
            'CLIENT_CLASS': 'django_redis.client.DefaultClient',
        }
    }
}
```

2. **Nginx 配置**
```nginx
upstream django {
    server unix:///run/gunicorn.sock;
}

server {
    listen 80;
    server_name example.com;
    
    location / {
        proxy_pass http://django;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_redirect off;
    }

    location /static/ {
        alias /var/www/example.com/static/;
    }

    location /media/ {
        alias /var/www/example.com/media/;
    }
}
```

3. **Gunicorn 配置**
```python
# gunicorn.conf.py
bind = 'unix:/run/gunicorn.sock'
workers = 4
worker_class = 'gevent'
max_requests = 1000
max_requests_jitter = 50
timeout = 30
keepalive = 2

# 日志配置
accesslog = '/var/log/gunicorn/access.log'
errorlog = '/var/log/gunicorn/error.log'
loglevel = 'info'
```

4. **部署脚本**
```bash
#!/bin/bash

# 更新代码
git pull origin main

# 安装依赖
pip install -r requirements/production.txt

# 收集静态文件
python manage.py collectstatic --noinput

# 数据库迁移
python manage.py migrate

# 重启服务
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```

#### 监控与维护
1. **日志配置**
```python
# settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {process:d} {thread:d} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/debug.log',
            'formatter': 'verbose',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
    },
}
```

2. **性能监控**
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start_time = time.time()
        response = self.get_response(request)
        duration = time.time() - start_time
        
        if duration > 1.0:  # 记录响应时间超过 1 秒的请求
            logger.warning(
                f'Slow request: {request.path} ({duration:.2f}s)'
            )
        
        return response
```

## 7. Django 最佳实践与问题解决
### 7.1 项目结构与代码组织
#### 项目结构
推荐的 Django 项目结构如下：

```
myproject/
├── manage.py
├── requirements/
│   ├── base.txt
│   ├── development.txt
│   └── production.txt
├── myproject/
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── apps/
│   ├── __init__.py
│   ├── accounts/
│   │   ├── __init__.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── urls.py
│   │   └── views.py
│   └── core/
│       ├── __init__.py
│       ├── apps.py
│       ├── models.py
│       └── utils.py
├── static/
├── media/
├── templates/
├── docs/
└── .env
```

#### 配置管理
1. **环境配置分离**
```python
# .env
DEBUG=True
SECRET_KEY=your-secret-key
DATABASE_URL=postgres://user:password@localhost:5432/dbname
REDIS_URL=redis://localhost:6379/1

# settings/base.py
from pathlib import Path
from decouple import config

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST', default='localhost'),
        'PORT': config('DB_PORT', default='5432'),
    }
}
```

2. **多环境配置**
```python
# settings/development.py
from .base import *

DEBUG = True
ALLOWED_HOSTS = ['localhost', '127.0.0.1']

INSTALLED_APPS += [
    'debug_toolbar',
]

MIDDLEWARE += [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]

# settings/production.py
from .base import *

DEBUG = False
ALLOWED_HOSTS = ['.example.com']

SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

### 7.2 代码质量与规范
#### 代码风格
1. **PEP 8 规范**
```python
# 正确的导入顺序
import os
import sys
from datetime import datetime

from django.conf import settings
from django.db import models
from django.utils import timezone

from .models import Article
from .utils import format_date

# 类定义
class Article(models.Model):
    """文章模型类
    
    用于存储博客文章的基本信息，包括标题、内容、作者等。
    """
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.ForeignKey(
        'auth.User',
        on_delete=models.CASCADE,
        related_name='articles'
    )
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    class Meta:
        ordering = ['-created_at']
        verbose_name = '文章'
        verbose_name_plural = '文章列表'
    
    def __str__(self):
        return self.title
    
    def get_absolute_url(self):
        return reverse('article_detail', kwargs={'pk': self.pk})
```

2. **文档规范**
```python
def calculate_reading_time(content):
    """计算文章阅读时间
    
    Args:
        content (str): 文章内容
    
    Returns:
        int: 预计阅读时间（分钟）
    
    Examples:
        >>> content = "这是一篇测试文章..."
        >>> calculate_reading_time(content)
        2
    """
    words = len(content)
    minutes = round(words / 500)  # 假设阅读速度为每分钟 500 字
    return max(1, minutes)  # 最少 1 分钟
```

### 7.3 常见问题与解决方案
#### 性能问题
1. **N+1 查询问题**
```python
# 错误示例
def article_list(request):
    articles = Article.objects.all()
    for article in articles:
        print(article.author.username)  # 每次循环都会查询数据库

# 正确示例
def article_list(request):
    articles = Article.objects.select_related('author').all()
    for article in articles:
        print(article.author.username)  # 只查询一次数据库
```

2. **内存泄漏**
```python
# 错误示例
def process_articles():
    articles = []
    for i in range(1000000):
        article = Article.objects.create(title=f'Article {i}')
        articles.append(article)  # 内存持续增长
    return articles

# 正确示例
def process_articles():
    for i in range(1000000):
        article = Article.objects.create(title=f'Article {i}')
        yield article  # 使用生成器避免内存积累
```

#### 并发问题
1. **竞态条件**
```python
from django.db import transaction
from django.db.models import F

# 错误示例
def increase_views(article_id):
    article = Article.objects.get(id=article_id)
    article.views += 1  # 可能导致竞态条件
    article.save()

# 正确示例
def increase_views(article_id):
    Article.objects.filter(id=article_id).update(
        views=F('views') + 1
    )

# 使用事务
@transaction.atomic
def transfer_points(from_user_id, to_user_id, points):
    with transaction.atomic():
        from_user = User.objects.select_for_update().get(id=from_user_id)
        to_user = User.objects.select_for_update().get(id=to_user_id)
        
        if from_user.points >= points:
            from_user.points -= points
            to_user.points += points
            from_user.save()
            to_user.save()
            return True
        return False
```

## 8. Django 高级特性与扩展开发
### 8.1 高级 ORM 技巧
#### 复杂查询
1. **聚合查询**
```python
from django.db.models import Count, Avg, Max, Min, Sum, F, Q
from django.db.models.functions import ExtractYear, ExtractMonth

# 按年份统计文章数量和平均点赞数
articles_stats = Article.objects.annotate(
    year=ExtractYear('created_at')
).values('year').annotate(
    count=Count('id'),
    avg_likes=Avg('likes_count')
).order_by('year')

# 统计每个作者的文章数和总阅读量
author_stats = User.objects.annotate(
    articles_count=Count('articles'),
    total_views=Sum('articles__views'),
    max_likes=Max('articles__likes_count')
).filter(articles_count__gt=0)

# 复杂条件查询
popular_articles = Article.objects.filter(
    Q(status='published') &
    (Q(views__gt=1000) | Q(likes_count__gt=100))
).exclude(
    created_at__lt='2024-01-01'
)
```

2. **子查询**
```python
from django.db.models import Subquery, OuterRef, Exists

# 获取每个作者最新的文章
latest_articles = Article.objects.filter(
    author=OuterRef('pk')
).order_by('-created_at')

authors = User.objects.annotate(
    latest_article_title=Subquery(
        latest_articles.values('title')[:1]
    )
)

# 查找有评论的文章
articles_with_comments = Article.objects.annotate(
    has_comments=Exists(
        Comment.objects.filter(article=OuterRef('pk'))
    )
).filter(has_comments=True)
```

#### 高级模型特性
1. **抽象基类**
```python
class TimeStampedModel(models.Model):
    """抽象基类，提供创建时间和更新时间字段"""
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True

class SoftDeleteModel(models.Model):
    """软删除模型基类"""
    is_deleted = models.BooleanField(default=False)
    deleted_at = models.DateTimeField(null=True, blank=True)

    class Meta:
        abstract = True

    def delete(self, using=None, keep_parents=False):
        self.is_deleted = True
        self.deleted_at = timezone.now()
        self.save()

class Article(TimeStampedModel, SoftDeleteModel):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
```

2. **自定义管理器**
```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(status='published')

    def popular(self):
        return self.get_queryset().filter(views__gt=1000)

class Article(models.Model):
    # ... 字段定义

    objects = models.Manager()
    published = PublishedManager()

    @property
    def is_popular(self):
        return self.views > 1000 or self.likes_count > 100
```

### 8.2 高级视图模式
#### 基于类的视图
1. **视图混入**
```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import ListView, DetailView

class AuthorRequiredMixin:
    """要求当前用户是对象的作者"""
    def dispatch(self, request, *args, **kwargs):
        obj = self.get_object()
        if obj.author != request.user:
            raise PermissionDenied
        return super().dispatch(request, *args, **kwargs)

class ArticleListView(LoginRequiredMixin, ListView):
    model = Article
    template_name = 'articles/list.html'
    context_object_name = 'articles'
    paginate_by = 10

    def get_queryset(self):
        queryset = super().get_queryset()
        if self.request.user.is_staff:
            return queryset
        return queryset.filter(status='published')

class ArticleDetailView(LoginRequiredMixin, AuthorRequiredMixin, DetailView):
    model = Article
    template_name = 'articles/detail.html'

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['comments'] = self.object.comments.all()
        return context
```

2. **自定义响应处理**
```python
from django.http import JsonResponse
from django.views import View

class APIView(View):
    """基础 API 视图"""
    def dispatch(self, request, *args, **kwargs):
        try:
            response = super().dispatch(request, *args, **kwargs)
            if isinstance(response, (dict, list)):
                return JsonResponse({
                    'status': 'success',
                    'data': response
                })
            return response
        except Exception as e:
            return JsonResponse({
                'status': 'error',
                'message': str(e)
            }, status=500)

class ArticleAPIView(APIView):
    def get(self, request, article_id):
        article = Article.objects.get(id=article_id)
        return {
            'id': article.id,
            'title': article.title,
            'content': article.content
        }

    def post(self, request):
        # 创建文章
        data = json.loads(request.body)
        article = Article.objects.create(
            title=data['title'],
            content=data['content'],
            author=request.user
        )
        return {'id': article.id}
```

### 8.3 高级模板开发
#### 自定义模板标签
1. **简单标签**
```python
# templatetags/custom_tags.py
from django import template
from django.utils.safestring import mark_safe
import markdown

register = template.Library()

@register.simple_tag
def get_popular_articles(count=5):
    """获取热门文章列表"""
    from blog.models import Article
    return Article.objects.order_by('-views')[:count]

@register.filter(name='markdown')
def markdown_format(text):
    """将 Markdown 文本转换为 HTML"""
    return mark_safe(markdown.markdown(
        text,
        extensions=[
            'markdown.extensions.fenced_code',
            'markdown.extensions.tables',
            'markdown.extensions.toc'
        ]
    ))

@register.inclusion_tag('components/pagination.html')
def show_pagination(page_obj):
    """显示分页组件"""
    return {
        'page_obj': page_obj,
        'has_previous': page_obj.has_previous(),
        'has_next': page_obj.has_next(),
        'previous_page_number': page_obj.previous_page_number(),
        'next_page_number': page_obj.next_page_number(),
        'number': page_obj.number,
        'paginator': page_obj.paginator
    }
```

2. **包含标签**
```python
@register.inclusion_tag('tags/article_list.html')
def show_latest_articles(count=5):
    latest_articles = Article.objects.order_by('-created_at')[:count]
    return {'articles': latest_articles}

@register.inclusion_tag('tags/comment_form.html', takes_context=True)
def comment_form(context, article):
    request = context['request']
    return {
        'article': article,
        'user': request.user,
        'form': CommentForm()
    }
```

### 8.4 异步功能开发
#### 异步视图
1. **基本异步视图**
```python
import asyncio
from django.http import JsonResponse
from asgiref.sync import sync_to_async

async def async_article_list(request):
    articles = await sync_to_async(list)(
        Article.objects.select_related('author').all()
    )
    return JsonResponse({
        'articles': [
            {
                'id': article.id,
                'title': article.title,
                'author': article.author.username
            }
            for article in articles
        ]
    })

async def async_article_detail(request, article_id):
    get_article = sync_to_async(Article.objects.get)
    article = await get_article(id=article_id)
    return JsonResponse({
        'id': article.id,
        'title': article.title,
        'content': article.content
    })
```

2. **WebSocket 支持**
```python
# consumers.py
from channels.generic.websocket import AsyncWebsocketConsumer
import json

class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.room_name = self.scope['url_route']['kwargs']['room_name']
        self.room_group_name = f'chat_{self.room_name}'

        await self.channel_layer.group_add(
            self.room_group_name,
            self.channel_name
        )
        await self.accept()

    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(
            self.room_group_name,
            self.channel_name
        )

    async def receive(self, text_data):
        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type': 'chat_message',
                'message': text_data
            }
        )

    async def chat_message(self, event):
        message = event['message']

        await self.send(text_data=json.dumps({
            'message': message
        }))
```

### 8.5 高级缓存技术
#### 多级缓存
1. **缓存策略**
```python
from django.core.cache import caches
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator

# 设置多个缓存后端
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': 'redis://127.0.0.1:6379/1',
    },
    'local': {
        'BACKEND': 'django.core.cache.backends.locmem.LocMemCache',
    }
}

def get_article(request, article_id):
    # 先查本地缓存
    local_cache = caches['local']
    article = local_cache.get(f'article_{article_id}')
    
    if article is None:
        # 查 Redis 缓存
        redis_cache = caches['default']
        article = redis_cache.get(f'article_{article_id}')
        
        if article is None:
            # 查数据库
            article = Article.objects.get(id=article_id)
            # 设置缓存
            redis_cache.set(f'article_{article_id}', article, 3600)
            local_cache.set(f'article_{article_id}', article, 300)
    
    return article
```

2. **缓存模式**
```python
from django.core.cache import cache
from functools import wraps

def cache_method(timeout=300):
    def decorator(func):
        @wraps(func)
        def wrapper(self, *args, **kwargs):
            key = f"{self.__class__.__name__}.{func.__name__}"
            if args:
                key += f".{'.'.join(str(arg) for arg in args)}"
            if kwargs:
                key += f".{'.'.join(f'{k}={v}' for k, v in kwargs.items())}"
            
            result = cache.get(key)
            if result is None:
                result = func(self, *args, **kwargs)
                cache.set(key, result, timeout)
            return result
        return wrapper
    return decorator

class Article(models.Model):
    # ... 字段定义

    @cache_method(timeout=3600)
    def get_related_articles(self):
        return Article.objects.filter(
            tags__in=self.tags.all()
        ).exclude(id=self.id)[:5]

    @cache_method(timeout=1800)
    def get_comments_count(self):
        return self.comments.count()
```

### 8.6 API 开发最佳实践
#### RESTful API 设计
1. **视图集和序列化器**
```python
from rest_framework import viewsets, serializers, permissions
from rest_framework.decorators import action
from rest_framework.response import Response

class ArticleSerializer(serializers.ModelSerializer):
    author = serializers.ReadOnlyField(source='author.username')
    
    class Meta:
        model = Article
        fields = ['id', 'title', 'content', 'author', 'created_at']
        read_only_fields = ['created_at']
    
    def validate_title(self, value):
        if len(value) < 10:
            raise serializers.ValidationError('标题长度不能少于 10 个字符')
        return value

class CategorySerializer(serializers.ModelSerializer):
    articles = ArticleSerializer(many=True, read_only=True)
    
    class Meta:
        model = Category
        fields = ['id', 'name', 'articles']
```

2. **API 版本控制**
```python
# urls.py
from rest_framework import routers
from django.urls import path, include

router_v1 = routers.DefaultRouter()
router_v1.register(r'articles', ArticleViewSetV1)

router_v2 = routers.DefaultRouter()
router_v2.register(r'articles', ArticleViewSetV2)

urlpatterns = [
    path('api/v1/', include(router_v1.urls)),
    path('api/v2/', include(router_v2.urls)),
]

# views.py
class ArticleViewSetV1(viewsets.ModelViewSet):
    queryset = Article.objects.all()
    serializer_class = ArticleSerializerV1

class ArticleViewSetV2(viewsets.ModelViewSet):
    queryset = Article.objects.all()
    serializer_class = ArticleSerializerV2

    def get_serializer_class(self):
        if self.action == 'list':
            return ArticleListSerializerV2
        return ArticleSerializerV2
```

## 9. Django 测试、部署和性能优化

### 9.1 测试最佳实践
Django 的测试框架建立在 Python 的 unittest 模块之上，提供了丰富的测试工具和方法。

#### 1. 单元测试
```python
from django.test import TestCase
from django.contrib.auth.models import User
from .models import Article

class ArticleTest(TestCase):
    def setUp(self):
        self.user = User.objects.create_user(
            username='testuser',
            password='12345'
        )
        self.article = Article.objects.create(
            title='Test Article',
            content='Test Content'
        )

    def test_article_creation(self):
        self.assertEqual(self.article.title, 'Test Article')
        self.assertEqual(self.article.author, self.user)

    def test_article_str(self):
        self.assertEqual(str(self.article), 'Test Article')
```

#### 2. API 测试
```python
from rest_framework.test import APITestCase
from rest_framework import status

class ArticleAPITest(APITestCase):
    def setUp(self):
        self.user = User.objects.create_user(
            username='testuser',
            password='12345'
        )
        self.client.force_authenticate(user=self.user)

    def test_create_article(self):
        data = {'title': 'New Article', 'content': 'Content'}
        response = self.client.post('/api/articles/', data)
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)
        self.assertEqual(Article.objects.count(), 1)
```

#### 3. 性能测试
```python
from django.test import TestCase
from django.test.utils import CaptureQueriesContext
from django.db import connection
import time

class PerformanceTest(TestCase):
    def test_efficient_querying(self):
        with CaptureQueriesContext(connection) as context:
            response = self.client.get('/api/articles/')
            self.assertLess(len(context), 5)  # 确保查询次数在合理范围

    def test_bulk_operations(self):
        start_time = time.time()
        Article.objects.bulk_create([
            Article(title=f'Article {i}', author=self.user)
            for i in range(100)
        ])
        duration = time.time() - start_time
        self.assertLess(duration, 1.0)  # 确保批量操作效率
```

### 9.2 部署最佳实践
#### 1. Docker 部署
```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app
ENV PYTHONUNBUFFERED 1

RUN apt-get update && apt-get install -y \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
RUN python manage.py collectstatic --noinput

EXPOSE 8000
CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  web:
    build: .
    command: gunicorn myproject.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://postgres:postgres@db:5432/myproject

  db:
    image: postgres:13
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=myproject
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres

volumes:
  postgres_data:
```

#### 2. Nginx 配置
```nginx
upstream django {
    server web:8000;
}

server {
    listen 80;
    server_name example.com;
    
    location / {
        proxy_pass http://django;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_redirect off;
    }

    location /static/ {
        alias /app/static/;
    }

    location /media/ {
        alias /app/media/;
    }
}
```

#### 3. Gunicorn 配置
```python
# gunicorn.conf.py
bind = 'unix:/run/gunicorn.sock'
workers = 4
worker_class = 'gevent'
max_requests = 1000
max_requests_jitter = 50
timeout = 30
keepalive = 2

# 日志配置
accesslog = '/var/log/gunicorn/access.log'
errorlog = '/var/log/gunicorn/error.log'
loglevel = 'info'
```

#### 4. 部署脚本
```bash
#!/bin/bash

# 更新代码
git pull origin main

# 安装依赖
pip install -r requirements/production.txt

# 收集静态文件
python manage.py collectstatic --noinput

# 数据库迁移
python manage.py migrate

# 重启服务
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```

#### 监控与维护
1. **日志配置**
```python
# settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {process:d} {thread:d} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/debug.log',
            'formatter': 'verbose',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
    },
}
```

2. **性能监控**
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        start_time = time.time()
        response = self.get_response(request)
        duration = time.time() - start_time
        
        if duration > 1.0:  # 记录响应时间超过 1 秒的请求
            logger.warning(
                f'Slow request: {request.path} ({duration:.2f}s)'
            )
        
        return response
```

### 9.3 性能优化

#### 1. 数据库优化
```python
# 使用 select_related 减少查询
articles = Article.objects.select_related('author').all()

# 使用 prefetch_related 处理多对多关系
articles = Article.objects.prefetch_related('tags').all()

# 批量操作
Article.objects.bulk_create(articles)
Article.objects.bulk_update(articles, ['title'])

# 添加索引
class Article(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['created_at', 'status']),
        ]
```

#### 2. 缓存优化
```python
from django.core.cache import cache
from django.views.decorators.cache import cache_page

# 视图缓存
@cache_page(60 * 15)  # 缓存 15 分钟
def article_list(request):
    articles = Article.objects.all()
    return render(request, 'article_list.html', {'articles': articles})

def get_article(request, article_id):
    cache_key = f'article_{article_id}'
    article = cache.get(cache_key)
    
    if article is None:
        article = Article.objects.get(id=article_id)
        cache.set(cache_key, article, 3600)
    
    return article
```

#### 3. 异步处理
```python
from channels.generic.websocket import AsyncWebsocketConsumer
import json

class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        await self.channel_layer.group_add(
            self.room_group_name,
            self.channel_name
        )
        await self.accept()

    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(
            self.room_group_name,
            self.channel_name
        )

    async def receive(self, text_data):
        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type': 'chat_message',
                'message': text_data
            }
        )
```

### 9.4 监控与日志

#### 1. 性能监控
```python
import time
from functools import wraps
from django.db import connection
import logging

logger = logging.getLogger('django.request')

def performance_monitor(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start_time = time.time()
        initial_queries = len(connection.queries)

        result = func(*args, **kwargs)

        end_time = time.time()
        execution_time = end_time - start_time
        queries_executed = len(connection.queries) - initial_queries

        logger.info(
            f'Function: {func.__name__}, '
            f'Time: {execution_time:.2f}s, '
            f'Queries: {queries_executed}'
        )

        return result
    return wrapper

@performance_monitor
def get_article_stats(article_id):
    article = Article.objects.get(id=article_id)
    return {
        'views': article.views,
        'likes': article.likes.count(),
        'comments': article.comments.count()
    }
```

#### 2. 日志配置
```python
# settings.py
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {process:d} {thread:d} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': '/var/log/django/debug.log',
            'formatter': 'verbose',
        },
        'mail_admins': {
            'level': 'ERROR',
            'class': 'django.utils.log.AdminEmailHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'INFO',
            'propagate': True,
        },
        'django.request': {
            'handlers': ['mail_admins'],
            'level': 'ERROR',
            'propagate': False,
        },
    },
}

```

Follow these instructions to make the following change to my code document.

Instruction: 添加第十章的第一部分（高级特性）

Code Edit:
```
### 10.1 高级特性应用

#### 1. 自定义管理命令
```python
# management/commands/cleanup_sessions.py
from django.core.management.base import BaseCommand
from django.contrib.sessions.models import Session
from django.utils import timezone

class Command(BaseCommand):
    help = '清理过期的会话数据'

    def add_arguments(self, parser):
        parser.add_argument(
            '--days',
            type=int,
            default=30,
            help='删除指定天数之前的会话'
        )

    def handle(self, *args, **options):
        days = options['days']
        deadline = timezone.now() - timezone.timedelta(days=days)
        
        count, _ = Session.objects.filter(
            expire_date__lt=deadline
        ).delete()
        
        self.stdout.write(
            self.style.SUCCESS(f'成功删除 {count} 个过期会话')
        )
```

#### 2. 自定义中间件
```python
# middleware.py
import time
import logging

logger = logging.getLogger('django.request')

class RequestTimeMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        # 请求到达时的时间
        start_time = time.time()
        
        # 处理请求
        response = self.get_response(request)
        
        # 请求处理完成的时间
        duration = time.time() - start_time
        
        # 记录处理时间超过阈值的请求
        if duration > settings.SLOW_REQUEST_THRESHOLD:
            logger.warning(
                f'Slow request detected: {request.path} '
                f'took {duration:.2f}s'
            )
        
        # 在响应头中添加处理时间
        response['X-Request-Duration'] = str(duration)
        return response

class APIThrottleMiddleware:
    """API 访问频率限制中间件"""
    def __init__(self, get_response):
        self.get_response = get_response
        self.cache = {}

    def __call__(self, request):
        if request.path.startswith('/api/'):
            client_ip = request.META.get('REMOTE_ADDR')
            current_time = time.time()
            
            # 清理过期记录
            self.cleanup_old_requests(current_time)
            
            # 检查访问频率
            if self.is_rate_limited(client_ip, current_time):
                return JsonResponse({
                    'error': '请求过于频繁，请稍后再试'
                }, status=429)
            
            # 记录本次请求
            self.record_request(client_ip, current_time)
        
        return self.get_response(request)

    def cleanup_old_requests(self, current_time):
        cutoff_time = current_time - 60  # 清理1分钟前的记录
        self.cache = {
            ip: times for ip, times in self.cache.items()
            if any(t > cutoff_time for t in times)
        }

    def is_rate_limited(self, client_ip, current_time):
        if client_ip not in self.cache:
            return False
        
        # 获取最近1分钟内的请求次数
        recent_requests = len([
            t for t in self.cache[client_ip]
            if t > current_time - 60
        ])
        
        return recent_requests >= 60  # 每分钟最多60次请求

    def record_request(self, client_ip, current_time):
        if client_ip not in self.cache:
            self.cache[client_ip] = []
        self.cache[client_ip].append(current_time)
```

#### 3. 自定义模板标签和过滤器
```python
# templatetags/custom_tags.py
from django import template
from django.utils.safestring import mark_safe
import markdown

register = template.Library()

@register.simple_tag
def get_popular_articles(count=5):
    """获取热门文章列表"""
    from blog.models import Article
    return Article.objects.order_by('-views')[:count]

@register.filter(name='markdown')
def markdown_format(text):
    """将 Markdown 文本转换为 HTML"""
    return mark_safe(markdown.markdown(
        text,
        extensions=[
            'markdown.extensions.fenced_code',
            'markdown.extensions.tables',
            'markdown.extensions.toc'
        ]
    ))

@register.inclusion_tag('components/pagination.html')
def show_pagination(page_obj):
    """显示分页组件"""
    return {
        'page_obj': page_obj,
        'has_previous': page_obj.has_previous(),
        'has_next': page_obj.has_next(),
        'previous_page_number': page_obj.previous_page_number(),
        'next_page_number': page_obj.next_page_number(),
        'number': page_obj.number,
        'paginator': page_obj.paginator
    }
```

#### 4. 自定义表单字段和验证器
```python
from django import forms
from django.core.exceptions import ValidationError
from django.core.validators import RegexValidator

class ColorField(forms.CharField):
    """自定义颜色选择字段"""
    def __init__(self, *args, **kwargs):
        kwargs.setdefault('max_length', 7)
        super().__init__(*args, **kwargs)
        self.validators.append(
            RegexValidator(
                regex=r'^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$',
                message='请输入有效的十六进制颜色代码'
            )
        )

def validate_file_size(value):
    """验证上传文件大小"""
    limit = 5 * 1024 * 1024  # 5MB
    if value.size > limit:
        raise ValidationError('文件大小不能超过5MB')

class ArticleForm(forms.ModelForm):
    color_theme = ColorField(
        required=False,
        help_text='请输入十六进制颜色代码，例如：#FF0000'
    )
    attachment = forms.FileField(
        required=False,
        validators=[validate_file_size]
    )

    class Meta:
        model = Article
        fields = ['title', 'content', 'color_theme', 'attachment']

    def clean_title(self):
        title = self.cleaned_data['title']
        if len(title) < 10:
            raise ValidationError('标题长度不能少于10个字符')
        return title

    def clean(self):
        cleaned_data = super().clean()
        title = cleaned_data.get('title')
        content = cleaned_data.get('content')
        
        if title and content and title in content:
            raise ValidationError('文章内容不能包含标题')
        
        return cleaned_data
```

```

Follow these instructions to make the following change to my code document.

Instruction: 添加第十章的第二部分（实战案例）

Code Edit:
```
### 10.2 实战案例：在线教育平台

#### 1. 数据模型设计
```python
# courses/models.py
from django.db import models
from django.contrib.auth.models import User
from django.core.validators import MinValueValidator, MaxValueValidator

class Course(models.Model):
    title = models.CharField('课程标题', max_length=200)
    description = models.TextField('课程描述')
    instructor = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name='courses_teaching'
    )
    price = models.DecimalField(
        '课程价格',
        max_digits=7,
        decimal_places=2,
        validators=[MinValueValidator(0)]
    )
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    students = models.ManyToManyField(
        User,
        through='Enrollment',
        related_name='courses_enrolled'
    )

    class Meta:
        ordering = ['-created_at']

    def __str__(self):
        return self.title

    def get_absolute_url(self):
        return reverse('course_detail', args=[str(self.id)])

    def get_rating(self):
        ratings = self.ratings.aggregate(Avg('score'))
        return ratings.get('score__avg') or 0.0

class Lesson(models.Model):
    course = models.ForeignKey(
        Course,
        on_delete=models.CASCADE,
        related_name='lessons'
    )
    title = models.CharField('课时标题', max_length=200)
    content = models.TextField('课时内容')
    video_url = models.URLField('视频链接', blank=True)
    order = models.PositiveIntegerField('课时顺序', default=0)
    
    class Meta:
        ordering = ['order']
        unique_together = ['course', 'order']

class Enrollment(models.Model):
    student = models.ForeignKey(User, on_delete=models.CASCADE)
    course = models.ForeignKey(Course, on_delete=models.CASCADE)
    enrolled_at = models.DateTimeField(auto_now_add=True)
    completed = models.BooleanField(default=False)

    class Meta:
        unique_together = ['student', 'course']

class CourseRating(models.Model):
    course = models.ForeignKey(
        Course,
        on_delete=models.CASCADE,
        related_name='ratings'
    )
    student = models.ForeignKey(User, on_delete=models.CASCADE)
    score = models.IntegerField(
        validators=[
            MinValueValidator(1),
            MaxValueValidator(5)
        ]
    )
    comment = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        unique_together = ['course', 'student']
```

#### 2. API接口设计
```python
# courses/api/serializers.py
from rest_framework import serializers
from ..models import Course, Lesson, Enrollment, CourseRating

class CourseSerializer(serializers.ModelSerializer):
    rating = serializers.FloatField(source='get_rating', read_only=True)
    instructor_name = serializers.CharField(
        source='instructor.get_full_name',
        read_only=True
    )

    class Meta:
        model = Course
        fields = [
            'id', 'title', 'description', 'price',
            'instructor_name', 'rating', 'created_at'
        ]

class LessonSerializer(serializers.ModelSerializer):
    class Meta:
        model = Lesson
        fields = ['id', 'title', 'content', 'video_url', 'order']

# courses/api/views.py
from rest_framework import viewsets, permissions, status
from rest_framework.decorators import action
from rest_framework.response import Response
from ..models import Course, Lesson
from .serializers import CourseSerializer, LessonSerializer

class CourseViewSet(viewsets.ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly]

    def perform_create(self, serializer):
        serializer.save(instructor=self.request.user)

    @action(detail=True, methods=['post'])
    def enroll(self, request, pk=None):
        course = self.get_object()
        user = request.user
        
        if course.students.filter(id=user.id).exists():
            return Response(
                {'error': '您已经报名了这门课程'},
                status=status.HTTP_400_BAD_REQUEST
            )
        
        course.students.add(user)
        return Response({'status': '报名成功'})

    @action(detail=True, methods=['post'])
    def rate(self, request, pk=None):
        course = self.get_object()
        user = request.user
        
        if not course.students.filter(id=user.id).exists():
            return Response(
                {'error': '只有报名的学生才能评分'},
                status=status.HTTP_403_FORBIDDEN
            )
        
        score = request.data.get('score')
        comment = request.data.get('comment', '')
        
        rating, created = CourseRating.objects.update_or_create(
            course=course,
            student=user,
            defaults={'score': score, 'comment': comment}
        )
        
        return Response({'status': '评分成功'})
```

#### 3. 前端实现
```html
<!-- templates/courses/course_list.html -->
{% extends 'base.html' %}

{% block content %}
<div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold mb-8">课程列表</h1>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {% for course in courses %}
        <div class="bg-white rounded-lg shadow-md overflow-hidden">
            <div class="p-6">
                <h2 class="text-xl font-semibold mb-2">
                    <a href="{{ course.get_absolute_url }}"
                       class="text-blue-600 hover:text-blue-800">
                        {{ course.title }}
                    </a>
                </h2>
                <p class="text-gray-600 mb-4">{{ course.description|truncatewords:30 }}</p>
                <div class="flex justify-between items-center">
                    <span class="text-lg font-bold text-green-600">
                        ¥{{ course.price }}
                    </span>
                    <div class="flex items-center">
                        <span class="text-yellow-400 mr-1">★</span>
                        <span class="text-gray-600">{{ course.get_rating|floatformat:1 }}</span>
                    </div>
                </div>
                <div class="mt-4 text-sm text-gray-500">
                    讲师: {{ course.instructor.get_full_name }}
                </div>
            </div>
        </div>
        {% endfor %}
    </div>
    
    {% include 'components/pagination.html' with page_obj=courses %}
</div>
{% endblock %}
```

```javascript
// static/js/courses.js
class CourseAPI {
    static async enrollCourse(courseId) {
        try {
            const response = await fetch(`/api/courses/${courseId}/enroll/`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'X-CSRFToken': getCookie('csrftoken')
                }
            });
            
            if (!response.ok) {
                throw new Error('报名失败');
            }
            
            const data = await response.json();
            return data;
        } catch (error) {
            console.error('报名出错:', error);
            throw error;
        }
    }
    
    static async rateCourse(courseId, score, comment = '') {
        try {
            const response = await fetch(`/api/courses/${courseId}/rate/`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'X-CSRFToken': getCookie('csrftoken')
                },
                body: JSON.stringify({ score, comment })
            });
            
            if (!response.ok) {
                throw new Error('评分失败');
            }
            
            const data = await response.json();
            return data;
        } catch (error) {
            console.error('评分出错:', error);
            throw error;
        }
    }
}

// 事件处理
document.addEventListener('DOMContentLoaded', () => {
    // 报名按钮点击事件
    const enrollButtons = document.querySelectorAll('.enroll-button');
    enrollButtons.forEach(button => {
        button.addEventListener('click', async (e) => {
            e.preventDefault();
            const courseId = button.dataset.courseId;
            
            try {
                await CourseAPI.enrollCourse(courseId);
                showMessage('报名成功！');
                button.disabled = true;
                button.textContent = '已报名';
            } catch (error) {
                showMessage('报名失败：' + error.message, 'error');
            }
        });
    });
    
    // 评分表单提交事件
    const ratingForm = document.querySelector('#rating-form');
    if (ratingForm) {
        ratingForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const courseId = ratingForm.dataset.courseId;
            const score = document.querySelector('#rating-score').value;
            const comment = document.querySelector('#rating-comment').value;
            
            try {
                await CourseAPI.rateCourse(courseId, score, comment);
                showMessage('评分成功！');
                location.reload();
            } catch (error) {
                showMessage('评分失败：' + error.message, 'error');
            }
        });
    }
});
```

```

Follow these instructions to make the following change to my code document.

Instruction: 添加第十章的第三部分（总结和扩展阅读）

Code Edit:
```
### 10.3 总结与扩展阅读

#### 1. 本章总结
本章我们深入探讨了Django的高级特性和实战应用：

1. **高级特性应用**
   - 自定义管理命令：实现了会话清理等维护任务
   - 自定义中间件：开发了请求时间监控和API访问频率限制
   - 自定义模板标签：实现了文章列表和分页组件
   - 自定义表单字段：开发了颜色选择和文件上传验证

2. **实战案例：在线教育平台**
   - 数据模型设计：课程、课时、报名和评分系统
   - API接口设计：RESTful API的最佳实践
   - 前端实现：现代化的UI设计和交互体验

#### 2. 扩展阅读

1. **Django官方文档**
   - [Django高级教程](https://docs.djangoproject.com/en/stable/topics/)
   - [Django最佳实践](https://docs.djangoproject.com/en/stable/misc/design-philosophies/)

2. **Django REST framework文档**
   - [DRF官方教程](https://www.django-rest-framework.org/tutorial/quickstart/)
   - [DRF高级特性](https://www.django-rest-framework.org/api-guide/viewsets/)

3. **相关书籍推荐**
   - 《Two Scoops of Django》：Django最佳实践指南
   - 《Django for Professionals》：Django专业开发指南
   - 《Test-Driven Development with Python》：Python测试驱动开发

4. **在线资源**
   - [Django项目模板](https://github.com/pydanny/cookiecutter-django)
   - [Django设计模式](https://python-patterns.guide/)
   - [Django安全最佳实践](https://docs.djangoproject.com/en/stable/topics/security/)

#### 3. 下一步学习建议

1. **深入学习领域**
   - Django Channels和WebSocket
   - Django与Celery的异步任务
   - Django的缓存策略优化
   - Django的数据库性能调优

2. **实践项目建议**
   - 开发一个完整的CMS系统
   - 构建一个实时聊天应用
   - 实现一个电子商务平台
   - 开发一个社交网络应用

3. **进阶技能提升**
   - Docker容器化部署
   - CI/CD流程集成
   - 微服务架构设计
   - 分布式系统开发

```

Follow these instructions to make the following change to my code document.

Instruction: 添加第十一章（附录：常见问题和实用工具）

Code Edit:
```
{{ ... }}

## 11. 附录：常见问题和实用工具

### 11.1 常见问题解决方案

#### 1. 性能问题
```python
# 1. 数据库查询优化
# 问题：N+1 查询问题
# 错误示例
for article in Article.objects.all():
    print(article.author.username)  # 每次循环都会查询数据库

# 正确示例
articles = Article.objects.select_related('author').all()
for article in articles:
    print(article.author.username)  # 只查询一次数据库

# 2. 内存泄漏
# 问题：大量查询结果占用内存
# 错误示例
big_queryset = HugeModel.objects.all()  # 一次加载所有数据

# 正确示例
from django.db import transaction

@transaction.atomic
def process_huge_data():
    for item in HugeModel.objects.iterator():
        process_item(item)

# 3. 缓存使用
# 问题：频繁访问的数据未缓存
# 正确示例
from django.core.cache import cache

def get_popular_articles():
    cache_key = 'popular_articles'
    result = cache.get(cache_key)
    if result is None:
        result = Article.objects.annotate(
            rating=Avg('ratings__score')
        ).order_by('-rating')[:10]
        cache.set(cache_key, result, 3600)
    return result
```

#### 2. 部署问题
```python
# 1. 静态文件处理
# settings.py
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATICFILES_STORAGE = 'django.contrib.staticfiles.storage.ManifestStaticFilesStorage'

# 2. 媒体文件处理
# settings.py
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'

# urls.py
from django.conf import settings
from django.conf.urls.static import static

if settings.DEBUG:
    urlpatterns += static(
        settings.MEDIA_URL,
        document_root=settings.MEDIA_ROOT
    )

# 3. 环境变量配置
# .env
DEBUG=False
SECRET_KEY=your-secret-key
DATABASE_URL=postgres://user:password@localhost:5432/dbname

# settings.py
import environ

env = environ.Env()
environ.Env.read_env()

DEBUG = env.bool('DEBUG', default=False)
SECRET_KEY = env('SECRET_KEY')
DATABASES = {
    'default': env.db()
}
```

#### 3. 安全问题
```python
# 1. CSRF 保护
# settings.py
MIDDLEWARE = [
    'django.middleware.csrf.CsrfViewMiddleware',
]

# template
{% csrf_token %}

# 2. XSS 防护
# settings.py
TEMPLATES = [{
    'OPTIONS': {
        'autoescape': True,
    },
}]

# 3. SQL 注入防护
# 错误示例
Article.objects.raw("SELECT * FROM articles WHERE title = '%s'" % title)

# 正确示例
from django.db.models import Q
Article.objects.filter(Q(title=title))

# 4. 密码安全
# settings.py
PASSWORD_HASHERS = [
    'django.contrib.auth.hashers.Argon2PasswordHasher',
    'django.contrib.auth.hashers.PBKDF2PasswordHasher',
]

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        'OPTIONS': {'min_length': 12,}
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
]
```

### 11.2 实用工具和扩展

#### 1. 开发工具
```python
# 1. Django Debug Toolbar
INSTALLED_APPS = [
    'debug_toolbar',
]

MIDDLEWARE = [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]

# 2. Django Extensions
INSTALLED_APPS = [
    'django_extensions',
]

# 使用示例
python manage.py shell_plus
python manage.py runserver_plus

# 3. Coverage.py
# .coveragerc
[run]
source = .
omit = 
    */tests/*
    */migrations/*
    */settings/*

# 运行测试覆盖率
coverage run manage.py test
coverage report
coverage html
```

#### 2. 实用装饰器
```python
# 1. 计时装饰器
import time
import functools

def timing_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f'{func.__name__} 执行时间：{end_time - start_time:.2f}秒')
        return result
    return wrapper

# 2. 缓存装饰器
from django.core.cache import cache

def cache_decorator(timeout=300):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            cache_key = f'{func.__name__}:{args}:{kwargs}'
            result = cache.get(cache_key)
            if result is None:
                result = func(*args, **kwargs)
                cache.set(cache_key, result, timeout)
            return result
        return wrapper
    return decorator

# 3. 权限检查装饰器
from django.core.exceptions import PermissionDenied

def permission_required(permission_name):
    def decorator(view_func):
        @functools.wraps(view_func)
        def wrapper(request, *args, **kwargs):
            if not request.user.has_perm(permission_name):
                raise PermissionDenied
            return view_func(request, *args, **kwargs)
        return wrapper
    return decorator
```

#### 3. 常用第三方包
```python
# 1. Django REST framework
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'rest_framework.authtoken',
]

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}

# 2. Celery
# celery.py
from celery import Celery

app = Celery('myproject')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()

# 3. Django Channels
INSTALLED_APPS = [
    'channels',
    # ...
]

ASGI_APPLICATION = 'myproject.asgi.application'
CHANNEL_LAYERS = {
    'default': {
        'BACKEND': 'channels_redis.core.RedisChannelLayer',
        'CONFIG': {
            "hosts": [('127.0.0.1', 6379)],
        }
    }
}
```

### 11.3 项目模板和最佳实践

#### 1. 项目结构
```
myproject/
├── manage.py
├── requirements/
│   ├── base.txt
│   ├── local.txt
│   └── production.txt
├── myproject/
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── local.py
│   │   └── production.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   ├── __init__.py
│   ├── users/
│   ├── articles/
│   └── comments/
├── static/
├── media/
├── templates/
└── docs/
```

#### 2. 配置管理
```python
# settings/base.py
from pathlib import Path
import environ

# 基础设置
BASE_DIR = Path(__file__).resolve().parent.parent
env = environ.Env()

# 读取环境变量
env.read_env(str(BASE_DIR / '.env'))

# 核心设置
SECRET_KEY = env('DJANGO_SECRET_KEY')
DEBUG = env.bool('DJANGO_DEBUG', False)
ALLOWED_HOSTS = env.list('DJANGO_ALLOWED_HOSTS', default=[])

# 数据库设置
DATABASES = {
    'default': env.db('DATABASE_URL')
}

# 缓存设置
CACHES = {
    'default': env.cache('REDIS_URL')
}

# 邮件设置
EMAIL_CONFIG = env.email_url('EMAIL_URL', default='smtp://user:password@localhost:25')
vars().update(EMAIL_CONFIG)
```

#### 3. 部署检查清单
```python
# 部署前检查项
def deployment_checklist():
    """
    部署前检查清单
    1. 安全设置
    - DEBUG = False
    - 设置安全的 SECRET_KEY
    - 配置 ALLOWED_HOSTS
    - 启用 HTTPS
    - 设置安全的会话和 Cookie 设置
    
    2. 性能优化
    - 启用数据库连接池
    - 配置缓存
    - 设置静态文件缓存
    
    3. 监控设置
    - 配置日志
    - 设置错误报告
    - 启用性能监控
    
    4. 备份策略
    - 数据库备份
    - 媒体文件备份
    - 配置文件备份
    """
    pass

# settings.py
SECURE_SSL_REDIRECT = True
SECURE_HSTS_SECONDS = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True
SECURE_CONTENT_TYPE_NOSNIFF = True
SECURE_BROWSER_XSS_FILTER = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
X_FRAME_OPTIONS = 'DENY'
