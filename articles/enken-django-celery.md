---
title: "DjangoにCeleryで非同期処理を導入しよう！サンプルコードあり"
emoji: "🦉"
type: "tech"
topics: [django, celery]
published: true
---

Djangoを使用している際，「重めの処理を行いたいけどレスポンスはすぐに返したい」という場合があります．
その希望を叶える解決策の1つとして「Celery」を用いた実装が挙げられます．
この記事では簡単な動作サンプルを用いて，そのコードの説明を行います．

## 想定読者

想定読者は以下の用な方です．

- Djangoの基本的な知識がある方
- Celeryを使ったことがない方
- Dockerについての基本的な知識がある方

## Celeryとは

野菜のセロリと同じスペルです．
Pythonにおいて非同期処理を簡単に実装できるパッケージです．

- [公式ドキュメント](https://docs.celeryq.dev/en/stable/)
- [PyPI](https://pypi.org/project/celery/)

## Broker

Celeryを使用するにあたりmessage brokerを用意する必要があります．

Celeryを用いた非同期処理をざっくり説明すると

1. タスクが呼ばれる
1. そのタスクをbrokerに送信
1. workerがbrokerからタスクを取得し実行

のような流れになります．

今回はBrokerとして，Celeryのドキュメントの[一番最初に記載](https://docs.celeryq.dev/en/main/getting-started/first-steps-with-celery.html#rabbitmq)されている[RabbitMQ](https://www.rabbitmq.com/)を使用します．

## サンプルリポジトリ

簡単な動作サンプルは以下のリポジトリにあります．

- [サンプルリポジトリ](https://github.com/pg-endokenta/django_celery_sample)

Docker環境で動かすことを想定しており，
READMEに簡単な説明を記載しています．

## コードの説明

ここからは上記の[サンプルリポジトリ](https://github.com/pg-endokenta/django_celery_sample)のコードを元に，簡単な説明を行います．

### Djangoのコンテナ

celeryとdjangoがインストールされたpythonの動く環境を用意します．

#### プロジェクト構成

はじめにDjangoのプロジェクトについてです．
djangoのプロジェクトの構成は以下であるとします．

```text
- sample_project/
  - manage.py
  - config/
    - __init__.py
    - settings.py
    - urls.py
```

#### Celeryインスタンスの生成を行う

configフォルダ内にcelery.pyを作成し，以下のように記述します．

```python
import os
from django.conf import settings
from celery import Celery

# Djangoの設定モジュールを環境変数として指定
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')

app = Celery('sample')

# Djangoの設定ファイルの中で、CELERY_で始まる設定をCELERY用として読み込む
app.config_from_object('django.conf:settings', namespace='CELERY')

# Djangoの各アプリからタスクを自動的に読み込む
app.autodiscover_tasks()
```

#### Celeryが読み込まれるようにする

上で定義したCeleryのappがDjangoのスタート時にロードされるように，`sample_project/config/__init__.py`に以下の記述を追加します．

```python
from .celery import app as celery_app

__all__ = ('celery_app',)
```

#### 関数の定義

Celeryで処理したい関数の定義についてです．
ここでは，AIのコメントを取得するために，時間のかかるAPIを叩いたような処理を行う関数を定義します．
`sample_project/memos/tasks.py`に以下のように記述します．

```python
from celery import shared_task
from .models import Memo, AIComment
from time import sleep
from datetime import datetime

@shared_task
def create_ai_comment(memo_id):
    memo = Memo.objects.get(id=memo_id)

    # AI のコメントを生成する処理
    start_time = datetime.now().strftime("%H:%M:%S")
    sleep(3)
    end_time = datetime.now().strftime("%H:%M:%S")
    ai_comment = f"AI がコメントしました！ 処理は {start_time} <--> {end_time} 間に行われました。"
    
    # AI のコメントを保存する処理
    AIComment.objects.create(memo=memo, content=ai_comment)
    return
```

#### 呼び出し側のサンプル

呼び出す側を`sample_project/memos/views.py`のクラスに実装します．

```python
class MemoCreateView(CreateView):
    model = Memo
    fields = ['content']
    success_url = reverse_lazy('memos:memo-list')

    def form_valid(self, form):
        response = super().form_valid(form)
        create_ai_comment.delay_on_commit(self.object.id)
        return response
```

関数名に`.deley_on_commit()`をつけることで，

- オープントランザクションがある場合
  - そのトランザクションがコミットされた後にCeleryのタスクを実行
- オープントランザクションがない場合
  - その場でCeleryのタスクを実行

という動作を実現します．
これはDjangoの[`on_commit()`](https://docs.djangoproject.com/en/5.1/topics/db/transactions/#django.db.transaction.on_commit)を利用しています．

#### settings.pyの設定

最後にDjangoのsettingsにCeleryの設定を追加します．

```python
RABBITMQ_DEFAULT_USER = os.getenv('RABBITMQ_DEFAULT_USER')
RABBITMQ_DEFAULT_PASS = os.getenv('RABBITMQ_DEFAULT_PASS')
CELERY_BROKER_URL = f'amqp://{RABBITMQ_DEFAULT_USER}:{RABBITMQ_DEFAULT_PASS}@rabbitmq:5672//'
```

重要なのは`CELERY_BROKER_URL`です．これがBrokerとの接続に使用されます．

- amqp: brokerとの通信プロトコル
- ユーザー名: rabbitmqのユーザー名
- パスワード: rabbitmqのパスワード
- rabbitmq: brokerのホスト名, 今回はDocker Composeのサービス名
- ポート: brokerのポート番号

となっています．

### RabbitMQのコンテナ

#### ユーザーとパスワードの設定

環境変数に

- RABBITMQ_DEFAULT_USER
- RABBITMQ_DEFAULT_PASS
  
を設定することでデフォルトのユーザーを定義することができます．
この値はDjangoのsettings.pyでも使用しています．

### workerのコンテナ

Djangoのコンテナと中身は同じです．
このコンテナではDjangoを起動するのではなく，Celeryのworkerを起動しています．

## おわり

以上でCeleryを用いた非同期処理のサンプルコードの説明を終わります．

## 参考

- [First Steps with Celery](https://docs.celeryq.dev/en/main/getting-started/first-steps-with-celery.html#first-steps)
- [First steps with Django](https://docs.celeryq.dev/en/main/django/first-steps-with-django.html)
