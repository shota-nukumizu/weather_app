# Sample Weather Application

Djangoで非常に簡単な天気情報を取得するアプリの開発方法を以下に示す。

# 初期設定

まずは、以下のコマンドで必要なパッケージをインストールする。

```
pip install django
django-admin startproject backend .
django-admin startapp weather
```

コマンドを入力したら、以下のコマンドを入力してデータベースを作成する。

```
py manage.py migrate
```


# 開発環境

* Visual Studio Code
* Python
* Django
* Bulma CSS