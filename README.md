# 🫀 Go Heart Bot

Библиотека для упрощённого создания Telegram-ботов на языке Go.
Проект ориентирован на **простоту, надежность и удобство расширения**.

![Go Version](https://img.shields.io/badge/Go-1.18%2B-blue.svg)
![License](https://img.shields.io/badge/License-GNU%20AGPLv3-red.svg)
![Status](https://img.shields.io/badge/Status-Dev-orange)
![Latest Tag](https://img.shields.io/github/v/tag/my-app-s/go-api-ping)

> Status Github Actions
> 
> ![Status GitHub Pages](https://github.com/my-app-s/go-api-ping/actions/workflows/deploy-pages.yml/badge.svg)

## 📦 Что это

`go-heart-bot` — это каркас для разработки Telegram-ботов:

- Упрощает настройку и запуск бота

## ⚙️ Пример `.env`

> [!IMPORTANT]
> Убедитесь, что .gitignore на уровне проекта полностью блокирует отправку `.env` файла в Git.

```env
TOKEN_API=your_bot_token
ACCESS_CODE=access_code
```

## 💻 Пример использования

```go
package main

import (
	"log"

	"your_project/heart" // Замените на ваш путь к проекту

	tgbotapi "github.com/go-telegram-bot-api/telegram-bot-api/v5"
)

func main() {
	// 1. Загружаем настройки доступа из env
	authConfig := heart.LoadAuthConfig()

	// 2. Инициализируем бота и получаем канал обновлений
	bot, updates := heart.GetHeartBot()

	log.Println("[INFO] Bot is up and running...")

	// 3. Основной цикл обработки входящих сообщений
	for update := range updates {
		// Пропускаем всё, что не является текстовым сообщением
		if update.Message == nil {
			continue
		}

		chatID := update.Message.Chat.ID
		text := update.Message.Text

		// 4. Проверка доступа (если пароль неверный или не введен — функция сама 
		// отправит запрос и вернет false, прерывая обработку этого сообщения)
		if !authConfig.CheckUserAccess(bot, text, chatID) {
			continue
		}

		// 5. Дальше работают только авторизованные пользователи
		if update.Message.IsCommand() {
			switch update.Message.Command() {
			case "start":
				bot.Send(tgbotapi.NewMessage(chatID, "Привет! Бот готов к работе. 🚀"))
			case "about":
				heart.AboutMessage(bot, chatID)
			default:
				bot.Send(tgbotapi.NewMessage(chatID, "Неизвестная команда."))
			}
		} else {
			// Обычный текст от авторизованного пользователя
			bot.Send(tgbotapi.NewMessage(chatID, "Получено: "+text))
		}
	}
}
```

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
