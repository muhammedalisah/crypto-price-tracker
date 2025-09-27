# crypto-price-tracker
README.md
# Crypto Price Tracker
CoinGecko API kullanarak kripto fiyatı çeker.
import sys
import requests

SYMBOL_TO_ID = {
    "BTC":"bitcoin",
    "ETH":"ethereum",
    "ADA":"cardano",
    "DOGE":"dogecoin"
}

def get_price(symbol):
    symbol = symbol.upper()
    coin_id = SYMBOL_TO_ID.get(symbol)
    if not coin_id:
        print("Desteklenmeyen sembol. Örnek: BTC, ETH")
        return
    url = f"https://api.coingecko.com/api/v3/simple/price?ids={coin_id}&vs_currencies=usd"
    r = requests.get(url).json()
    price = r.get(coin_id, {}).get("usd")
    print(f"{symbol} fiyatı: ${price}")

if __name__=="__main__":
    if len(sys.argv) < 2:
        print("Kullanım: python crypto.py BTC")
    else:
        get_price(sys.argv[1])
