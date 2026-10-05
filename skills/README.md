# Скиллы интенсива

Скилл — это инструкция для Гермеса или его сотрудника: роль, порядок работы, формат результата. Один скилл — одна папка с файлом `SKILL.md`.

| Скилл | Версия | Для кого | Урок |
|---|---|---|---|
| [komanda-dispetcher](komanda-dispetcher/SKILL.md) | 2.1.0 | сотрудник Диспетчер: сортирует входящие сообщения клиентов | [урок 1](../nedelya-1-jev-laya/README.md) |
| [otvety-na-otzyvy](otvety-na-otzyvy/SKILL.md) | 1.0.0 | твой основной Гермес (без сотрудника): черновик ответа на отзыв клиента | [урок 2](../nedelya-2-skilly/README.md) |
| [skill-stroitel](skill-stroitel/SKILL.md) | 1.0.0 | твой основной Гермес: интервью → поиск готового скилла → установка/донастройка или сборка с нуля | [бонус к уроку 2](../nedelya-2-skilly/БОНУС_skill-stroitel.md) |

## Скилл «Ответы на отзывы» — как его делают на уроке 2

На уроке участники **не скачивают** этот файл — они просят Гермеса создать такой скилл обычной фразой в чате (см. [урок 2](../nedelya-2-skilly/README.md#живой-пример-ответы-на-отзывы-клиентов)), без терминала и путей. Файл в этой папке — эталон для сверки: на него ссылается бонус-блок урока «Для любопытных» и заметки ведущего, если результат у кого-то выйдет не похож на ожидания.

Технический путь ниже (скачать и поставить готовый файл напрямую) — альтернатива для тех, кто уже освоился с терминалом, не основной путь урока.

<details>
<summary><b>Технический путь: поставить готовый файл напрямую (не основной путь урока)</b></summary>

Этот скилл ставится самому Гермесу, не сотруднику — поэтому путь без `-p <профиль>`.

**Сообщение в Chat:**

```
Поставь мне скилл «Ответы на отзывы». По шагам, после каждого коротко доложи.
1. mkdir -p ~/.hermes/skills/neurosprint/otvety-na-otzyvy
2. curl -fsSL https://raw.githubusercontent.com/freemind-club/neurosprint/main/skills/otvety-na-otzyvy/SKILL.md -o ~/.hermes/skills/neurosprint/otvety-na-otzyvy/SKILL.md
3. Покажи строку version из файла.
4. hermes skills list | grep otzyv — скилл должен быть в списке.
5. Итог одной строкой: скачано / версия / виден в списке.
```

<details>
<summary><b>Если Гермес не справился — команды для терминала Netcatty</b></summary>

```
mkdir -p ~/.hermes/skills/neurosprint/otvety-na-otzyvy
curl -fsSL https://raw.githubusercontent.com/freemind-club/neurosprint/main/skills/otvety-na-otzyvy/SKILL.md -o ~/.hermes/skills/neurosprint/otvety-na-otzyvy/SKILL.md
grep version ~/.hermes/skills/neurosprint/otvety-na-otzyvy/SKILL.md
hermes skills list | grep otzyv
```

</details>

</details>

## Как поставить скилл сообщением в Chat Гермеса (сотруднику)

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
