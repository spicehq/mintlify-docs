---
description: Example queries that use the Ethereum and Polygon Tokens datasets
---

# Tokens

Querying the Tokens datasets enable use cases like finding a token's recent token transfers and the token standard information, and getting Spice's confidence (as a score from 0 to 1) on whether a smart contract implements the given token standard. Copy example queries directly into your Spice.ai Playground to get started in seconds.&#x20;

### Get Token Transfers with Token Standard

Get recent token transfers along with the token standard the token is using.

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT token_address, 
       token_standard, 
       from_address, 
       to_address, 
       token_id, 
       "value", 
       transaction_hash, 
       log_index, 
       block_number 
FROM eth.recent_token_transfers 
ORDER BY block_number DESC
LIMIT 10
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT token_address, 
       token_standard, 
       from_address, 
       to_address, 
       token_id, 
       "value", 
       transaction_hash, 
       log_index, 
       block_number 
FROM polygon.recent_token_transfers 
ORDER BY block_number DESC
LIMIT 10
```
{% endtab %}
{% endtabs %}

### Get Tokens With Standard

Use the tokens table to get information about the token standard that the token is using.

**Typical query time**: <20 seconds

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT symbol, name, is_erc20, is_erc721, is_erc1155
FROM eth.tokens
WHERE name != ''
ORDER BY name
LIMIT 10
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT symbol, name, is_erc20, is_erc721, is_erc1155
FROM polygon.tokens
WHERE name != ''
ORDER BY name
LIMIT 10
```
{% endtab %}
{% endtabs %}

### Get Confidence for Token Standards

Get Spice's confidence (as a score from 0 to 1) on whether a smart contract implements the given token standard.

{% tabs %}
{% tab title="Ethereum" %}
```sql
SELECT address, erc20_confidence, erc721_confidence, erc1155_confidence
FROM eth.contracts
WHERE erc20_confidence > 0 OR erc721_confidence > 0 OR erc1155_confidence > 0
LIMIT 10
```
{% endtab %}

{% tab title="Polygon" %}
```sql
SELECT address, erc20_confidence, erc721_confidence, erc1155_confidence
FROM polygon.contracts
WHERE erc20_confidence > 0 OR erc721_confidence > 0 OR erc1155_confidence > 0
LIMIT 10
```
{% endtab %}
{% endtabs %}
