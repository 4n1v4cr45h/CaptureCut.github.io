KALI LINUX — УСТАНОВКА GDB
Дата: 2026-10-19
Статус: УСПЕШНО

ЦЕЛЬ
Установить GDB в Kali Linux для дальнейшего изучения ELF-файлов и реверс-инжиниринга.

ИСХОДНАЯ ПРОБЛЕМА
Команда sudo apt install gdb не завершила установку из-за недоступности отдельных зеркал Kali.

Ошибки:
- mirror.keiminem.com — Connection timed out при загрузке libipt2.
- mirror.hashy0917.net — Connection failed при загрузке libpython3.14.

Большая часть пакетов загрузилась, но APT сообщил:
Error: Unable to fetch some archives.

ПРОВЕРКА ИСТОЧНИКОВ APT
Проверен каталог:
  /etc/apt/sources.list.d/

Файл debian.sources отсутствовал.
В каталоге обнаружен файл:
  kali.sources

Команда:
  grep -RhsE '^(Types|URIs|Suites|Components):' /etc/apt/sources.list.d/

Результат:
  Types: deb
  URIs: http://http.kali.org/kali/
  Suites: kali-rolling
  Components: main contrib non-free non-free-firmware

Проверка HTTP-доступа к официальному адресу:
  curl -I --connect-timeout 10 http://http.kali.org/kali/

Результат: HTTP/1.1 200 OK.

РЕШЕНИЕ
Повторена установка с увеличенным количеством попыток и тайм-аутом:

  sudo apt-get \
    -o Acquire::Retries=5 \
    -o Acquire::http::Timeout=30 \
    -o Acquire::https::Timeout=30 \
    install gdb

При повторной попытке APT получил недостающие пакеты с других зеркал:
- libipt2 — kali.download
- libpython3.14 — ftp.yz.yamagata-u.ac.jp

Установка завершилась успешно. Установлены GDB и необходимые зависимости; обновлены libdw1t64, libelf1t64 и python3.14-tk.

ПРОВЕРКА
Команда:
  gdb --version

Результат:
  GNU gdb (Debian 18.1-3) 18.1

ИТОГ
GDB установлен и запускается.
Первоначальная проблема была связана с недоступностью отдельных зеркал при загрузке пакетов. Повторная установка с Acquire::Retries=5 и тайм-аутом 30 секунд позволила APT скачать недостающие зависимости с других зеркал.

СЛЕДУЮЩИЙ ВОЗМОЖНЫЙ ШАГ
Продолжить локальную практику реверс-инжиниринга ELF-файла с помощью file, strings, objdump и GDB.
