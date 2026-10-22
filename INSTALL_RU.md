# RTK для Claude Code – короткая инструкция

RTK сокращает вывод команд терминала, который читает Claude Code: вместо сотен строк `git status` или логов тестов он получает короткую выжимку. Ответы остаются теми же, а лимит токенов расходуется медленнее.

Установка занимает пару минут. Ниже два способа – выберите один.

## Способ 1: попросить Claude Code

Откройте Claude Code и вставьте этот текст целиком:

```
Установи RTK (https://github.com/rtk-ai/rtk) на этот компьютер и подключи его к Claude Code:
1. Установи: на macOS – brew install rtk, на Windows – winget install rtk-ai.rtk.
   Если brew не установлен, используй
   curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
   и добавь ~/.local/bin в PATH.
2. Проверь, что работают обе команды: rtk --version и rtk gain.
   Если rtk --version работает, а rtk gain – нет, установился другой пакет с тем же именем:
   удали его и поставь правильный (cargo install --git https://github.com/rtk-ai/rtk).
3. Выполни rtk init -g и подтверди изменения.
4. Проверь установку командой rtk init --show и скажи мне, что Claude Code нужно перезапустить.
```

Когда Claude Code закончит, закройте его и откройте снова.

## Способ 2: вручную в терминале

macOS:

```bash
brew install rtk
rtk --version
rtk gain
rtk init -g
```

Windows (PowerShell или Windows Terminal, не двойным щелчком по файлу):

```powershell
winget install rtk-ai.rtk
rtk --version
rtk gain
rtk init -g
```

После `rtk init -g` перезапустите Claude Code.

## Как понять, что всё работает

- `rtk init --show` – показывает, что хук подключён к Claude Code.
- `rtk gain` – показывает, сколько токенов уже сэкономлено. Сразу после установки там нули, это нормально.
- Попросите Claude Code выполнить `git status` в любом проекте: в выводе инструмента будет видно, что команда прошла через `rtk`.

## Частые проблемы

| Что видно | Что делать |
|---|---|
| `rtk: command not found` | Терминал не видит программу. Откройте новое окно терминала; если не помогло – добавьте `~/.local/bin` в PATH (для установки через curl). |
| `rtk --version` работает, `rtk gain` – нет | Установлен чужой пакет с тем же именем. `cargo uninstall rtk`, затем `cargo install --git https://github.com/rtk-ai/rtk`. |
| Claude Code не сокращает вывод | Claude Code не перезапущен после `rtk init -g`. Закройте и откройте его. |
| Чтение файлов не сокращается | Так и задумано: RTK работает только с командами терминала, встроенные инструменты Claude Code (чтение и поиск файлов) он не трогает. |

## Как удалить

```bash
rtk init -g --uninstall   # отключить от Claude Code
brew uninstall rtk        # macOS; на Windows – winget uninstall rtk-ai.rtk
```

После удаления перезапустите Claude Code.

Подробная английская инструкция – [INSTALL.md](INSTALL.md).
