# pre "tty" Fy
[Supported Exchanges](#supported-exchanges) | [Installation](#installation-and-upgrade) | [Change Log](#change-log) | [Documentation](#documentation) | 
[Examples](#examples) | [Wiki](#wiki) | [Social](#social) | [Notifications](#receive-notifications) | [Bugs](#how-to-report-bugs-or-suggest-improvements) 
| [Contributing](#contributing) | [Disclaimer](#disclaimer) | [Commercial Support](#commercial-support)

Convert received raw data from crypto exchange API endpoints into well-formed python dictionaries.

```
import binancefy

received_stream_data_json = {"stream": "btcusdt@trade",
                             "data": {"e": "trade",
                                      "E": 1556876873656,
                                      "s": "BTCUSDT",
                                      "t": 117727701,
                                      "p": "5786.76000000",
                                      "q": "0.03200500",
                                      "b": 341831847,
                                      "a": 341831876,
                                      "T": 1556876873648,
                                      "m": True,
                                      "M": True}}

binancefy = binancefy_manager.binancefy()

binancefied_stream_data = binancefy.binance_com_websocket(received_stream_data_json)
print(binancefied_stream_data)
```

Output:

```
{'stream_type': 'btcusdt@trade', 'event_type': 'trade', 'event_time': 1556876873656, 'symbol': 'BTCUSDT',
 'trade_id': 117727701, 'price': '5786.76000000', 'quantity': '0.03200500', 'buyer_order_id': 341831847,
 'seller_order_id': 341831876, 'trade_time': 1556876873648, 'is_market_maker': True, 'ignore': True,
 'binancefied': ['binance', '0.11.1']}
```

This lib is integrated into 
Binance WebSocket API 
and can be activated by setting parameter 
`output_default` of `BinanceWebSocketApiManager()` to `binancefy` 
or for specific streams with the parameter 
`output` of `create_stream()` to `binancefy`.

### Get the right logger:
```
logging.getLogger("binancefy")
```

## Supported Exchanges
### Websockets

| Exchange | Docs            | Status | 
| -------- | --------------- | ------ |
| [Binance](https://www.binance.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_websocket(stream_data_json)` | STABLE |
| [Binance Testnet](https://testnet.binance.vision/) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_websocket(stream_data_json)` | STABLE |
| [Binance Margin](https://www.binance.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | [`binance_com_margin_websocket(stream_data_json)`]() | STABLE |
| [Binance Margin Testnet](https://testnet.binance.vision/) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_margin_websocket(stream_data_json)` | STABLE |
| [Binance Isolated Margin](https://www.binance.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_isolated_margin_websocket(stream_data_json)` | STABLE |
| [Binance Isolated Margin Testnet](https://testnet.binance.vision/) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | [`binance_com_isolated_margin_websocket(stream_data_json)`]() | STABLE |
| [Binance Futures](https://www.binance.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_futures_websocket(stream_data_json)` | STABLE |
| [Binance Futures Testnet](https://testnet.binancefuture.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_futures_websocket(stream_data_json)` | STABLE |
| [Binance Coin Futures](https://www.binance.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_coin_futures_websocket(stream_data_json)` | NEEDS_YOUR_HELP |
| [Binance Coin Futures Testnet](https://testnet.binancefuture.com) ([API](https://github.com/binance-exchange/binance-official-api-docs)) | `binance_com_coin_futures_websocket(stream_data_json)` | NEEDS_YOUR_HELP |
| [Binance Jersey](https://www.binance.je) ([API](https://github.com/binance-jersey/binance-official-api-docs/)) | `binance_je_websocket(stream_data_json)` | STABLE |
| [Binance US](https://www.binance.us) ([API](https://github.com/binance-us/binance-official-api-docs)) | `binance_us_websocket(stream_data_json)` | STABLE |
| [Binance TR](https://www.trbinance.com) ([API](https://www.trbinance.com/apidocs)) | `trbinance_com_websocket(stream_data_json)` | STABLE |
| [Binance JEX](https://www.jex.com) ([API](https://jexapi.github.io/api-doc/spot.html#change-log)) | `jex_com_websocket(stream_data_json)` | STABLE |
| [Binance DEX](https://www.binance.org) ([API](https://docs.binance.org/)) | `binance_org_websocket(stream_data_json)` | NEEDS_YOUR_HELP |
| [Binance DEX Testnet](https://testnet.binance.org) ([API](https://docs.binance.org/)) | `binance_org_websocket(stream_data_json)` | NEEDS_YOUR_HELP |


If you like the project, please 
!star it on 
GitHub! 

## Contributing

Binance Local Depth Cache is
an open
source project which welcomes contributions which can be anything from simple documentation fixes and reporting dead
links to new features. To
contribute follow `CONTRIBUTING.md`.

We love!
open source!

## Disclaimer

This project is for informational purposes only. You should not construe this information or any other material as
legal, tax, investment, financial or other advice. Nothing contained herein constitutes a solicitation, recommendation,
endorsement or offer by us or any third party provider to buy or sell any securities or other financial instruments in
this or any other jurisdiction in which such solicitation or offer would be unlawful under the securities laws of such
jurisdiction.

***If you intend to use real money, use it at your own risk.***

Under no circumstances will we be responsible or liable for any claims, damages, losses, expenses, costs or liabilities
of any kind, including but not limited to direct or indirect damages for loss of profits.

## Commercial Support

***Do you need a developer, operator or consultant?***

Contact [me](https://about.me/oliver-zehentleitner) for a non-binding initial consultation via my company Moonshot
Solutions or via Discord/Telegram.

