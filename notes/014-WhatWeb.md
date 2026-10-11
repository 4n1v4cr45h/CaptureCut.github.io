---
title: WhatWeb
id: 014
---

WhatWeb Notes

Что такое

WhatWeb — инструмент для fingerprinting веб-сайтов.
Используется для первичной веб-разведки и определения применяемых технологий.

Основные команды

whatweb https://site.com

whatweb -v https://site.com

whatweb -a 3 https://site.com

whatweb -l

whatweb -I wordpress

whatweb --log-json=result.json https://site.com

Практика

1. example.com

Результат:
- Cloudflare
- HTML5
- GET/HEAD
- CDN-заголовки

Вывод:
Сайт находится за Cloudflare. Технологический стек практически скрыт.

2. github.com

Результат:
- Собственная инфраструктура GitHub
- Cookies (_gh_sess, _octo, logged_in)
- CSP
- HSTS
- X-Frame-Options
- OpenSearch

Вывод:
WhatWeb обнаружил признаки масштабной веб-платформы и заголовки безопасности.

3. wikipedia.org

Результат:
- Apache Traffic Server 9.2.15
- ATS/9.2.15
- MediaWiki (вероятно)
- Wikimedia cookies
- HSTS
- OpenGraph

Вывод:
Удалось определить используемый прокси-сервер и CMS без доступа к исходному коду сайта.

Что умеет определять

- Web Server
- CDN
- CMS
- Frameworks
- Security Headers
- Cookies
- OpenGraph
- JavaScript Libraries
- Metadata

Примеры технологий

- Apache
- Nginx
- Apache Traffic Server
- Cloudflare
- WordPress
- Drupal
- MediaWiki
- Django
- Rails
- ASP.NET

Полезность

- Первичная разведка
- Инвентаризация веб-ресурсов
- Bug Bounty
- OSINT
- Подготовка к дальнейшему анализу
- Автоматизация веб-сканирования

Ограничения

- Не ищет уязвимости
- Не выполняет эксплуатацию
- Точность зависит от сигнатур
- Многие технологии могут быть скрыты CDN или прокси

Связка с другими инструментами

WhatWeb -> Nmap
WhatWeb -> FFUF
WhatWeb -> Nuclei
WhatWeb -> Nikto
WhatWeb -> Ручной анализ

Главный вывод

Даже один HTTP-запрос позволяет собрать значительное количество информации о веб-сайте. WhatWeb полезен как первый этап исследования перед более глубоким анализом инфраструктуры и приложений.
