# Automation-of-cryptocurrency-trading
Automation of cryptocurrency trading

import ccxt
import time

exchange = ccxt.binance({
    'apiKey': 'YOUR_API_KEY',
    'secret': 'YOUR_SECRET_KEY',
})

def buy(symbol, amount):
    try:
        order = exchange.create_market_buy_order(symbol, amount)
        print(f'Покупка выполнена: {order["id"]}')
    except Exception as e:
        print(f'Ошибка при покупке: {e}')

def sell(symbol, amount):
    try:
        order = exchange.create_market_sell_order(symbol, amount)
        print(f'Продажа выполнена: {order["id"]}')
    except Exception as e:
        print(f'Ошибка при продаже: {e}')

def check_price_and_trade(symbol, target_price, amount):
    ticker = exchange.fetch_ticker(symbol)
    current_price = ticker['last']
    if current_price >= target_price:
        buy(symbol, amount)
    elif current_price <= target_price / 2:
        sell(symbol, amount)

if __name__ == '__main__':
    symbol = 'BTC/USDT'
    target_price = 40000
    amount = 0.001
    while True:
        check_price_and_trade(symbol, target_price, amount)
        time.sleep(60)  # Проверять цену каждую минуту
```
