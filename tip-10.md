---
tip: 10
title: TRC-10 Token Standard
author: Marcus <zhaohong229@gmail.com>
type: Standards Track
category: TRC
status: in process
created: 2018-11-11
---
## Simple Summary

A standard interface for tokens.


## Abstract


## Motivation



## Specification

## Token
### Methods

**NOTES**:


#### name

Returns the name of the token - e.g. `"MyToken"`.

OPTIONAL - This method can be used to improve usability,
but interfaces and other contracts MUST NOT expect these values to be present.


``` js
function name() public view returns (string)
```


#### symbol

Returns the symbol of the token. E.g. "HIX".

OPTIONAL - This method can be used to improve usability,
but interfaces and other contracts MUST NOT expect these values to be present.

``` js
function symbol() public view returns (string)
```



#### decimals


#### totalSupply


#### balanceOf


#### transfer


### Events


#### Transfer




#### Approval



## Implementation
