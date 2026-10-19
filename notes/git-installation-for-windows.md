ЗАМЕТКА — УСТАНОВКА И ПРОВЕРКА GIT FOR WINDOWS
Дата: 2026-10-19
Тема: установка Git, диагностика PATH и подготовка PowerShell
Статус: Git установлен и запускается по полному пути; добавление в PATH выполнено, но после перезапуска PowerShell ещё не проверено.

1. ЗАЧЕМ МЫ ЭТО ДЕЛАЛИ

На Windows был установлен Microsoft VS Code, но команда git не распознавалась в PowerShell. Git нужен отдельно от VS Code:
- VS Code — редактор кода.
- Git — система контроля версий и инструмент для клонирования репозиториев, просмотра истории изменений и сравнения правок.
- GitHub — сайт, на котором размещаются удалённые репозитории.

Решили установить Git for Windows, чтобы в дальнейшем работать с репозиториями через PowerShell и встроенный терминал VS Code.

2. ИСХОДНОЕ СОСТОЯНИЕ

PowerShell был открыт в:
C:\WINDOWS\system32

Команда:
$HOME

Результат:
C:\Users\Syste

Проверка Git:
where.exe git

Результат:
ИНФОРМАЦИЯ: не удается найти файлы по заданным шаблонам.

Проверка VS Code:
where.exe code

Результат:
C:\Users\Syste\AppData\Local\Programs\Microsoft VS Code\bin\code
C:\Users\Syste\AppData\Local\Programs\Microsoft VS Code\bin\code.cmd

Вывод: VS Code доступен из PowerShell, а Git по имени не находился.

3. СКАЧИВАНИЕ И УСТАНОВКА

Официальная страница:
https://git-scm.com/install/windows

Выбран обычный установщик Git for Windows для x64:
Git-2.56.0.2-64-bit.exe

Страница релиза:
https://github.com/git-for-windows/git/releases/tag/v2.56.0.windows.2

При выборе PATH в установщике рекомендован вариант:
“Git from the command line and also from 3rd-party software”.

4. ДИАГНОСТИКА ПОСЛЕ УСТАНОВКИ

Команда:
Test-Path "C:\Program Files\Git\cmd\git.exe"

Результат:
True

Команда:
Test-Path "$env:LOCALAPPDATA\Programs\Git\cmd\git.exe"

Результат:
False

Это показало, что Git находится в стандартном каталоге Program Files, а не в каталоге LocalAppData.

Проверка запуска по полному пути:
& "C:\Program Files\Git\cmd\git.exe" --version

Результат:
git version 2.56.0.windows.2

Вывод: Git установлен и работает. Проблема была в том, что PowerShell не находил его по команде git через PATH.

5. ДОБАВЛЕНИЕ GIT В PATH ПОЛЬЗОВАТЕЛЯ

Выполнены команды:

$userPath = [Environment]::GetEnvironmentVariable("Path", "User")
$gitPath = "C:\Program Files\Git\cmd"

if (($userPath -split ";") -notcontains $gitPath) {
    [Environment]::SetEnvironmentVariable(
        "Path",
        (($userPath.TrimEnd(";") + ";" + $gitPath).TrimStart(";")),
        "User"
    )
}

Команда завершилась без видимого сообщения об ошибке.

Важно: после этого ещё не проверяли, что команда git работает в новом окне PowerShell. Изменение пользовательского PATH требует открыть новый процесс терминала, чтобы он получил обновлённое значение окружения.

6. СЛЕДУЮЩИЙ ШАГ

Когда вернусь к компьютеру:

1. Закрыть текущее окно PowerShell и открыть новое.
2. Выполнить:
   git --version

Ожидаемый результат — строка вида:
git version 2.56.0.windows.2

3. Если команда всё ещё не находится, проверить:
   where.exe git
   $env:Path -split ";"

4. Не переустанавливать Git без необходимости: запуск по полному пути уже подтвердил, что установленный файл работает.

7. ЧТО ПОКА НЕ ДЕЛАЛИ

- Не клонировали репозитории в рамках этой сессии.
- Не изменяли и не удаляли существующий проект.
- Не настраивали GitHub-аккаунт, SSH-ключи или учётные данные.
- Не проверяли Git в новом PowerShell после изменения PATH.

8. КОРОТКИЙ ИТОГ

Git for Windows 2.56.0.windows.2 установлен в:
C:\Program Files\Git

VS Code уже установлен и доступен командой code.

Git успешно запускается так:
& "C:\Program Files\Git\cmd\git.exe" --version

Путь C:\Program Files\Git\cmd добавлен в пользовательский PATH, но результат нужно подтвердить в новом PowerShell с помощью git --version.

Конец заметки.
