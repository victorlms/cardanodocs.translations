---
layout: default
title: 转账费用
permalink: /cardano/transaction-fees/cn/
group: cn-cardano
language: cn
---

# 卡尔达诺结算层的转账费用

## 驱动力

卡尔达诺结算层需要交易费主要因为两个原因：

1. 人们运行卡尔达诺结算层完整节点，需要花费时间、金钱和经历来运行协议，为此他们应得到补偿和奖励。在卡尔达诺结算层中与比特币不同的是，当新货币在每个区块被挖出时，交易费用是协议参与者的唯一收入来源。

2. 第二个原因是为了防 DDoS（分布式拒绝服务攻击）。在 DDoS 攻击者，攻击者尝试用虚假交易来冲击网络，如果他必须为每个虚假交易支付足够高的费用，这种攻击形式对于他来说就过于昂贵了。


## 交易费用如何运作

每当有人想要转移一定数量的 Ada，这笔转账就会有一个最低的转账费。如果想让这个交易有效，必须包含这笔很小的费用，尽管发送者可以选择支付更高的费用。

请阅读[下面](#transaction-fees-distribution)的交易分配方式。


## 最低转账费

一笔转账的最低费用通过下面的公式计算：


```
a + b × size
```

其中:

* `a` 是一个特殊常量，目前是 0.155381 ADA;
* `b` 是一个特殊常量，目前是 0.000043946 ADA/byte;
* `size` 是以字节为单位的转账数据大小


这意味着每笔交易至少需要 0.155381 ADA, 每字节的交易需要额外的 0.000043946 ADA。例如，大小为200字节（相当典型的大小）的转账费用是：

```
0.155381 ADA + 0.000043946 ADA/byte × 200 byte = 0.1641702 ADA.
```

有参数 `a` 的原因是为了防止上面提到的 DDoS 攻击：即使是非常小的虚假交易也要花费足够的代价，以此来防止试图产生成千上万交易的攻击者。

引入参数 `b` 用来反映实际成本：存储更大的交易比存储更小的交易需要更多计算机内存，因此数据量更大的交易应该比数据量小的交易收费更贵。

虽然是通过特定参数 `a` 和 `b` 计算的，这些值可能会在未来进行调整，以更好地反映实际成本。

## 交易分配方式

在一个特定 [epoch](http://cardanodocs.com/glossary/cn/#epoch) 中产生的交易费用会被收集到一个虚拟池里，然后将这个池里的资金重新分配给由 PoS 算法选举的那些 [slot 领导者](https://cardanodocs.com/glossary/cn/#slot-leader)。

在卡尔达诺结算层这个阶段，所有的区块都是有 IOHK 以及我们的合作伙伴运行的节点创建的，收集了费用（为了防止 DDoS 攻击），但它们不会被重新分配，而是被销毁。


不久，卡尔达诺结算层进入下一个阶段，[完全分布式阶段](https://cardanoroadmap.com/)后，费用会按如上所述分配。

