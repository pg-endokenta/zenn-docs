---
title: "DjangoにCeleryを用いた非同期処理を追加する"
emoji: "🗂"
type: "tech"
topics: []
published: false
---

Djangoを使用している際，「重めの処理を行いたいいけどレスポンスはすぐに返したい」という場合があります．
その希望を叶える解決策の1つとして「Celery」を用いた実装が挙げられます．

## Celeryとは

野菜のセロリと同じスペルです．
Pythonにおいて非同期処理を簡単に実装できるパッケージです．
公式ドキュメント

PyPI

Celeryを使用するにあたりmessage brokerを用意する必要があります．
今回はCeleryのドキュメントの一番最初に記載されているRabbitMQを使用します．

django/configフォルダ内にcelery.pyを作成し，中身は以下のように記述します

```python
import os

from celery import Celery

# Set the default Django settings module for the 'celery' program.
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')

app = Celery('practice')

# Using a string here means the worker doesn't have to serialize
# the configuration object to child processes.
# - namespace='CELERY' means all celery-related configuration keys
#   should have a `CELERY_` prefix.
app.config_from_object('django.conf:settings', namespace='CELERY')

# Djangoの各アプリからtasks.pyを探す
app.autodiscover_tasks()


@app.task(bind=True, ignore_result=True)
def debug_task(self):
    print(f'Request: {self.request!r}')
```
