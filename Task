import json
import random
import urllib.request
import urllib.error

def getDataPoint(quote):
    stock = quote['01. symbol']
    bid_price = float(quote['05. price'])  # Use the current price as a substitute for bid
    ask_price = float(quote['05. price'])  # Use the current price as a substitute for ask
    price = (bid_price + ask_price) / 2
    return stock, bid_price, ask_price, price

def getRatio(price_a, price_b):
    """ Get ratio of price_a and price_b """
    if price_b == 0:
        return None
    return price_a / price_b

if __name__ == "__main__":
    # Replace 'YOUR_API_KEY' with your actual Alpha Vantage API key
    API_KEY = 'YOUR_API_KEY'
    SYMBOL_1 = 'IBM'
    SYMBOL_2 = 'AAPL'
    
    QUERY = f"https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol={{}}&apikey={API_KEY}"

    try:
        # Get quote for the first stock
        response_1 = urllib.request.urlopen(QUERY.format(SYMBOL_1))
        data_1 = json.loads(response_1.read())

        # Debug print to check the structure of the JSON response
        print("Response for SYMBOL_1:", data_1)

        # Check if 'Global Quote' is in the response
        if 'Global Quote' in data_1:
            quote_1 = data_1['Global Quote']
        else:
            print(f"Error: 'Global Quote' not found in the response for {SYMBOL_1}")
            quote_1 = None

        # Get quote for the second stock
        response_2 = urllib.request.urlopen(QUERY.format(SYMBOL_2))
        data_2 = json.loads(response_2.read())

        # Debug print to check the structure of the JSON response
        print("Response for SYMBOL_2:", data_2)

        # Check if 'Global Quote' is in the response
        if 'Global Quote' in data_2:
            quote_2 = data_2['Global Quote']
        else:
            print(f"Error: 'Global Quote' not found in the response for {SYMBOL_2}")
            quote_2 = None

        if quote_1 and quote_2:
            # Extract prices
            prices = {}
            stock_1, bid_price_1, ask_price_1, price_1 = getDataPoint(quote_1)
            stock_2, bid_price_2, ask_price_2, price_2 = getDataPoint(quote_2)
            prices[stock_1] = price_1
            prices[stock_2] = price_2

            print(f"Quoted {stock_1} at (bid:{bid_price_1}, ask:{ask_price_1}, price:{price_1})")
            print(f"Quoted {stock_2} at (bid:{bid_price_2}, ask:{ask_price_2}, price:{price_2})")

            # Print the ratio of the two stock prices
            print("Ratio %s" % getRatio(prices[stock_1], prices[stock_2]))

    except urllib.error.HTTPError as e:
        print(f"HTTP error: {e.code} - {e.reason}")
    except urllib.error.URLError as e:
        print(f"Failed to reach server: {e.reason}")
    except json.JSONDecodeError:
        print("Failed to decode JSON from the response")
