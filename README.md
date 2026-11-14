# Vibes TCG Connector

🌐 [English](README_EN.md)

Лёгкий обходчик блокировок DPI для карточной игры **Vibes TCG**. Одна кнопка: включил — играешь. Лобби, магазин, ивенты и карточки — грузятся сразу и без задержек.

**Автор:** [🌐 mixas.pro](https://mixas.pro) · [✈️ Telegram: mixaseth.t.me](https://mixaseth.t.me)

> Хотите так же смотреть YouTube, сидеть в Discord и на других сайтах без VPN?
> Используйте бесплатно полную версию [Zapret2](https://github.com/MixasV/zapret2-gui/tree/fix/graceful-exit-and-bridge-cooldowns)

⭐ **Пользуетесь программой — поставьте звёздочку репозиторию!** Это бесплатная поддержка и лучший способ сказать «спасибо».

## Как это работает

Внутри — движок [winws](https://github.com/bol-van/zapret) (zapret) + драйвер WinDivert. Программа запускает его с одной фиксированной стратегией, настроенной под серверы Vibes TCG:

- **QUIC и TCP-десинк** для доменов игры (`vibes.game`, лобби, API, ресурсы)
- **Десинк по IP-подсетям** игровых серверов и CloudFront CDN (их трафик не всегда содержит имя домена, поэтому по IP)
- **UDP any-protocol** на игровых портах — покрывает игровой протокол

Списки лежат в `bin/lists/` — правятся любым текстовым редактором.

## Быстрый старт

1. Скачайте релиз (или соберите сами — ниже)
2. Запустите `Запустить.bat` — он попросит права администратора (нужны для WinDivert)
3. Нажмите «Подключиться» — лобби и магазин игры загрузятся

Закрытие окна полностью завершает программу — никаких фоновых процессов и автозапуска. Если обход когда-нибудь «залипнет» после закрытия — запустите `Остановить_обход.bat`, он гарантированно всё остановит.

## Сборка из исходников

Нужны: [Node.js](https://nodejs.org), [Rust](https://rustup.rs), Visual Studio Build Tools.

```powershell
npm install
npm run build
cargo build --release
```

Готовый exe: `src-tauri\target\release\vibes-connector.exe`. Запускайте `Запустить.bat` из корня — он сам найдёт бинарник и движок в `bin\`.

## Структура

```
vibes/
  bin/                  движок (winws.exe, WinDivert) и списки доменов
    lists/              списки доменов и IP-подсетей
  src/                  интерфейс (React)
  src-tauri/            бэкенд (Rust)
  Запустить.bat         запуск с правами администратора
  Остановить_обход.bat  аварийная остановка обхода
```

## Дисклеймер

Неофициальная утилита. **Не связана с разработчиками Vibes TCG.** Программа не модифицирует игру — только обрабатывает сетевые пакеты. Используйте на свой страх и риск.

## Сторонние компоненты

| Компонент | Проект | Лицензия |
|---|---|---|
| `bin/winws.exe` | [zapret](https://github.com/bol-van/zapret) | [MIT](https://raw.githubusercontent.com/bol-van/zapret/master/docs/LICENSE.txt) |
| `bin/WinDivert.dll`, `bin/WinDivert64.sys` | [WinDivert](https://reqrypt.org/windivert.html) © basil | LGPL v3 / GPL v2 (на выбор) |
| `bin/cygwin1.dll` | [Cygwin](https://cygwin.com/) | LGPL v3 |
