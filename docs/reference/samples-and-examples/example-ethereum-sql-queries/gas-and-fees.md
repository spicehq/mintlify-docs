---
description: Example queries that use the Ethereum Gas & Fees datasets
---

# Gas & Fees

Querying the Gas & Fees datasets enable use cases like tracking the average transaction fees for recent blocks in Ethereum, calculating the total amount of Ethereum paid in fees for all of the transactions in each block, and monitoring the average amount of gas used for a transaction. Copy example queries directly into your Spice.ai Playground to get started in seconds.&#x20;

### Average Gas Used by Transactions per Block

Gets the average amount of gas used for a transaction within a single block.

**Typical query time**: <10 seconds

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT block_number, avg(receipt_gas_used) AS avg_gas_used
FROM eth.transactions 
WHERE block_timestamp > UNIX_TIMESTAMP()-4*60*60 -- only consider transactions from 4 hours ago
GROUP BY block_number 
ORDER BY block_number DESC 
LIMIT 500
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT block_number, avg(receipt_gas_used) AS avg_gas_used
FROM polygon.transactions 
WHERE block_timestamp > UNIX_TIMESTAMP()-4*60*60 -- only consider transactions from 4 hours ago
GROUP BY block_number 
ORDER BY block_number DESC 
LIMIT 500
```
{% endtab %}
{% endtabs %}

### Avg Transaction Fees for Recent Blocks

Gets information about the average transaction fees for recent blocks and the calculation of the fee in Ethereum.

**Typical query time**: <10 seconds

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT block_number,
       TO_TIMESTAMP(block_timestamp) as block_timestamp,
       avg(gas) as avg_gas_used,
       avg(max_priority_fee_per_gas) as avg_max_priority_fee_per_gas,
       avg(gas_price) as avg_gas_price,
       avg(gas_price / 1e9) AS avg_gas_price_in_gwei,
       avg(gas * (gas_price / 1e18)) AS avg_fee_in_eth
FROM eth.transactions
WHERE block_timestamp > UNIX_TIMESTAMP()-60*60*24*10 -- last 30 days
GROUP BY block_number, block_timestamp
ORDER BY block_number DESC
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT block_number,
       TO_TIMESTAMP(block_timestamp) as block_timestamp,
       avg(gas) as avg_gas_used,
       avg(gas_price) as avg_gas_price,
       avg(gas_price / 1e9) AS avg_gas_price_in_gwei,
       avg(gas * (gas_price / 1e18)) AS avg_fee_in_eth
FROM polygon.transactions
WHERE block_timestamp > UNIX_TIMESTAMP()-60*60*24*10 -- last 30 days
GROUP BY block_number, block_timestamp
ORDER BY block_number DESC
```
{% endtab %}
{% endtabs %}

Run this query yourself using a [Kaggle notebook](https://www.kaggle.com/code/phillipleblanc/spice-xyz-ethereum-tx-average-gas-prices)

### Total Transaction Fees in Ethereum Per Block

For recent blocks, calculate the total amount of Ethereum paid in fees for all of the transactions in that block.

**Typical query time**: <15 seconds

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT eth.recent_blocks.number,
       sum(eth.recent_transactions.gas * (eth.recent_transactions.gas_price / 1e18)) AS fee_in_eth
FROM eth.recent_blocks INNER JOIN 
  eth.recent_transactions ON eth.recent_transactions.block_number = recent_blocks.number
GROUP BY recent_blocks.number
ORDER BY number DESC
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT polygon.recent_blocks.number,
       sum(polygon.recent_transactions.gas * (polygon.recent_transactions.gas_price / 1e18)) AS fee_in_matic
FROM polygon.recent_blocks INNER JOIN 
  polygon.recent_transactions ON polygon.recent_transactions.block_number = recent_blocks.number
GROUP BY recent_blocks.number
ORDER BY number DESC
```
{% endtab %}
{% endtabs %}
