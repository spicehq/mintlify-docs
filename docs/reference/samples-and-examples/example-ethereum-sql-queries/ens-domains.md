---
description: Example queries that use the Ethereum Name Service Domains datasets
---

# ENS Domains

Querying the ENS Domains datasets enable use cases like retrieving the Ethereum address of a domain or subdomain, and listing Ethereum addresses with the most ENS names. Copy example queries directly into your Spice.ai Playground to get started in seconds.&#x20;

### Retrieve an Ethereum address

Get the Ethereum address of a domain or subdomain, or perform a reverse look-up.

#### Look up a domain

**Typical query time**: <1 second.

```sql
--- *.eth domain look-up:
SELECT * FROM ens.domains WHERE name='spiceai.eth'
```

#### Look up a subdomain

**Typical query time**: <1 second.

```sql
SELECT * FROM ens.domains WHERE name='ccc.earth.eth'
```

#### Reverse lookup a domain from eth\_address

**Typical query time**: <1 second.

```sql
--- reverse look-up:
SELECT * FROM ens.domains WHERE eth_address='0x425ec049c2a4722edfd770ab7bc4f9ca8b7bd815'
```



**Ethereum addresses that have most ENS names**

**Typical query time**: <1 second.

<pre class="language-sql"><code class="lang-sql">SELECT COUNT(*) AS num_names, owner
FROM ens.domains
<strong>WHERE owner IS NOT NULL
</strong>GROUP BY owner
ORDER BY COUNT(*) DESC
</code></pre>

