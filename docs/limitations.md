# Limitations

{% hint style="info" %}
For higher limits become a [Design Partner](https://www.craft.do/s/bgJFtYzSZwuFXD)
{% endhint %}

In beta, Spice.ai has a number of limitations, including:

#### Global API Limits

* 10 apps per account.
* 10 request-per-second (rps).
* 90-second request/query timeout.
* 500 row limit for HTTP API results (use the [Apache Arrow API](api/sql-query-api/apache-arrow-flight-api.md) or the [Async HTTP API](api/sql-query-api/http-api-1.md) for no limit).

#### Guest API Limits - No API Key

* 4 request-per-minute SQL API limit.
* 10 row result limit.

#### **Apache Flight Endpoint**

* API Key (provided as gRPC password) is always required.

#### **SQL Query Limits**

* 3 concurrent-requests.

#### Data Limitations (as of June 2022)

* 128-bit integer limit (while data can be uint256). We include both the 128-bit `DECIMAL(38)` type and `_hex` fields where the type is 256-bit.

#### Data format limitations

* List data cannot be downloaded as CSV
  * If you wish to download list data as CSV, you should use the [flatten](https://docs.dremio.com/software/sql-reference/sql-functions/functions/FLATTEN/) operator first:
    * `select topics from eth.logs limit 1` will **NOT** be able to be downloaded as CSV
    * `select flatten(topics) from eth.logs limit 1` _will_ be able to be downloaded as CSV
