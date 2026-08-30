# 🫀 Go Heart Bot

Библиотека для упрощённого создания Telegram-ботов на языке Go.
Проект ориентирован на **простоту, надежность и удобство расширения**.

> [!NOTE]
> 
> ![Go Version](https://img.shields.io/badge/go-1.18%2B-blue.svg)
> ![License](https://img.shields.io/badge/license-GNU%20AGPLv3-red.svg)
> ![status: dev](https://img.shields.io/badge/status-dev-orange)
> ![CI](https://img.shields.io/badge/CI-GitHub%20Actions-green)
> ![CI](https://github.com/my-app-s/go-heart-bot/actions/workflows/deploy.yml/badge.svg)
![Latest Tag](https://img.shields.io/github/v/tag/my-app-s/go-heart-bot)

## 📦 Что это

`go-heart-bot` — это каркас для разработки Telegram-ботов:

- Упрощает настройку и запуск бота
- Содержит готовые модули для работы с Telegram API (`heart/accessbot.go`, `corebot.go`, `degugbot.go`, `infobot.go`, `updatebot.go`)
- Легко расширяемый и тестируемый

## ⚙️ Пример `.env`

```env
TOKEN_API=your_bot_token
ACCESS_CODE=12345
ALLOWED_USER_ID=987654321
STATUS_DEBUG=true
STATUS_CHECK_ACCESS=false
TZ=UTC
```

## 💻 Пример использования

```go
package main

import (
    "github.com/my-app-s/go-heart-bot/heart"
)

func main() {
    bot := heart.NewCoreBot()
    
    bot.Start()
}
```

> Здесь `NewCoreBot` — функция для инициализации бота. Другие модули (`AccessBot`, `DebugBot`, `InfoBot`, `UpdateBot`) можно подключать по необходимости.

## 🧪 Тестирование

```bash
go test ./...
```

- Запускает все тесты внутри пакета `heart`
- Использует стандартный `testing` пакет Go

## Disclaimer & License

* **Short Disclaimer (EN)**: Materials are provided ***as is*** under the LICENSE file. No warranties. Authors are not liable for damages. No partnership or obligations created.
* **Short Disclaimer (RU)**: Материалы предоставляются ***как есть*** и регулируются файлом LICENSE. Гарантий нет. Автор(ы) не несут ответственности за убытки. Партнёрство или обязательства не создаются.
* **Full Disclaimer**: Read the full text in the [DISCLAIMER](./DISCLAIMER.md) (Available in EN/RU).
* **License**: This project is dual-licensed:
  * **Open Source**: Licensed under the [GNU AGPLv3](./LICENSE).
  * **Commercial**: A separate proprietary commercial license is required for proprietary, closed-source, or enterprise use that does not comply with AGPLv3 terms. Contact the copyright holder for commercial licensing.

## Author & Contacts

* **GitHub**: [@my-app-s](https://github.com/my-app-s)
* **LinkedIn**: [In/my-app-s](https://www.linkedin.com/in/my-app-s)
* **Mail**: [myapps.mre.dev@gmail.com](mailto:myapps.mre.dev@gmail.com)
