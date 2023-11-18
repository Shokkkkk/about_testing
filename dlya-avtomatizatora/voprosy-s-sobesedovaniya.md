# Вопросы с собеседования

чем отличаются \
`assert status_code == 200`\
`assert status_code is 200`

и

`assert status_code == 400`\
`assert status_code is 400`



почему не стоит делать вот так:

```
def get_user(name, params={}):
```

поотому что появляется неявное изменение кода при сборке



зачем нужны @pytest.fixture(scope=session) ? vs хуки



docker logs - как включить? \
не стоит использовать, потому что могут стырить инфу из логов
