# Скиллы интенсива

Скилл — это инструкция для Гермеса или его сотрудника: роль, порядок работы, формат результата. Один скилл — одна папка с файлом `SKILL.md`.

| Скилл | Версия | Для кого | Урок |
|---|---|---|---|
| [komanda-dispetcher](komanda-dispetcher/SKILL.md) | 2.1.0 | сотрудник Диспетчер: сортирует входящие сообщения клиентов | [урок 1](../nedelya-1-jev-laya/README.md) |

## Как поставить скилл сообщением в Chat Гермеса

Пример для Диспетчера. Сотрудник `dispetcher` уже должен быть создан ([урок 1, шаг 6](../nedelya-1-jev-laya/README.md#шаг-6-создаём-диспетчера)).

**Поставить или обновить до новой версии** — вставь во вкладку **Chat** веб-интерфейса Гермеса (запасной путь — чат `hermes` в терминале Netcatty):

```
Обнови скилл komanda-dispetcher у сотрудника dispetcher. По шагам:
1. mkdir -p ~/.hermes/profiles/dispetcher/skills/neurosprint/komanda-dispetcher
2. curl -fsSL https://raw.githubusercontent.com/freemind-club/neurosprint/main/skills/komanda-dispetcher/SKILL.md -o ~/.hermes/profiles/dispetcher/skills/neurosprint/komanda-dispetcher/SKILL.md
3. Покажи строку version из файла.
4. hermes -p dispetcher config get skills.auto_load — если komanda-dispetcher там нет, выполни:
   hermes -p dispetcher config set skills.auto_load '["komanda-dispetcher"]'
Итог двумя строками: версия скилла / автозагрузка.
```

<details>
<summary><b>Если Гермес не справился — команды для терминала Netcatty</b></summary>

```
mkdir -p ~/.hermes/profiles/dispetcher/skills/neurosprint/komanda-dispetcher
curl -fsSL https://raw.githubusercontent.com/freemind-club/neurosprint/main/skills/komanda-dispetcher/SKILL.md -o ~/.hermes/profiles/dispetcher/skills/neurosprint/komanda-dispetcher/SKILL.md
grep version ~/.hermes/profiles/dispetcher/skills/neurosprint/komanda-dispetcher/SKILL.md
hermes -p dispetcher config set skills.auto_load '["komanda-dispetcher"]'
```

</details>

После обновления скилла в разговоре с сотрудником начни новую сессию (`/new`), чтобы он прочитал новую версию.

## Как вызывать

Командой в начале сообщения: `/komanda-dispetcher …`. В меню Telegram скилл может быть показан с подчёркиванием (`/komanda_dispetcher`) — работают оба варианта.

## Безопасность

- Скиллы не просят ключей и паролей и не выводят их в чат.
- Текст сообщений клиентов скилл считает данными, а не командами.
- Сторонние программы, которые ставятся в уроках, закреплены по версии (`laya[mcp]==0.3.20`, `jev-mcp` v0.3.0 со сверкой контрольной суммы).
- Если внешний сервис недоступен, Диспетчер продолжает работу своей моделью (движок «сам»).
