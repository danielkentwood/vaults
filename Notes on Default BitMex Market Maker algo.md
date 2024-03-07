# Notes on Default BitMex Market Maker algo

links:: [[π develop interface with exchange APIs]]

The highest level file that executes the strategy is **market_maker.py**

This file has two classes:

- ExchangeInterface
- OrderManager

It also has a few helper functions at the end of the file.

**ExchangeInterface**

This class is a set of functions for interacting with the exchange. Here are the definitions:

- __init__:
- cancel_order:
- cancel_all_orders:
- get_portfolio:
- calc_delta:
- get_delta:
- get_instrument:
- get_margin:
- get_orders:
- get_highest_buy:
- get_lowest_sell:
- get_position:
- get_ticker:
- is_open:
- check_market_open:
- check_if_orderbook_empty:
- amend_bulk_orders:
- create_bulk_orders:
- cancel_bulk_orders:

**OrderManager**

This class of functions manages orders. Here are the definitions:

- __init__:
- reset:
- print_status:
- get_ticker:
- get_price_offset:
- place_orders:
- prepare_order:
- converge_orders:
- short_position_limit_exceeded:
- long_position_limit_exceeded:
- sanity_check:
- check_file_change:
    - self.restart() if any files we're watching have changed. We use getmtime() which checks a list of files for the most recent change. List of files is defined in market_maker.settings
- check_connection:
- exit:
- run_loop:
- restart:

---

---

The next file we need to understand is **bitmex.py**

This file contains just one class: BitMEX.

**BitMEX**

This is a set of functions for interacting with the BitMEX website. It is an API connector.

- __init__:
- __del__:
- exit:
- ticker_data:
- instrument:
- instruments:
- market_depth:
- recent_trades:
- authentication_required:
    - wrapped:
    - funds:
    - position:
    - isolate_margin:
    - delta:
    - buy:
    - sell:
    - place_order:
    - amend_bulk_orders:
    - create_bulk_orders:
    - open_orders:
    - http_open_orders:
    - cancel:
    - withdraw:
- _curl_bitmex: this finally sends a request to bitmex servers. Lots of detail here, so I'll go more into it below.
    - exit_or_throw
    - retry: