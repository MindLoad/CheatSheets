---
Title: Python
Date: 2024-08-07 17:24
tags:
  - cheatsheet
  - python
---
> [!example]- @singledispatchmethod with @classmethod
> ```python
> def _register(self, cls, method=None):
 >   if hasattr(cls, "__func__"):
 >       setattr(cls, "__annotations__", cls.__func__.__annotations__)
 >   return self.dispatcher.register(cls, func=method)
> singledispatchmethod.register = _register
>```

