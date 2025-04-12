# Telegram Bot
Middleware для обработки flow с fsm для `tucnak/telebot`.

Работа со стейтами в примере сделана через `looplab/fsm`. Но можно использовать другое решение, т.к. декларация и специфическая работа с fsm вынесена из `Flow` в `handler`-ы 

## Установка
```bash
go get github.com/ulngollm/middleware
```

## Features
1. Сохранение стейта между сообщениями
2. Просто и понятно добавлять обработчики для стейтов

## Как использовать

```go
package main

import (
	"github.com/ulngollm/fsm-chat-bot/internal/flow"
	"github.com/ulngollm/fsm-chat-bot/internal/middleware"
)

func run() {
	pool := flow.NewPool()
	flowManager := flow.New(pool)
	router := middleware.NewFlowRouter(flowManager)

	g := router.Group("default") // flow name
	g.AddHandler("opened", handle)
	g.AddHandler("waiting", handle)
	g.AddHandler("closed", handle)
}

func handle(c tele.Context) error {
    return c.Send(middleware.GetCurrentFlow(c))
}

```


## Модификации
Как добавить другой storage для flow...

## todo
1. format as library
2. use interfaces for flow handling
3. simplify initialization
