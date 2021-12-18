Changes from original strategy:
* Only be long or short one lot for any given stock to prevent position accumulation. 
* Use stop limits at 100 bps to prevent large losses

Questions:
* [✗] Sometimes commission charges are more than 1 dollar even if using 200 shares. 
* [✗] Why would anyone ever not use tiered? 
* Should we consider updating the limit or stop limit order depending on our theo
* [✗] Should we end each day position neutral? 
    * Keep track of how long it takes on average to settle a trade per symbol. Don't allow entering that position n minutes before close.
    * In case we are still in a position x minutes to close, gradually converge the stop limit order with the outstanding bid / ask

Follow ups:
* Compute theo as a function of intrinsic risk (SPY exposure) and sector risk (basket exposure)
* [✗] Consider using asymmetric quoting. ie, if market is below theo, bid is likely to be filled, so request a smaller edge on the asking side. 
* When we are in a long / short position, update the outstanding bid / ask base bd on new theos.
* Parameter tuning for edge and stop bps
* deadpixi contracts for testing
* Test on market crash / rally days. Do we continuously enter short positions and then trigger the stop order? 
* How long do we hold each position? Are there some positions that we're just holding all day and missing out on trade opportunities for?
* How good is our theo compared to a baseline of just using the market price as theo? 
* Place a max loss bps so we stop trading if we lose ~100 bps of account value. 
* Need to figure out when we should stop entering new positions.

Meeting Notes:
* I computed the corrected bps. Average bps over past 20 days:
    * 2 bps per trade
    * 33 bps per day over account value
* The original algo updated quotes every minute which had the effect of us accumulating large positions and hitting cash / margin limits. This made it hard to debug where things were going wrong, so I decided to simplify first and build up to the complex strategy one step at a time.
    * First, to prevent position accumulation, I only allow us to be long / short a single lot at any given time for a given symbol. We ask for 3 bps of edge above and below our theo. 
        * As a side note, I did try leaning the quotes on one live traded paper session, but still had issues with position accumulation. I can retry this method with the backtester and compare it to the symmetric quoting to see how much it helps. 
    * Second, rather than dynamically updating the quote every minute, I keep our bid on the book if we enter a short position and keep the ask if we enter a long position. If we're in no position, then we keep quoting until we do enter. 
    * Third, I placed stop limit orders 100 bps above / below theo so that we can stop losses when we're stuck on the wrong side of a trade for a long time. 
* 
