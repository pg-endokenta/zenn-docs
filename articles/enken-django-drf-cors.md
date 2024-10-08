---
title: "Django REST frameworkでCORSの設定を行う方法"
emoji: "👻"
type: "tech"
topics:
  - "django"
  - "cors"
  - "drf"
published: true
published_at: "2024-09-28 02:46"
---

## CORSを簡単に説明

CORSを簡単に説明すると，「どこからならアクセスしても良いか」を設定するものです．

## 今回使用するもの

django-cors-headerというパッケージを使用します．
このパッケージはDRFの[公式ドキュメントでも言及](https://www.django-rest-framework.org/topics/ajax-csrf-cors/)されているものです．

- [PyPIのリンク](https://pypi.org/project/django-cors-headers/)
- [GitHubのリポジトリ](https://github.com/adamchainz/django-cors-headers)

## Djangoへ導入する

### 1. django-cors-headerをインストール

```bash
python -m pip install django-cors-headers
```

でdjango-cors-headerをインストールします

### 2. Djangoのsettings.pyのINSTALLED_APPSに追記

```py
INSTALLED_APPS = [
    ...,
    "corsheaders",
    ...,
]
```

### 3. Djangoのsettings.pyのMIDDLEWAREに追記

```py
MIDDLEWARE = [
    ...,
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.common.CommonMiddleware",
    ...,
]
```

ミドルウェアとして記載する位置はできるだけ上の方が良いです．
レスポンスの生成に関わるものより上に記載することで，効果を発揮できます．
例えば，

- DjangoのCommonMiddleware
- WhitenoiseのWhiteNoiseMiddleware

より上に書く必要があります．

### 4. Djangoのsettings.pyにCORS_ALLOWED_ORIGINSを追加

```py
CORS_ALLOWED_ORIGINS = [
    "https://example.com",
    "https://sub.example.com",
    "http://localhost:8080",
    "http://127.0.0.1:9000",
]
```

ここに追加されたオリジンからの接続は許可されます．

### その他

その他にも

- REGEXで許可のリスト作成する
- 特定のURLに対してのみ許可する

ということができます．
詳しくは[GitHubのREADME](https://github.com/adamchainz/django-cors-headers/blob/main/README.rst)に記載されています

## 参考

[DRFのcorsについてのページ](https://www.django-rest-framework.org/topics/ajax-csrf-cors/)
[django-cors-headerのGitHub](https://github.com/adamchainz/django-cors-headers)
