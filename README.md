# backtest


This is a demonstration of the OOP backtesting system that runs well on the mid-frequency strategy feeding with Open-High-Low-Close daily prices from a CSV file. While the main structure was adopted from Successful Algorithmic Trading, I fixed fatals bug and changed the outline to adapt to the objective of sensitivity analysis on long-short strategy with different hodlding periods. The system pulls the result that was extremely similar to the one by Zipline. 

Data.py - Data handler that pushes slice of stock prices as bars. The current bar is the price of the "current" date in backtest, while multiple bars(n) return the last n trading days of prices. HistoricalCSVHandler is the derived class of the Handler class, and it can read prices from CSV files. To make the program avaiable for live-trading, just derive a new data-handler class that feeds the live data.

Event.py - Describe different event types, such as market event (bars from data handler class from Data.py), signal event (controlled by strategy.py, pushed when bars, or prices, meet the signal requirement), order event (generated after the receival of the signal event and requirement checking. It simulated as the way of submitting the limited or market order to the market), and filled event (order event getting filled).

Execution.py - Put events into priority queue and it would be managed in the Portfolio.py.

Portfolio.py - Initiate a portfolio and manage how the event affects the portfolio accounts.

Backtest.py - Update the initialzied portfolio through the method of the portfolio and manage the event queue.

Strategy.py - Transform the bars to signal event. Every strategy has different strategy file. 
