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

    def __getattr__(self, name):
        if name == "com":
            return get(f"{self.name}.com")
        else:
            return WWW(f"{self.name}.{name}")


class get:
    def __init__(self, web: str):
        self.web = web
        self.res = requests.get(web)

    def get(self, func: Callable):
        print(func(self.res))


www = WWW()
www.example.com.get(lambda x: x.status_code)
```

Just for fun😉
