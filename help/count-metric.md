# Нормальный минимальный способ без кода

Если у тебя nginx — можно просто считать строки в access.log.

NGINX по умолчанию пишет все заходы в:

```
/var/log/nginx/access.log
```

Посчитать:

```bash
wc -l /var/log/nginx/access.log
```

Посчитать за сегодня:

```bash
grep "$(date '+%d/%b/%Y')" /var/log/nginx/access.log | wc -l
```

Это честный минимализм.

---
