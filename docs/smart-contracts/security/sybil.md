---
id: sybil
title: Sybil Attacks
description: "Learn about sybil attacks in NEAR smart contracts and how to prevent them with proper identity verification and anti-gaming mechanisms."
---

While developing your smart contract, keep in mind that an individual can potentially create multiple NEAR accounts. This is especially relevant in ecosystems involving crowd decisions, such as [DAOs](../../primitives/dao.md). 

Imagine that you open the voting to anyone in the community. If each account can cast a vote, a malicious actor could span multiple accounts and gain a disproportionately large influence on the result.