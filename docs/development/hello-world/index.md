---
title: первое приложение с extremum
description: создайте первое приложение с использованием платформы
---


# Ваше первое приложение с extremum

В данном руководстве мы напишем наше первое приложение с использованием платформы **extremum**

## Подготовка к работе

[Установите](/ru/development/tutorials/setup) необходимое вспомогательное ПО

[Установите](/ru/development/tutorials/cli#установка) интерфейс командной строки **extremum CLI**

## Создание приложения

[Создайте](/ru/development/tutorials/cli#создание-приложения-extremum) новое приложение. Назовите его *pusk.fm*

:::info
Вы можете выбрать другое имя для вашего приложения. В этом случае, при выполнении дальнейших упражнений этого руководства вам следует заменять *pusk.fm* на выбранное вами имя
:::

[Выполните](/ru/development/tutorials/cli#аутентификация-пользователя) аутентификацию в платформе **extremum**

[Инициализируйте](/ru/development/tutorials/cli#инициализация-приложения-на-основе-шаблона) ваше приложение

## Сборка и запуск приложения

Перейдем в каталог *pusk.fm*/ui:

*Linux, MacOS:*

```bash
$ cd pusk.fm/ui
```

*Windows:*

```bash
> cd pusk.fm\ui
```

Установим зависимости:

```bash
$ npm install
```

Теперь мы можем запустить отладочный сервер:

```bash
$ npm run dev
```

В случае успешного запуска вы увидите примерно такой вывод:

```bash
> pusk.fm@0.1.0 dev
> webpack serve

<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] Loopback: http://localhost:8080/
<i> [webpack-dev-server] On Your Network (IPv4): http://192.168.1.49:8080/
<i> [webpack-dev-server] Content not from webpack is served from '/home/t0m/work/extremum/tmp/123/pusk.fm/ui/public' directory
```

Откроем веб-браузер и перейдем по адресу http://localhost:8080/

<!-- ![tutorial-hello-world-1.png](/img/tutorials/tutorial-hello-world-1.png) -->

Нажмем кнопку *Login* и попадем на страницу аутентификации **extremum**:

<!-- ![tutorial-hello-world-2.png](/img/tutorials/tutorial-hello-world-2.png) -->

Укажем имя пользователя и пароль и нажмем кнопку Sign In:

<!-- ![tutorial-hello-world-3.png](/img/tutorials/tutorial-hello-world-3.png) ![](/api/attachments.redirect?id=26770008-9fd0-4e95-bcbb-6ef402b3d118) -->

Наше первое приложение работает!

## Разработка функциональности приложения

Создадим файл *src/components/models/Models.tsx* и поместим в него следующий текст:

```typescript title="src/components/models/Models.tsx"
import React, {useEffect, useState} from 'react';
import {useSDK} from "../../extremum/sdk/hooks/useSDK";
import {EntityModel} from "extremum-sdk/lib/interfaces";

/**
  * Отображение списка моделей данных
  */
const Models = () => {
    const [models,setModels] = useState<EntityModel[]>()

    // Создадим клиент API extremum
    const client = useSDK()


    useEffect(()=>{
        // Получим список моделей
        client.management.storage.models.list().then(
            res => {
                setModels(res)
            }
        ).catch(er =>console.log(er))
    },[])

    // Отобразим имена моделей на странице
    return (
        <div>
            <h2>Hello world!</h2>

            <h4>Example of models from SDK:</h4>
            {
                models?.map( model => (<div>
                    {
                        model.name
                    }
                </div>)
                )
            }
        </div>
    );
};

export default Models;
```

Откроем файл *src/app/routes/AppRouter.tsx* и добавим в нем новый защищенный маршрут *Models*:

```typescript title="src/app/routes/AppRouter.tsx"
const routes = [{
    path: "/",
    element: <ProtectedRoute><Models/></ProtectedRoute>
},{
    path: "/login",
    element:<Login />
}]
```

Обновим страницу в браузере и увидим, что на ней появился список моделей, полученных из API:

<!-- ![tutorial-hello-world-3.png](/img/tutorials/tutorial-hello-world-4.png) -->

## Что дальше?

В этом руководстве мы научились создавать, собирать и запускать приложения на основе платформы **extremum**. Изучите другие наши руководства, чтобы узнать, как

* [работать с данными](/ru/development/tutorials/data-management)
* [отправлять и обрабатывать сигналы](/ru/development/tutorials/signals)
* [разрабатывать серверные функции](/ru/development/tutorials/functions)

## Полезные ссылки

* [Установка необходимого ПО на компьютер пользователя](/ru/development/tutorials/setup)
* [Работа с extremum CLI](/ru/development/tutorials/cli)
* [Клиентские библиотеки](/ru/tools/libraries/about)
