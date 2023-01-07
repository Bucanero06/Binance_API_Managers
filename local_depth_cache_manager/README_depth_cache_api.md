# Binance Local Depth Cache

[Description](#description) | [Installation](#installation-and-upgrade) | [Documentation](#documentation) | [Examples](#examples) | [Change Log](#change-log) | [Wiki](#wiki) | [Social](#social) | [Notifications](#receive-notifications) | [Bugs](#how-to-report-bugs-or-suggest-improvements) | [Contributing](#contributing) | [Disclaimer](#disclaimer) | [Commercial Support](#commercial-support)

A local Binance DepthCache Manager for Python that supports multiple depth caches in one instance in a easy, fast,
flexible,
robust and fully-featured way.

### How to start the trailing stop loss engine:

```
import binance_local_depth_cache

depth_cache = binance_local_depth_cache.BinanceLocalDepthCacheManager(exchange="binance.com")
depth_cache.create_depth_cache("BTCUSDT")
```

### Get the [asks] and [bids] depth with:

```
asks = depth_cache.get_asks("BTCUSDT")
bids = depth_cache.get_bids("BTCUSDT")
```

### Catch an exception, if the [depth_cache is out of sync] while accessing its data:

```
try:
    print(f"Top 10 asks: {depth_cache.get_asks(market=market)[:10]}")
    print(f"Top 10 bids: {depth_cache.get_bids(market=market)[:10]}")
except DepthCacheOutOfSync as error_msg:
    print(f"ERROR: {error_msg}")
```

### [Stop and delete a depth_cache]:

```
depth_cache.stop_depth_cache("BTCUSDT")
```

### [Stop the full instance]:

```
depth_cache.stop_manager_with_all_depth_caches()
```

### Get the right logger:

```
logging.getLogger("binance_local_depth_cache")
```

[Discover more possibilities.]

## Description

The Python package Binance Local Depth Cache
provides a local depth_cache for the Binance
Exchanges [Binance](https://github.com/binance-exchange/binance-official-api-docs)
([+Testnet](https://testnet.binance.vision/)),
[Binance Futures](https://binance-docs.github.io/apidocs/futures/en/#websocket-market-streams)
([+Testnet](https://testnet.binancefuture.com)) - more are coming soon.

The algorithm of the depth_cache management was designed according to these instructions:

- [Binance Spot: "How to manage a local order book correctly"](https://developers.binance.com/docs/binance-api/spot-detail/web-socket-streams#how-to-manage-a-local-order-book-correctly)
- [Binance Futures: "How to manage a local order book correctly"](https://binance-docs.github.io/apidocs/futures/en/#diff-book-depth-streams)

By `create_depth_cache()`
the depth_cache is started and initialized, that means for each depth_cache you want to create a separate
thread is started. As soon as at least one depth update is received via websocket, a REST snapshot is downloaded and
the depth updates are applied to it, keeping it in sync in real-time. Once this is done, the state of the cache is set
to "synchronous".

Data in the depth_cache can be accessed
with 'get_asks()'
and 'get_bids()'.
If the state of the depth_cache is not synchronous during access, the exception
'DepthCacheOutOfSync'
is thrown.

The depth_cache will immediately start an automatic re-initialization if a gap in the UpdateID`s is detected (missing
update event) or if the websocket connection is interrupted. As soon as this happens the state of the depth_cache is set
to "out of sync" and when accessing the cache the
exception 'DepthCacheOutOfSync'
is thrown.

### Why a local depth_cache?

A local depth_cache is the fastest way to access the current order book depth at any time while transferring as little
data as necessary. A REST snapshot takes a lot of time and the amount of data that is transferred is relatively large.
Continuous full transmission of the order book via websocket is faster, but the amount of data is huge. A local
depth_cache is initialized once with a REST snapshot and then handles Diff. Depth updates applied by the websocket
connection. By transferring a small amount of data (only the changes), a local depth_cache is kept in sync in real time
and also allows extremely fast (local) access to the data without exceeding
the [Binance request weight limits](https://www.binance.com/en/support/faq/360004492232).

### What are the benefits of the Binance Local Depth Cache?

- Always know if the cache is in sync! If the depth_cache is out of sync, the
  exception 'DepthCacheOutOfSync'
  is thrown or ask
  with `is_depth_cache_synchronized()`.
- If a depth cache is out of sync it gets refreshed automatically within a few seconds.
- 100% Websocket auto-reconnect!
- Supported Exchanges

| Exchange                                                           | Exchange string                                                         | 
|--------------------------------------------------------------------|-------------------------------------------------------------------------| 
| [Binance](https://www.binance.com)                                 | `BinanceLocalDepthCacheManager(exchange="binance.com")`                 |
| [Binance Testnet](https://testnet.binance.vision/)                 | `BinanceLocalDepthCacheManager(exchange="binance.com-testnet")`         |
| [Binance USD-M Futures](https://www.binance.com)                   | `BinanceLocalDepthCacheManager(exchange="binance.com-futures")`         |
| [Binance USD-M Futures Testnet](https://testnet.binancefuture.com) | `BinanceLocalDepthCacheManager(exchange="binance.com-futures-testnet")` |
| More are coming soon                                               | -                                                                       |

- Create multiple depth caches within a single object instance.
- Each depth_cache is processed in a separate thread.
- Start or stop multiple caches with just one command
  `create_depth_cache()` or `stop_depth_cache()`.
- Control websocket out of sync detection
  with `websocket_ping_interval`, `websocket_ping_timeout` and `websocket_close_timeout`
- Powered by Binance REST API and Binance WebSocket API.

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

