---


---

<p>Uniswap v1 was launched in November 2018 as a proof of concept for automated market makers (AMMs), a type of exchange where anyone can pool assets into shared market making strategies.</p>
<p>In May 2020, Uniswap v2 introduced new features and optimizations, setting the stage for exponential growth in AMM adoption. Less than one year since its launch, v2 has facilitated over $135bn in trading volume, ranking as one of the largest cryptocurrency spot exchanges in the world.</p>
<p>Uniswap now serves as critical infrastructure for decentralized finance, empowering developers, traders, and liquidity providers to participate in a secure and robust financial marketplace.</p>
<p>Today, we are excited to present an overview of Uniswap v3. We are targeting an  <strong>L1 Ethereum mainnet launch on May 5</strong>, with an  <strong>L2 deployment on Optimism set to follow shortly after.</strong></p>
<p>Uniswap v3 introduces:</p>
<ul>
<li>
<p><strong>Concentrated liquidity,</strong>  giving individual LPs granular control over what price ranges their capital is allocated to. Individual positions are aggregated together into a single pool, forming one combined curve for users to trade against</p>
</li>
<li>
<p><strong>Multiple fee tiers</strong>, allowing LPs to be appropriately compensated for taking on varying degrees of risk</p>
</li>
</ul>
<p>These features make Uniswap v3  <strong>the most flexible and efficient AMM ever designed</strong>:</p>
<ul>
<li>
<p>LPs can provide liquidity with  <strong>up to 4000x capital efficiency</strong>  relative to Uniswap v2, earning  <strong>higher returns on their capital</strong></p>
</li>
<li>
<p>Capital efficiency paves the way for low-slippage  <strong>trade execution that can surpass both centralized exchanges and stablecoin-focused AMMs</strong></p>
</li>
<li>
<p>LPs can significantly  <strong>increase their exposure to preferred assets</strong>  and  <strong>reduce their downside risk</strong></p>
</li>
<li>
<p>LPs can sell one asset for another by adding liquidity to a price range entirely above or below the market price, approximating  <strong>a fee-earning limit order that executes along a smooth curve</strong></p>
</li>
</ul>
<p>Uniswap’s  <strong>oracles are now far easier and cheaper to integrate</strong>. V3 oracles are capable of providing time-weighted average prices (TWAPs) on demand for any period within the last ~9 days. This removes the need for integrators to checkpoint historical values.</p>
<p>Even with these groundbreaking design improvements, the  <strong>gas cost of v3 swaps on Ethereum mainnet is slightly cheaper than v2</strong>. Transactions made on the Optimism deployment will likely be  <em>significantly</em>  cheaper!</p>
<p>Read on for more details on Uniswap v3. For a deeper technical overview check out the  <a href="https://uniswap.org/whitepaper-v3.pdf">Uniswap v3 Core whitepaper</a>, the  <a href="https://github.com/Uniswap/uniswap-v3-core/">Uniswap v3 Core smart contracts</a>.</p>
<h1 id="concentrated-liquidity"><a href="https://blog.uniswap.org/uniswap-v3#concentrated-liquidity"></a>Concentrated Liquidity</h1>
<p>In Uniswap v2, liquidity is distributed evenly along an x*y=k price curve, with assets reserved for all prices between 0 and infinity. For most pools, a majority of this liquidity is never put to use. As an example,  <strong>the v2 DAI/USDC pair reserves just ~0.50% of capital for trading between $0.99 and $1.01</strong>  , the price range in which LPs would expect to see the most volume and consequently earn the most fees.</p>
<p>V2 LPs only earn fees on a small portion of their capital, which can fail to appropriately compensate for the price risk (“impermanent loss”) they take by holding large inventories in both tokens. Additionally, traders are often subject to high degrees of slippage as liquidity is spread thin across all price ranges.</p>
<p>In Uniswap v3, LP’s can  <strong>concentrate their capital within custom price ranges, providing greater amounts of liquidity at desired prices.</strong>  In doing so,  <strong>LPs construct individualized price curves</strong>  that reflect their own preferences.</p>
<p>LPs can combine any number of distinct concentrated positions within a single pool. For example, an LP in the ETH/DAI pool may choose to allocate $100 to the price ranges $1,000-$2,000 and an additional $50 to the ranges $1,500-$1,750.</p>
<p>By doing so, an LP can approximate the shape of any automated market maker or active order book.</p>
<p><strong>Users trade against the combined liquidity of all individual curves</strong>  with no gas cost increase per liquidity provider. Trading fees collected at a given price range are split pro-rata by LPs proportional to the amount of liquidity they contributed to that range.</p>
<h2 id="capital-efficiency"><a href="https://blog.uniswap.org/uniswap-v3#capital-efficiency"></a>Capital Efficiency</h2>
<p>By concentrating their liquidity, LPs can provide  <strong>the same liquidity depth as v2 within specified price ranges while putting far less capital at risk.</strong>  The capital saved can be held externally, invested in different assets, deposited elsewhere in DeFi, or used to increase exposure within the specified price range to earn more trading fees.</p>
<p>Let’s illustrate with an example:</p>
<p>Alice and Bob both want to provide liquidity in an ETH/DAI pool on Uniswap v3. They each have $1m. The current price of ETH is 1,500 DAI.</p>
<p>Alice decides to deploy her capital across the entire price range (as she would have in Uniswap v2). She deposits 500,000 DAI and 333.33 ETH (worth a total of $1m).</p>
<p>Bob instead creates a concentrated position, depositing only within the price range from 1,000 to 2,250. He deposits 91,751 DAI and 61.17 ETH, worth a total of about $183,500. He keeps the other $816,500 himself, investing it however he prefers.</p>
<p>While Alice has put down 5.44x as much capital as Bob,  <em>they earn the same amount of fees</em>, as long as the ETH/DAI price stays within the 1,000 to 2,250 range.</p>
<p><img src="https://images.ctfassets.net/oc3ca6rftwdu/pgajcrSvF51NZo6WQ7QMT/aa4dc1497cab699f5b5747e69160d9c5/example_1.png" alt="example 1"></p>
<p>Bob’s custom position also acts as a kind of stop-loss for his liquidity. Both Alice and Bob’s liquidity will be entirely denominated in ETH if the price of ETH falls to $0. However, Bob will have lost just $159,000, versus Alice’s $1m. Bob can use his additional $816,500 to hedge against downside exposure or to invest in any other conceivable strategy.</p>
<p><img src="https://images.ctfassets.net/oc3ca6rftwdu/7fJVwfL5ZEqwsfiAH6JvCV/74dcdb9c8d2500547e7bd1df272a14da/example_2.png" alt="example 2"></p>
<p>Instead of providing equivalent liquidity depth as a v2 LPs with less capital, v3 LPs can choose to provide  <strong>greater depth with the same amount of capital</strong>  as their v2 counterparts. This requires  <strong>taking on more price risk</strong>  (“impermanent loss”) while supporting greater amounts of trading and earning higher fees.</p>
<p>LPs in more stable pools will likely provide liquidity in particularly narrow ranges. If the ~$25m currently held in the Uniswap v2 DAI/USDC pair was instead concentrated between 0.99 — 1.01 in v3, it would provide the same depth as $5bn in Uniswap v2 as long as the price stayed within that range.  <strong>If the ~$25m was concentrated into the 0.999 - 1.001 range it would provide the same depth as $50b in Uniswap v2.</strong></p>
<p>The tool below calculates the capital efficiency gains of a concentrated liquidity position (centered around the current price) relative to allocating capital across the entire price curve.</p>
<p>Liquidity Deposit Value</p>
<p>Value of paired tokens</p>
<p>$</p>
<p>Select ETH price range</p>
<p>Current Price: $1,820</p>
<p>V3 Range Position</p>
<p>Capital Required</p>
<p>$150,000</p>
<p>Fees per $ vs. V2</p>
<p>5.24x</p>
<p>V2 Position</p>
<p>Capital Required</p>
<p>$785,779</p>
<p>These two positions will earn equal fees and perform idenitcally while the price remains between $1200  and $2800.</p>
<p>At launch, capital efficiency gains will max out at 4000x for LPs providing liquidity within a single 0.10% price range. The v3 pool factory is technically capable of supporting ranges as granular as 0.02%, translating to a maximum 20,000x capital efficiency gains relative to v2. However, more granular pools can increase swap gas costs and might be more useful on Layer 2.</p>
<h2 id="active-liquidity"><a href="https://blog.uniswap.org/uniswap-v3#active-liquidity"></a>Active Liquidity</h2>
<p>If market prices move outside an LP’s specified price range, their liquidity is effectively removed from the pool and is no longer earning fees. In this state, an LP’s liquidity is composed entirely of the less valuable of the two assets, until the market price moves back into their specified price range or they decide to update their range to account for current prices.</p>
<p>In v3, it is theoretically possible for no liquidity to exist in a given price range. However, we expect rational LPs to continuously update their price ranges to cover the current market price.</p>
<h2 id="range-orders"><a href="https://blog.uniswap.org/uniswap-v3#range-orders"></a>Range Orders</h2>
<p>v3’s LP customizability opens up a novel order feature to complement market orders, which we are calling “range orders”.</p>
<p>LPs can deposit a single token in a custom price range above or below the current price: if the market price enters into their specified range, they sell one asset for another along a smooth curve while earning swap fees in the process.</p>
<p>Depositing to a narrow range feels similar to a traditional limit order. For example, if the current price of DAI is below 1.001 USDC, Alice could add $10m worth of DAI to the range of 1.001 — 1.002 DAI/USDC.</p>
<p>Once DAI trades above 1.002 DAI/USDC, Alice’s liquidity will have fully converted into USDC. Alice must withdraw her liquidity (or use a third-party service to withdraw on her behalf) to avoid automatically converting back into DAI if DAI/USDC starts trading below 1.002.</p>
<p><img src="https://images.ctfassets.net/oc3ca6rftwdu/2l33qlFlZ6f1KmeJOZ3rDp/55b6546fa088b619d70dcb3a5a54889d/range.png" alt="range"></p>
<p>The average execution price of a fully executed range order is the geometric average of the minimum and maximum price: in Alice’s case, the execution price equals 1.001499 DAI/USDC for a total of $1,001,499. This execution price does not account for additional swap fees earned during the period in which prices trade within the 1.001 — 1.002 DAI/USDC range.</p>
<p>Range orders within wider ranges may prove particularly useful for  <strong>profit-taking, buying the dip,</strong>  and  <strong>primary issuance events</strong>: in the later use case, issuers are now able to deposit liquidity in a single asset and specify the exact range of prices across which they wish to sell their tokens.</p>
<h2 id="non-fungible-liquidity"><a href="https://blog.uniswap.org/uniswap-v3#non-fungible-liquidity"></a>Non-Fungible Liquidity</h2>
<p>As a byproduct of per-LP custom price curves, liquidity positions are no longer fungible and are not represented as ERC20 tokens in the core protocol.</p>
<p>Instead, LP positions will be represented by non-fungible tokens (NFTs). However, common shared positions can be made fungible (ERC20) via peripheral contracts or through other partner protocols. Additionally, trading fees are no longer automatically reinvested back into the pool on LPs’ behalf.</p>
<p>Over time we expect increasingly sophisticated strategies to be tokenized, making it possible for LPs to participate while maintaining a passive user experience. This could include multi-positions, auto-rebalancing to concentrate around the market price, fee reinvestment, lending, and more.</p>
<h1 id="flexible-fees"><a href="https://blog.uniswap.org/uniswap-v3#flexible-fees"></a>Flexible Fees</h1>
<p>Uniswap v3 offers LPs three separate fee tiers per pair — 0.05%, 0.30%, and 1.00%. This array of options ensures that LPs tailor their margins according to expected pair volatility: LPs take on more risk in non-correlated pairs like ETH/DAI and, conversely, take on minimal risk in correlated pairs like USDC/DAI.</p>
<p>Although distinct fee tiers may lead to some degree of liquidity fragmentation, we believe that most pairs will calibrate to an obvious fee tier, which then serves as the canonical market. We expect like-kind asset pairs to congregate around the 0.05% fee tier and pairs like ETH/DAI to use 0.30%, while exotic assets might find 1.00% swap fees more appropriate. governance can add additional fee tiers as needed.</p>
<p>Uniswap v2 introduced a protocol fee switch, which allowed a flat 5 basis point (16.66% of LP fees) fee to be turned on by governance. Uniswap v3 protocol fees are far more flexible. Fees will be off by default, but can be turned on by governance on a per-pool basis and set between 10% and 25% of LP fees.</p>
<h1 id="advanced-oracles"><a href="https://blog.uniswap.org/uniswap-v3#advanced-oracles"></a>Advanced Oracles</h1>
<p>Uniswap v2 introduced time weighted average price (TWAP) oracles. These oracles serve as a critical piece of DeFi infrastructure, and have been integrated into dozens of projects, including Compound and Reflexer.</p>
<p>V2 oracles work by storing cumulative sums of Uniswap pair prices on a per-second basis. These price sums can be checked once at the beginning of a period and once at the end to calculate an accurate TWAP over that period.</p>
<p>Uniswap v3 offers significant improvements to the TWAP oracle, making it possible to calculate any recent TWAP within the past ~9 days in a single on-chain call. This is achieved by storing an array of cumulative sums instead of just one.</p>
<p><img src="https://images.ctfassets.net/oc3ca6rftwdu/645gRZmrsruhM4dXb2obKR/581ef8cb9406de64f2acd27145f1e778/oracles.png" alt="oracles"></p>
<p>This array of historical price accumulators makes it far easier and cheaper to create more advanced oracles that include simple-moving averages (SMA), exponential moving averages (EMA), outlier filtering, and more.</p>
<p>Despite this major improvement, the gas cost to Uniswap traders for keeping oracles up to date has been reduced by ~50% relative to v2. The costs for calculating TWAPs in external smart contracts is significantly cheaper as well.</p>

