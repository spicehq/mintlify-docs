---
description: >-
  Returns true when the specified regular expression matches values in a column.
  Otherwise, returns false.
---

# REGEXP\_MATCHES

### Syntax <a href="#syntax" id="syntax"></a>

#### REGEXP\_MATCHES(_input_ string, _regex_ string) → boolean <a href="#regexp_matchesinput-string-regex-string--boolean" id="regexp_matchesinput-string-regex-string--boolean"></a>

* input: The expression to test.
* regex: The Perl-compatible regular expression (PCRE) to use for the test.

**Examples**

{% code title="REGEXP_MATCHES example" %}
```sql
SELECT REGEXP_LIKE('the data lakehouse', '.*?\Qlake\E.*?')
-- True
```
{% endcode %}

{% code title="REGEXP_MATCHES example" %}
```sql
SELECT Category, REGEXP_LIKE(Category, '.*?\Q-\E.*?') 
FROM eth.recent_blocks 
LIMIT 5

-- Category, EXPR$1
-- WEAPON LAWS, false
-- WEAPON LAWS, false
-- WARRANTS, false
-- NON-CRIMINAL, true
-- NON-CRIMINAL, true
```
{% endcode %}

### Usage Notes <a href="#usage-notes" id="usage-notes"></a>

This function is identical to the function [`REGEXP_LIKE`](regexp\_like.md).
