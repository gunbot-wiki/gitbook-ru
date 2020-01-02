---
description: Информация о запуске Gunbot в режиме Headless mode – «беспилотный режим».
---

# Headless mode – «Беспилотный режим»

{% hint style="info" %}
Эта статья предназначена для опытных пользователей, которые хотят запускать Gunbot без использования графического интерфейса. 

Это не полный обзор всех доступных настроек, а лишь краткий обзор того, как вручную работать с файлом конфигурации. Обратитесь к другим частям wiki для ознакомления с подробным описанием настроек.
{% endhint %}

## Описание файла Config

Все настройки Gunbot определены в одном файле с именем `config.js`. Здесь вы добавляете свои ключи API, добавляете торговые пары и определяете свои стратегии.

Вы можете обратиться к прилагаемому файлу `config-js-example.txt` за примером файла конфигурации с правильно определенными парами и всеми необходимыми параметрами для добавления каждого обмена. В wiki вы найдете подробное описание каждого параметра, доступного в файле конфигурации.

Когда файл конфигурации будет перезаписан во время работы Gunbot, измененные настройки будут загружены автоматически.

Убедитесь, что никакие параметры не удаляются при настройке. Убедитесь, что JSON-форматирование не повреждено. Если вы не уверены в своем конфигурационном файле, вы можете проверить его на [https://jsonlint.com](https://jsonlint.com) \(или аналогичном валидаторе JSON\).

Действия, которые требуют использования графического интерфейса:

* Обновление мастер-ключей
* Обновление адреса GUNTHY кошелька
* Передача лицензии на программное обеспечение третьей стороне

## Отключение графического интерфейса

Чтобы полностью отключить графический интерфейс, необходимо внести следующее изменение в разделе GUI файла `config.js`:

```text
"GUI": {
        "enabled": false,
```

## Connecting exchanges

To connect an exchange, add the relevant settings to the exchange section of `config.js`.

It looks like this:

```text
"binance": {
            "masterkey": "registered_api_key",
            "mastersecret": "secret_for_registered_api_key",
            "key": "trading_api_key",
            "secret": "secret_for_trading_api_key",
            "delay": 1,
            "type": "binance"
        },
```

Note that you can use a different API key for trading than the registered key. If you don't use a secondary key, you can just enter the registered key in the `key` parameter.

## Strategies

A strategy is defined by giving it a unique name and adding it to the `strategies` section of the config file. This strategy can then be assigned to one or more trading pairs.

It looks like this:

```text
"custom-strategy": {
            "BUY_METHOD": "tssl",
            "BUY_ENABLED": true,
            "SELL_METHOD": "tssl",
            "SELL_ENABLED": true,
            "BUY_LEVEL": 1,
            "GAIN": 0.5,

(many lines cut out to keep this page clean)

            "SL_DISABLE_BUY": false,
            "COUNT_SELL": 9999,
            "TRADES_TIMEOUT": 0
        },
```

## Defining pairs and overrides

In the `pairs` section of the config file you can add one or more pairs inside a block specifying the exchange the pairs will run on.

Each pair must be assigned an existing strategy, it must be specified if the pair is enabled or not.

```text
"Binance": {
            "BTC-LTC": {
                "strategy": "SMACROSS",
                "enabled": true,
                "override": {
                    "TRADING_LIMIT": 1000
                }
            }
        },
```

The override section allows for pair specific modifications to the assigned strategy. Any strategy parameter can be used as an override.

In the example above the pair will run the SMACROSS strategy, with a `TRADING_LIMIT` different from what is defined in the strategy itself.

