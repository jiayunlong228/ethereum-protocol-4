---
timezone: UTC+12
---

# Bruce Xu

1. 自我介绍：E 卫兵
2. 你认为你会完成本次残酷学习吗？：会
3. 你的联系方式（推荐 Telegram）：brucexu_eth

# Notes

<!-- Content_START -->

# 2025.07.16

我的学习计划大概是：

1. 扫一遍 VB 文章，整理一些问题和思路
2. 完成 geth 源码阅读文章，本地配置好环境，适应阅读代码
3. 围绕一个 https://forum.ethpanda.org/ 协议问题，从 EIP 标准，到 geth 实现都 debug 一遍，熟悉整个流程是怎么运转的

## https://vitalik.eth.limo/general/2024/10/14/futures1.html

The Merge: key goals

- Single slot finality
- Transaction confirmation and finalization as fast as possible, while preserving decentralization
- Improve staking viability for solo stakers
- Improve robustness
- Improve Ethereum's ability to resist and recover from 51% attacks (including finality reversion, finality blocking, and censorship)

### Single slot finality

Two params:

- 2-3 epochs (~15min) to finalize a block
  - 1 epochs = 32 slots, 1 slot = 12s
  - a committee of 128 validators are selected to participate in the finality process
- 32 ETH for staking

Balance of three goals:

- Maximizing the number of validators
- Minimizing the time to finality
- Minimizing the overhead of running a node

Status quo:

- every single validator has to sign two messages each time finality happens
  - TODO what is the process of finality?
  - long time to process all signatures or beefy nodes to process all at the same time

Solutions:

- randomly selecting a committee to finalize each slot
  - easier to perform an attack, and not working well
- consensus algorithm to finalize blocks in one slot
  - e.g. [Tendermint](https://docs.tendermint.com/v0.34/introduction/what-is-tendermint.html) TODO how?
  - But does not support TODO [inactivity leak](https://eth2book.info/capella/part2/incentives/inactivity/)

Goals:

- Finalize blocks in one slot 12s
- Stake with 1 ETH, support solo stakers

Paths:

- how to make ssf work with very high validator count?
  - Brute force: better signatures aggregation (ZK-SNARKs?) to process all signatures in one slot
    - high tech, aggregating 1M+ signatures in 5-10s
    - TODO what is the current speed of aggregating signatures?
  - [Orbit committees](https://ethresear.ch/t/orbit-ssf-solo-staking-friendly-validator-set-management-for-ssf/19928/1): new mechanism to randomly-select a committee but in a safe way. TODO how?
    - relax the economic finality requirement
  - two-tiered staking: two classes of stakers, higher deposit and lower deposit.
    - centralization risks, depends on the rights that lower staking tier gets

Multiple strategies can be combined.

TODO [inclusion lists](https://ethereum-magicians.org/t/eip-7547-inclusion-lists/17474)

TODO BLS aggregation

TODO MEV attacks

What are some links to existing research for SSF?

- Paths toward single slot finality (2022): https://notes.ethereum.org/@vbuterin/single_slot_finality
- A concrete proposal for a single slot finality protocol for Ethereum (2023): https://eprint.iacr.org/2023/280
- Orbit SSF: https://ethresear.ch/t/orbit-ssf-solo-staking-friendly-validator-set-management-for-ssf/19928
- Further analysis on Orbit-style mechanisms: https://ethresear.ch/t/vorbit-ssf-with-circular-and-spiral-finality-validator-selection-and-distribution/20464
- Horn, signature aggregation protocol (2022): https://ethresear.ch/t/horn-collecting-signatures-for-faster-finality/14219
- Signature merging for large-scale consensus (2023): https://ethresear.ch/t/signature-merging-for-large-scale-consensus/17386?u=asn
- Signature aggregation protocol proposed by Khovratovich et al: https://hackmd.io/@7dpNYqjKQGeYC7wMlPxHtQ/BykM3ggu0#/
- STARK-based signature aggregation (2022): https://hackmd.io/@vbuterin/stark_aggregation
- Rainbow staking: https://ethresear.ch/t/unbundling-staking-towards-rainbow-staking/18683

### Single secret leader election

which validator is going to propose the next block is known ahead of time, therefore, leading potential DoS attacks.

TODO

# 2025.07.17

<!-- Content_END -->
