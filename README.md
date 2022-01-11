# Sample Weather Application

Djangoで非常に簡単な天気情報を取得するアプリの開発方法を以下に示す。

# ファイルのディレクトリ

```
C:.
│  db.sqlite3
│  manage.py
│  README.md
│  
├─backend
│  │  asgi.py
│  │  settings.py
│  │  urls.py
│  │  wsgi.py
│  │  __init__.py
│  │
│  └─__pycache__
│          settings.cpython-310.pyc
│          urls.cpython-310.pyc
│          wsgi.cpython-310.pyc
│          __init__.cpython-310.pyc
│
├─templates
│      index.html
│
└─weather
    │  admin.py
    │  apps.py
    │  models.py
    │  tests.py
    │  urls.py
    │  views.py
    │  __init__.py
    │
    ├─migrations
    │  │  __init__.py
    │  │
    │  └─__pycache__
    │          __init__.cpython-310.pyc
    │
    └─__pycache__
            admin.cpython-310.pyc
            apps.cpython-310.pyc
            models.cpython-310.pyc
            urls.cpython-310.pyc
            views.cpython-310.pyc
            __init__.cpython-310.pyc
```

# 初期設定

まずは、以下のコマンドで必要なパッケージをインストールする。

```
pip install django
django-admin startproject backend .
django-admin startapp weather
```

# データベース作成

コマンドを入力したら、以下のコマンドを入力してデータベースを作成する。

```
py manage.py migrate
```

データベースを作り終えたら、以下のコマンドを入力して管理サイトにログインするための管理者を作成する。

```
py manage.py createsuperuser
```

これでユーザ名とメールアドレス、パスワードを入力して管理者を作成する。

# アプリの作成

`backend/settings.py`にアクセス。

```py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'weather', #追加
]

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'], #追加
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

プロジェクト側のルーティングを設定するために、`backend/urls.py`にアクセスして以下のプログラムを書く。

```py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('weather.urls')),
]
```

# テンプレートの表示

`templates/index.html`を新しく作成して、以下のプログラムを書く。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>What's the weather like?</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.6.2/css/bulma.css" />
</head>

<body>
    <section class="hero is-primary">
        <div class="hero-body">
            <div class="container">
                <h1 class="title">
                    What's the weather like?
                </h1>
            </div>
        </div>
    </section>
    <section class="section">
        <div class="container">
            <div class="columns">
                <div class="column is-offset-4 is-4">
                    <form method="POST">
                        <div class="field has-addons">
                            <div class="control is-expanded">
                                <input class="input" type="text" placeholder="City Name">
                            </div>
                            <div class="control">
                                <button class="button is-info">
                                    Add City
                                </button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </section>
    <section class="section">
        <div class="container">
            <div class="columns">
                <div class="column is-offset-4 is-4">
                    <div class="box">
                        <article class="media">
                            <div class="media-left">
                                <figure class="image is-50x50">
                                    <img src="http://openweathermap.org/img/w/10d.png" alt="Image">
                                </figure>
                            </div>
                            <div class="media-content">
                                <div class="content">
                                    <p>
                                        <span class="title">Las Vegas</span>
                                        <br>
                                        <span class="subtitle">29° F</span>
                                        <br> thunderstorm with heavy rain
                                    </p>
                                </div>
                            </div>
                        </article>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <footer class="footer">
    </footer>
</body>

</html>
```

最後に`weather/views.py`にアクセスして以下のプログラムを書く。

```py
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

これで基本的な動作は終了。


# 開発環境

* Visual Studio Code
* Python
* Django
* Bulma CSS