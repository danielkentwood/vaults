# algorithmic trading
created:: 2022-10-30 23:17
modified:: <%+ tp.file.last_modified_date() %>
mode:: #mode/management
kind:: #project 
status:: #status/raw
parent::

***
## Project Summary

***
## Rollups
### Subprojects
```dataview
TABLE
FROM #project 
WHERE contains(parent, link(this.file.name))
```

### Task backlog
```dataviewjs

let curr = dv.current();
let curr_nm = curr.file.name;

let proj_pages = dv.pages('#project')
	.where(p => 
		dv.array(p.parent).includes(dv.current().file.link) ||
		p.file.name == curr_nm
	)
	.file.link

let all_tasks = dv.pages().file.tasks
	.where(t => t.project)
	.where(t => proj_pages.includes(t.project)
	)

let done_tasks = all_tasks.where(t => t.completed)
let still_tasks = all_tasks.where(t => !t.completed)
	
dv.header(4, 'Remaining tasks:')	
if (still_tasks.length > 0){
    for (let group of still_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em", "No pending tasks")
}

dv.paragraph('<br><hr>')
dv.header(4, 'Completed tasks:')	
if (done_tasks.length > 0){
    for (let group of done_tasks
		    .groupBy(t => t.project)
		){
			dv.header(5, group.key)
			dv.taskList(group.rows, false)
		}
} else {
	dv.el("em","No completed tasks")
}
```
***
### Meetings
```dataview
table created
from #meeting and #mode/management and #aetna
where contains(parent, link(this.file.name))
sort created asc
```


### Contextual Notes
```dataviewjs
let curr = dv.current()

let pages = dv.pages("#periodic/daily and -#project")
	.where(p => {
		if (p.sendto) {
			let sendto = dv.isArray(p.sendto) ? 
				p.sendto : 
				dv.array(p.sendto);
			if (sendto.some(str => str.includes(curr.file.name))) {
				return true
			}
		}		
	})
	.sort(p => p.file.cday, "asc")

function formatLinks(page) {
	let st_arr = dv.isArray(page.sendto) ?
		page.sendto.filter(str => str.includes(curr.file.name)) :
		dv.array(page.sendto).filter(str => str.includes(curr.file.name));

	let link_arr = st_arr.map(str => {
		return dv.sectionLink(
			page.file.name,
			("sendto:: " + str.replace(/\[\[/g, '').replace(/\]\]/g, '')),
			false,
			str.replace(/\[\[.*?\]\]/g, '')
		)
	});

	return link_arr
}

// set up table
dv.table(
	["File", "Note"], 
	pages
	.map(b => [
		b.file.link,
		formatLinks(b)
	])
)
```

***
## Documentation


List of resources on computational finance (w emphasis on machine learning)
[https://github.com/grananqvist/Awesome-Quant-Machine-Learning-Trading](https://github.com/grananqvist/Awesome-Quant-Machine-Learning-Trading)

## Goals

- Create a system for backtesting strategies. This means you need historical data of the sort that the algorithm works with.
    - Improve the get_historical class so that it can also pull high-resolution order book data. It is important to try and get at least a week's worth of data at this resolution.
        - Here is raw trade data (no order book depth) for a number of exchanges, for free: [http://api.bitcoincharts.com/v1/csv/](http://api.bitcoincharts.com/v1/csv/)
        - Here's another place to get some raw datasets: [https://www.cryptodatasets.com/](https://www.cryptodatasets.com/)
        - Another (free for students): [https://spreadstreet.io/pricing/](https://spreadstreet.io/pricing/)
        - Kraken: [https://support.kraken.com/hc/en-us/articles/218198197-How-to-pull-all-trade-data-using-the-Kraken-REST-API?mobile_site=true](https://support.kraken.com/hc/en-us/articles/218198197-How-to-pull-all-trade-data-using-the-Kraken-REST-API?mobile_site=true)
    - Make it easy to just plug in historical data to any new trading strategy.
        - To get here, you'll have to spend some time learning about how people construct their bots. Learn from the public repositories. Map out the logic in pseudocode first.
            - [https://github.com/enigmampc/catalyst](https://github.com/enigmampc/catalyst)
            - [https://github.com/llens/CryptoCurrencyTrader/blob/master/poloniex_API.py](https://github.com/llens/CryptoCurrencyTrader/blob/master/poloniex_API.py)
            - Bitmex market maker bot
- Parallel with the backtesting system, create a stack of machine learning approaches that you can plug in to any dataset (financial or otherwise)
    - Learn common data formats and structures that people use to feed into their algorithms. The more general you can get, the better.
    - Try them out on a few Kaggle competitions.
- Learn about alpha
    - Start using futures volume as a predictor?
    - alphalens
    - Really start getting active on Quantopian.

Market follower algorithm

1. Identify current price
2. Set up stop-market buy and sell orders (of the same size) on either side of the current price.
3. As soon as one of them is activated, double the size of the opposite order and keep it a few ticks away from the price as it moves. For example, here's a scenario:The tricky part of this is the chop between movements, where the price might hover and flip multiple times before choosing a direction to move in. It will be necessary to make more money on the big movements than you lose from slippage and market taker fees in the chop. Or fine tune the gap between orders to allow for some chop.
    1. Starting price is at $998.
    2. Set stop market buy and sell orders for $100 each at $1000 and $996, respectively.
    3. Suppose the buy order is activated at $1000.
    4. Immediately put in a stop market sell order for $200 at one tick below $1000. If activated, this will cover the original buy order and also short the asset for another $100.
    5. Assuming the sell order hasn't been triggered, make it a trailing stop market sell order, so as the asset price moves up, so does the price of the sell order.
    6. As soon as the price reverses and starts moving down, it should trigger the stop sell order. Now, you're exposed $100 short, hopefully following a downward trend.
4. 
- get a running estimate of the following:
    - volume
    - histogram of length of movement for most recent movements

Another strategy:

Train a neural network to use the order book and the transaction history at various timescales to try and predict short term fluctuations in the price.

First, collect your dataset. Start by simply opening a websocket and logging all of the data into files broken up by 5 minutes (or some other optimal interval).

Then, develop the model offline.

Using only the price and order book history, it might not be possible to reliably predict short term fluctuations. It might be a random walk. Once you have a working model, you can start increasing your alpha.

- Sentiment analysis on twitter and reddit
- Geographical data, figuring out which markets drive crypto prices most efficiently
- Current landscape of price direction for top 10, 50, or 100 coins on Coinmarketcap
    - Would it be possible to train an algorithm that looks at the price direction for each of the top 100 at multiple time scales and produces for each of the top 100 a probability that it will be in the positive movement category

Notes:

- Look at fees at [www.bitmex.com/app/fees](http://www.bitmex.com/app/fees). For perpetual contracts, there is a funding fee. Sometimes, longs will get a rebate and shorts will have to pay. Other times, the opposite. This gets evaluated every 8 hours. Does it happen immediately after purchase of the contract, too? Or if you buy the contract immediately after the 8 hour point, do you get to wait another 8 hours before the funding fee is levied/credited? Could this be used to your advantage in any way?
- Set up a calculator and see how much the price would have to move in a given direction to overcome the BitMex taker fee of 0.075%. Get historical BTC data at the level of each transaction. Track the volatility. When the price changes direction, what is the histogram of price changes before it reverses direction again? How quickly does it tend to move? What is the max and min price acceleration? What is the distribution of price accelerations?
- 

Finance/Algorithmic trading Links

- [https://medium.com/@nitin.v/future-of-machine-learning-in-finance-55878c5c8aff](https://medium.com/@nitin.v/future-of-machine-learning-in-finance-55878c5c8aff)
- [https://www.datacamp.com/community/tutorials/finance-python-trading](https://www.datacamp.com/community/tutorials/finance-python-trading)
- [https://github.com/llens/CryptoCurrencyTrader/blob/master/poloniex_API.py](https://github.com/llens/CryptoCurrencyTrader/blob/master/poloniex_API.py)
- Enigma's catalyst engine: [https://github.com/enigmampc/catalyst](https://github.com/enigmampc/catalyst)
- [https://www.quantinsti.com/blog/webinar-artificial-intelligence-algorithmic-trading-strategies/](https://www.quantinsti.com/blog/webinar-artificial-intelligence-algorithmic-trading-strategies/)
- [https://www.quantinsti.com/blog/free-resources-learn-machine-learning-trading/](https://www.quantinsti.com/blog/free-resources-learn-machine-learning-trading/)
- [https://www.quantinsti.com/blog/artificial-neural-network-python-using-keras-predicting-stock-price-movement/](https://www.quantinsti.com/blog/artificial-neural-network-python-using-keras-predicting-stock-price-movement/)
- [https://www.quantinsti.com/blog/machine-learning-logistic-regression-python/](https://www.quantinsti.com/blog/machine-learning-logistic-regression-python/)
- [https://www.quantopian.com/tutorials](https://www.quantopian.com/tutorials)
- An example of a good blog with great analysis of crypto markets: [http://aurie.me/bitcoin-trading-pivotal-decision-points/](http://aurie.me/bitcoin-trading-pivotal-decision-points/)
-
