# python-www

Inspired by proxy-www

```py
from typing import Callable
import requests


class WWW:
    def __init__(self, name: str = "http://www"):
        self.name = name

    def __repr__(self):
        return repr(self.name)

    def get(self, *args: Callable):
        res = requests.get(self.name)
        for f in args:
            f(res)

    def __getattr__(self, name):
        return WWW(f"{self.name}.{name}")


www = WWW()
www.example.com.get(
    lambda x: print(x.status_code),
    lambda x: print(x.headers["content-type"]),
)
```

Just for fun😉
