# AMM simulation + visualization

I found AMM math not very intuitive for the non-academic user. I created a [spreadsheet](https://docs.google.com/spreadsheets/d/1iUrOd6Hwv7HTPKvif7isTQ5KoepZ-nGo-U2MuurslJE/) to simulate what happens to the pool when you swap assets or add liquidity. Cells are adjustable, so you can play around with numbers to see their impact on the pool; this helped me develop intuition on what's happening in the pools.

---
### Sushiswap

Sushiswap (equivalent to Uniswap v2) is the first example. It uses the "constant product" formula to price a trade; in English, "the product of the quantities of X and Y remains constant when a trade is made." When you swap X for Y, the price you get isn't the exact ratio of X:Y you see in the pool (e.g. if there is 1 ETH and 3000 DAI in a pool, you don't get 1 ETH for 3000 DAI). 

You always get an inferior price, because price slips down (or up, depending on your perspective) along a curve. The curve is defined by the function Y = k / X (or, k = X * Y, i.e. constant product). See the curve chart in the spreadsheet for reference. 

When you add liquidity, however, "constant product" doesn't apply. The whole curve shift outwards, so the k in k = X * Y changes.

---

### Balancer

On the second tab, we look at Balancer. Balancer is known for using "constant weighted-product." In English, "the product of the quantities of X and Y, each weighted by a pre-determined exponent (power), remains constant when a trade is made." k = (quantity of A ^ chosen weight of A) * (quantity of B ^ chosen weight of B).

Another distinction between Sushiswap and Balancer (in their current forms) is the value of each token in a pool. In Sushiswap (or Uniswap v2), each token comprises 50% of the value fo the pool (and if it doesn't, it represents a price arbitrage opportunity and arbitrageurs will bring it in line with external market prices until the pool halves are equal again). This is equivalent in function to the weight of each token being 0.5. 

In Balancer, the weights can be anywhere between 0 and 100%, as long as the weight of both tokens add up to 100%. Each token comprises a different % of value in the pool (not 50% each). This results in a curve of assets (~ a pricing curve) that is shaped differently than in Sushiswap.

The different shape of curves results in different levels of slippage and tendency for "impermanent loss" (which is really just unrealized loss, in tradfi terms).

---

Sample:
![simulator](/../main/Ignore/2022-01_AMMmath.png)

[Google spreadsheet here](https://docs.google.com/spreadsheets/d/1iUrOd6Hwv7HTPKvif7isTQ5KoepZ-nGo-U2MuurslJE/)

***Feedback, suggestions and requests welcome. Leave a comment or DM at Twitter @88crypt.***

---

Sources:
* https://arxiv.org/abs/2103.12732
* This by the Balancer Simulations team was really good: [Understanding Balancer Pools](https://medium.com/balancer-simulations/understanding-balancer-pools-c2b877dcc082)
* Other papers and articles
