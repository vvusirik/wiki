= Wing Vol Model =

== Background ==
* Predict `target_sd_vol` for a given (underlying, target_sd) using parameters (`atm_vol`, `atm_slope`, `bdays`)
* Use some parameter transforms (sqrt(bdays), ln(atm_vol))
* Use ratio of target_sd_vol to atm_vol since vol is hard to predict. (`ln(target_sd_vol / atm_vol)`) 

== Hedging ==
* Delta hedge to remove exposure to underlying
* Vega hedge against atm_vol to expose us to only the spread between `target_sd_vol` and `atm_vol`
    * # of ATM options for atm_vega hedge = atm_vega(target_sd) / atm_vega(atm_sd)
* Slega

== MPT ==
Cost of variance

Suppose we have a trade opportunity that is ~ N(mu, sd)
And k = the size we choose for this opportunity
utility = ev - cost_of_variance * variance
so u = k * mu - c * (k * sd)^2
To find the optimal k, we take derivative of both sides and set it = 0
dU / dk = mu - 2 * c * k * sd^2 = 0
Suppose I currently have a 500k portfolio. I want to make 250k this year with a 3 sharpe (so I want my annual sd = 250k / 3)
So if I had an investment opportunity with mu = 250k, sd = 83k, then I would want my utility calibration to suggest me size = 1
So I plug in 250k for mu, 83k for sd, 1 for k, and I solve for c
And that gave me roughly c = 18e-6
So as our portfolio grows, we'd lower c

== Servers == 
Here's the example work flow. Right now the vol curve server refresh every minute. I think even if I cut out the "sleep", it would maybe be a 10-15 second loop
That turns live option prices into strike vols and fits vol curves. 
Then our wing model says something like "the -3sd vol is 0.02 too high". So then we just calculate the vega of the -3sd option, multiply it by 0.02, and that's our pnl theo of the -3sd option
The forward price is fit by first fitting a discount rate at each (exp) and then a forward at each (und, exp). This forward price will not exactly equal the und price at that time due to interest rates
So we can't say something like "the vol curve's forward for this expiry was 321.894. now the stock is 323.25. Just change the forward to 323.25 and what does our model say the price of the option is now"
So perhaps the vol_curve server should communicate with the und_price server to take a snapshot of the und_price at the time that the vol_curve is fit

I think there is still an advantage to getting the live markets of the actual spread we're trading though
E.g. lets say we do all the math properly and submit a $3.40 limit bid
But the spread is 30 delta, and the underlying ticks down 3 points
So now our new bid should be 2.50
By submitting limit orders on spreads that have delta, we're accepting the cost of "when our order is filled, a lot of that is probably just bc the underlying ticked against us and we've lost some EV on that"
But we want some sort of cap on how much we're losing to that basically. Like when we submit a limit order in a stock, we just know most of the stocks we're trading are so tight / competitive, that it's unlikely our trade will ever be THAT bad
That's not true for options
I believe IBKR has some order types where you can peg the price to a reference instrument and say how much to adjust it on each tick
To summarize, I think no matter what fix we put in place right now, this will be a recurring problem and we'll eventually need some large comprehensive solution which involves us auto-updating order prices and stuff, and that's why trading options is hard
And particularly market-making options. Someone just marketin making SPX options is updating a bid and offer on the call and put in every strike in every expiry on SPX, SPY, and ES. That's probalby over 100k instruments

1. Get current positions from risk_server
2. Get theos from wing_vol_theo_server
3. Get greeks from vol_curve_server
4. Calculate current ev, vega, slega, and utility
5. Generate trade opportunities
6. For each opportunity, calculate changes in ev, vega, slega, utility
7. Find the opportunity with best marginal utility
8. For top opportunity, convert SDs to strikes
9. Suggest order to user, who can then submit it

== TODO == 
* Make the server architecture event driven s.t. when vol curves update, we immediately predict wing vols, and then immediately submit orders. Prevents large underlying movements. 
* Order adjustment server 
    * While an option order is on the book, adjust our quote based on delta and the changes in the underlying so that we're not just getting filled because of underlying movement
    * While we are waiting to close an order, we'll want to update our closing order based on any changes in the underlying
* Risk Server
    * [✗] log slega over time for each open position 
* Wing Vol Theo Server
    * [✗] Fit a vol curve using the theos. This would help us get a more exact exit price for the actual strikes we submit orders for. 
* Wing Vol Order Server
    * [✗] Use peg to bid / ask
    * [✗] Update book orders
* Refactor the servers to accept Request objects and produce Response objects
    * [✗] ibkr_position_server
    * [✗] und_price_server
    * [✓] vol_curve_server
    * [✓] wing_vol_theo_server
    * [✓] wing_vol_order_server
* Delta hedger
    * [✗] minimum amount needed to re-hedge
    * [✗] peg to bid / ask +/-%
* Dashboard
    * [✗] Table formatting
* Misc 
    * [✗] Make things work when we don't have any options positions. Currently the wing_vol_order_server and the dashboard break without any options positions.
