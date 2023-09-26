---
locale: zh
---
# 发布交易

有几种方法可以将交易发布到Arweave上。每种方法都具有自己独特的优势和限制。下面的图示展示了发布交易的四种主要方法。

`直接发送到节点`，`直接发送到网关`，`打包`和`分配`。

<img src="https://arweave.net/Z1eDDnz4kqxAkkzy6p5elMz-jKnlaVIletp-Tm6W8kQ" width="550">

::: tip <img src="https://arweave.net/blzzObMx8QvyrPTdLPGV3m-NsnJ-QqBzvQIQzzZEfIk" width="20"> 保证交易
当发布大量的交易或者追求快速结算时间时，考虑使用打包服务。打包器立即结算大量的交易，并在毫秒内提供交易数据。打包服务会保留已发布的交易，直到它们在链上得到确认。如果这些交易没有包含在最新的区块中，打包服务将在每个新的区块中重新发布它们，直到它们得到足够数量的确认并记录在区块链上。
:::

## 直接交易

直接发布到Arweave的交易有两种类型：**钱包到钱包**交易和**数据**交易。第一种在钱包地址之间转移**AR**代币。第二种将数据发布到Arweave并支付相关的存储费用。

有趣的是，**数据**交易也可以同时将**AR**代币转移到钱包地址，并同时支付存储费用。

所有的交易都允许用户以最多2KB的元数据形式进行指定，称为[自定义标签](./tags.md)。

### 直接发送到节点

交易可以直接发布到Arweave的节点（挖矿节点）。这可能是最为去中心化的发布交易方式，因为客户端可以自由选择希望发布的节点。

这种方法不是没有缺点的。节点可能会离线，导致从应用程序可靠地发布交易变得困难。虽然可以查询活动节点列表并在发布之前选择一个节点，但这会增加流程的开销和摩擦。此外，发布到节点的交易只有在其被挖掘到区块后，在网关上才可以查询。这会导致从发布交易到它在浏览器从网关中可读取之间有1-2分钟的延迟。

出于上述原因，开发者往往会在发布直接交易时将`arweave-js`配置为指向一个网关，因为网关上的乐观缓存使得交易几乎立即可用。

### 直接发送到网关

网关位于客户端和Arweave的节点网络之间。网关的主要功能之一是索引交易并乐观地缓存发布到网络的数据，同时等待它们被包含在区块中。这使得交易在“待处理”(Pending)状态下几乎可以立即进行查询，从而使在网关上构建的应用程序能够更加响应。然而，如果交易未在节点的区块中被挖掘，它们可能会从乐观缓存中消失。

使用类似于[bundlr.network](https://bundlr.network)的打包服务时，您必须在发布交易之前在打包器节点上进行一笔小额存款。这使得打包服务能够计费，而无需每次直接在Arweave上结算**AR**代币转移的开销。

[bundlr.network](https://bundlr.network)允许客户端使用多种[支持的加密货币](https://docs.bundlr.network/docs/currencies)进行存款。

::: info
当交易被发布到bundlr.network上时，它们也会出现在连接的网关的乐观缓存中，因此几乎可以立即进行查询。
:::

使用`bundlr.network/client`，您可以在[此指南](../guides/posting-transactions/bundlr.md)中找到有关如何发布打包交易的示例。

## 打包交易

在Arweave之上构建的提供额外便利的永久网络构建工具有时被称为永久网络服务，其中一个就是打包器。打包器接受多个单独的交易，并将它们打包成单个交易，直接发布到Arweave。通过这种方式，协议层面上的单个交易可以包含成千上万个打包交易。但是，有一个限制，只有**数据**交易可以包含在一个打包交易中。**钱包到钱包**交易（在钱包地址之间转移**AR**代币）必须作为单独的交易直接发布到Arweave。

使用类似于[bundlr.network](https://bundlr.network)的打包服务时，您必须在发布交易之前在打包器节点上进行一笔小额存款。这使得打包服务能够计费，而无需每次直接在Arweave上结算**AR**代币转移的开销。

[bundlr.network](https://bundlr.network)允许客户端使用多种[支持的加密货币](https://docs.bundlr.network/docs/currencies)进行存款。

::: info
当交易被发布到bundlr.network上时，它们也会出现在连接的网关的乐观缓存中，因此几乎可以立即进行查询。
:::

使用`bundlr.network/client`，您可以在[此指南](../guides/posting-transactions/bundlr.md)中找到有关如何发布打包交易的示例。

## 分配交易

发布捆绑交易的另一种方法是通过浏览器。虽然浏览器对可上传的数据大小施加了一些限制，但基于浏览器的钱包仍然可以将交易发布到打包器。Arweave浏览器钱包实现了一个`dispatch()`的API方法。如果您发布的是小交易（100KB或更小），即使您的应用程序未使用`bundlr.network/client`，您也可以使用钱包的`dispatch()`方法利用打包交易的优势。

使用Arweave钱包的`dispatch()`方法，您可以在[此指南](../guides/posting-transactions/dispatch.md)中找到如何发布一个大小为100KB或更小的打包交易的示例。

## 资源

- [arweave-js](../guides/posting-transactions/arweave-js.md) 示例
- [bundlr.network](../guides/posting-transactions/bundlr.md) 示例
- [dispatch](../guides/posting-transactions/dispatch.md) 示例