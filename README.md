<br />

<p align="center">
  <img src="https://github.com/juspay/hyperswitch/raw/main/docs/imgs/hyperswitch-logo-dark.svg#gh-dark-mode-only" alt="Hyperswitch-Logo" width="40%" />
</p>

[![Discord Shield](https://img.shields.io/discord/831165782750789672)](https://discord.com/invite/xPHTuHCmuV)
[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/OpenBB-finance/OpenBB)
<a href="https://codespaces.new/OpenBB-finance/OpenBB">
  <img src="https://github.com/codespaces/badge.svg" height="20" />
</a>
<a target="_blank" href="https://colab.research.google.com/github/OpenBB-finance/OpenBB/blob/develop/examples/googleColab.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>
[![PyPI](https://img.shields.io/pypi/v/openbb?color=blue&label=PyPI%20Package)](https://pypi.org/project/openbb/)


## Why HyperSwitch Plugins?
HyperSwitch Plugins let you **build once, use anywhere** across backtests, paper trading, and live markets.

<p align="center">
  <img src="https://raw.githubusercontent.com/juspay/hyperswitch/main/docs/gifs/quickstart.gif" alt="Quickstart demo" />
</p>

They are:
- 🔌 Modular & reusable components
- 📦 Environment-agnostic (backtest, sandbox, live)
- 🧩 Easy to plug into any strategy or workflow
- 🌐 Exchange-agnostic with unified interfaces

Create, share, or combine plugins for indicators, strategies, risk controls, and more — all while keeping your code clean and scalable.

<summary><h2> What Can I Do with Hyperswitch?</h2></summary>

Hyperswitch offers a modular, open-source payments infrastructure designed for flexibility and control. Apart from our Payment Suite offering, this solution allows businesses to pick and integrate only the modules they need on top of their existing payment stack — without unnecessary complexity or vendor lock-in.

Each module is independent and purpose-built to optimize different aspects of payment processing.

<h3> Learn More About The Payment Modules </h3>
<details>

- **Cost Observability**  
  Advanced observability tools to audit, monitor, and optimize your payment costs. Detect hidden fees, downgrades, and penalties with self-serve dashboards and actionable insights.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/ai-powered-cost-observability)_

- **Revenue Recovery**  
  Combat passive churn with intelligent retry strategies tuned by card bin, region, method, and more. Offers fine-grained control over retry algorithms, penalty budgets, and recovery transparency.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/revenue-recovery)_

- **Vault**  
  A PCI-compliant vault service to store cards, tokens, wallets, and bank credentials. Provides a unified, secure, and reusable store of customer-linked payment methods.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/vault)_

- **Intelligent Routing**  
  Route each transaction to the PSP with the highest predicted auth rate. Reduce retries, avoid downtime, and minimize latency while maximizing first attempt success.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/intelligent-routing)_

- **Reconciliation**  
  Automate 2-way and 3-way reconciliation with backdated support, staggered scheduling, and customizable outputs. Reduces manual ops effort and increases audit confidence.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/reconciliation)_

- **Alternate Payment Methods**  
  Drop-in widgets for PayPal, Apple Pay, Google Pay, Samsung Pay, Pay by Bank, and BNPL providers like Klarna. Maximizes conversions with seamless one-click checkout.  
  _[Read more](https://docs.hyperswitch.io/about-hyperswitch/payments-modules/enable-alternate-payment-method-widgets)_

</details>
### Trade Stocks, Crypto, Futures, and Forex

```python
from HyperSwitch import Alpaca, CoinbasePro

stocks = Alpaca()
crypto = CoinbasePro()
futures = BinanceFutures()

# Easily perform the same actions across exchanges & asset types
stocks.interface.market_order('AAPL', 'buy', 1)
crypto.interface.market_order('BTC-USD', 'buy', 1)
# Full futures feature set
futures.interface.get_hedge_mode()
```

### Backtest your trades, events, websockets, and custom data

```python
import HyperSwitch
"""
This example shows how backtest over tweets
"""

class TwitterBot(HyperSwitch.Model):
    def main(self, args):
        while self.has_data:
            self.backtester.value_account()
            self.sleep('1h')

    def event(self, type_: str, data: str):
        # Now check if it's a tweet about Tesla
        if 'tsla' in data.lower() or 'gme' in data.lower():
            # Buy, sell or evaluate your portfolio
            pass


if __name__ == "__main__":
    exchange = HyperSwitch.Alpaca()
    model = TwitterBot(exchange)

    # Add the tweets json here
    model.backtester.add_custom_events(HyperSwitch.data.JsonEventReader('./tweets.json'))
    # Now add some underlying prices at 1 month
    model.backtester.add_prices('TSLA', '1h', start_date='3/20/22', stop_date='4/15/22')

    # Backtest or run live
    print(model.backtest(args=None, initial_values={'USD': 10000}))

```

![image](https://github.com/user-attachments/assets/fb77fc15-02d1-4669-8e74-c973619238c1)
![image](https://github.com/user-attachments/assets/214fb653-bae0-4c93-8cb6-4ac9ce74a647)



## 🛠️ Installation

Follow the steps below to install and run this project on your local machine.

### 1. 📦 Prerequisites

Make sure you have the following tools installed on your system:

- [Node.js](https://nodejs.org/)  (v14.x or newer)
- [npm](https://www.npmjs.com/)  (comes with Node.js)
- [Git](https://git-scm.com/) 
- Python 3.x (optional, if any indicators or tools require it)

> You can also use Docker to run the project in an isolated environment.

### 3. 📦 Install Dependencies

Install the required npm packages:

```bash
npm install
```

If the plugin uses Python-based tools or indicators, install the Python dependencies as well:

```bash
pip install -r requirements.txt
```

---

### 4. 🔐 Set Up Exchange API Keys

To allow the plugin to interact with cryptocurrency exchanges, set up your API credentials.

Create a `.env` file in the root directory and add your exchange keys:

```env
EXCHANGE_API_KEY=your_api_key_here
EXCHANGE_SECRET_KEY=your_secret_key_here
```

> Make sure not to commit this file to version control. It should remain private.

---

### 5. ⚙️ Configure the Plugin

Each plugin comes with a configuration file. For example:

```yaml
# config/rsi-config.yaml
strategy:
  rsi_period: 14
  overbought_threshold: 70
  oversold_threshold: 30
  symbol: BTC/USDT
  interval: "1h"
```

You can modify these values based on your trading preferences.

---

### 6. ▶️ Run the Plugin

Once everything is set up, start the plugin:

```bash
npm start -- --plugin rsi --config config/rsi-config.yaml
```

Or, if you're using a custom script:

```bash
node index.js --plugin rsi --config config/rsi-config.yaml
```

---

### 7. 🐳 Optional: Run with Docker

Build and run the plugin using Docker:

```bash
docker build -t HyperSwitch-rsi-plugin .
docker run -it --env-file .env HyperSwitch-rsi-plugin
```

```mermaid
erDiagram
    PLUGIN {
        string id
        string name
        string type
    }

    PLUGIN ||--o{ STRATEGY : implements
    STRATEGY ||--o{ INDICATOR : uses
    STRATEGY ||--o{ EXECUTOR : runs
    EXECUTOR ||--o{ MARKET_INTERFACE : interacts
    MARKET_INTERFACE }|--o{ EXCHANGE : connects
    PLUGIN ||--o{ CONFIGURATION : requires
    PLUGIN ||--o{ LOGGING : logs
```



<p align="center">
    <img src="https://minkxx-spotify-readme.vercel.app/api?theme=dark&rainbow=true&scan=true&spin=True" alt="Preview">
</p>

<p align="center">
  <img src="https://github.com/tarikmanoar/tarikmanoar/raw/output/github-snake-dark.svg" alt="snake"></center>
</p>

## Contributors

 wouldn't be  without you. If we are going to disrupt financial industry, every contribution counts. Thank you for being part of this journey.

<a href="https://github.com/OpenBB-finance/OpenBB/graphs/contributors">
   <img src="https://contributors-img.web.app/image?repo=OpenBB-finance/OpenBB" width="800"/>
</a>
