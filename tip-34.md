```
tip: 34
title: TRC-34 Event subscribe to support contract without ABI
author: wubin1<wubin1@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/34
category: TRC
status: accepted
created: 2019-4-19
tip: <to be assigned>
title: <TIP title>
author: <a list of the author's or authors' name(s) and/or username(s), or name(s) and email(s), e.g. (use with the parentheses or triangular brackets): FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)>
discussions-to: <URL>
status: Draft
type: <Standards Track (Core, Networking, Interface, TRC)  | Meta | Informational>
category (*only required for Standard Track): <Core | Networking | Interface | TRC>
created: <date created on, in ISO 8601 (yyyy-mm-dd) format>
requires (*optional): <TIP number(s)>
replaces (*optional): <TIP number(s)>
```

## Abstract
To support contract without ABI,  contract log parsing is separated from java-tron main program.
Moreover, developers could upload self ABI string to parse contract log and contract event,  which could be more convenient to support some contracts without ABI.

## Motivation

The contract does not need ABI anymore after the introduction of [triggerConstantContract](#31 ) api, so tron-eventquery service could support developers to upload ABI and parse contract log and contract event.

## Specification
In order to support contract without ABI, contract log parsing is separated from java-tron main program and we parse contract log in event plugin.
In addition,  the function of parse contract log is configurable. It's is true by default. 

event.subscribe = {
      contractParse = true,
    ......

If it is false, we only pass  the  raw data to developers who subscribe events.

Moreover, event query service adds three new http api for supporting developers to developers parse contract log and contract event by self upload ABI string.

Developers could subscribe triggers more conveniently.  

## Backwards Compatibility

There are no backwards compatibility concerns.

## Test Cases

1. Emitting events from contract that without ABI.
2. Emitting events from contract that with ABI.
