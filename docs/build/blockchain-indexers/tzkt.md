---
sidebar_position: 2
hide_table_of_contents: true
title: "TzKT"
hide_title: true
---
## TzKT

We have talked about how a blockchain includes a lot of transactions and information. Working directly on the whole blockchain to fetch and process data will be time consuming. 

[TzKT](https://github.com/baking-bad/tzkt) is a lightweight Tezos blockchain indexer with an advanced API created by the [Baking Bad](https://baking-bad.org/docs) team with huge support from the [Tezos Foundation](https://tezos.foundation/).

The indexer fetches raw data from the Tezos node, then processes it and stores in the database in such a way as to provide effective access to the blockchain data. For example, getting operations by hash, or getting all operations of the particular account, or getting detailed baking rewards, etc. None of this can be accessed via node RPC, but TzKT indexer makes this data \(and much more\) available.

### Features:

- **More detailed data.** TzKT not only collects blockchain data, but also processes and extends it to make it more convenient to work with. For example, TzKT was the first indexer introduced synthetic operation types such as "migration" or "revelation penalty", which fill in the gaps in account's history, because this data is simply not available from the node.
- **Micheline-to-JSON conversion** TzKT automatically converts raw Micheline JSON to human-readable JSON, so it's extremely handy to work with transaction parameters, contract storages, bigmaps keys, etc.
- **Tokens support** TzKT also indexes FA1.2 and FA2 tokens (including NFTs), token balances, and token transfers (including mints and burns), as well as token metadata, even if it is stored in IPFS.
- **Data quality comes first!** You will never see an incorrect account balance, or contract storage, or missed operations, etc. TzKT was built by professionals who know Tezos from A to Z (or from tz to KT 😼).
- **Advanced API.** TzKT provides a REST-like API, so you don't have to connect to the database directly (but you can, if you want). In addition to basic data access TzKT API has a lot of cool features such as "deep filtering", "deep selection", "deep sorting", exporting .csv statements, calculating historical data (at some block in the past) such as balances, storages, and bigmap keys, injecting historical quotes and metadata, built-in response cache, and much more. See the complete [API documentation](https://api.tzkt.io).
- **WebSocket API.** TzKT allows to subscribe to real-time blockchain data, such as new blocks or new operations, etc. via WebSocket. TzKT uses SignalR, which is very easy to use and for which there are many client libraries for different languages.
- **No local node needed.** There is no need to run your own local node. Also, the indexer does not create much load on the node RPC, so it's ok to use any public one. By default it uses [rpc.tzkt.io](https://rpc.tzkt.io/mainnet/chains/main/blocks/head/header).
- **No archive node needed.** There is no need to use an archive node (running in "archive" mode). If you bootstrap the indexer from the most recent snapshot, using a simple rolling node will be enough.
- **Easy to start.** Indexer bootstrap is very simple and quite fast, because you can easily restore it from a fresh snapshot, publicly available for all supported networks, so you don't need to index the whole blockchain from scratch. But of course, you can do that, if you want.
- **Validation and diagnostics.** TzKT indexer validates all incoming data so you will never get to the wrong chain and will never commit corrupted data because of invalid response from the node. Also, the indexer performs self-diagnostics after each block, which guarantees the correctness of its state after committing new data.
- **Flexibility and scalability.** TzKT is split into 3 components: indexer, database, and API, which enables quite efficient horizontal scalability ([see example](https://baking-bad.org/blog/2019/12/03/tezos-explorer-tzkt-2-overview-of-architecture-and-core-components/#general-picture)). This also enables flexible optimization, because you can optimize each component separately and according to your needs.
- **PostgreSQL.** TzKT uses the world's most advanced open source database, that gives a lot of possibilities such as removing unused indexes to reduce storage usage or adding specific indexes to increase performance of specific queries. You can configure replication, clustering, partitioning and much more. You can use a lot of plugins to enable cool features like GraphQL. This is a really powerful database.

You can [install](https://github.com/baking-bad/tzkt#installation-docker) or [build](https://github.com/baking-bad/tzkt#installation-from-source) it, and [configure](https://github.com/baking-bad/tzkt#install-tzkt-indexer-and-api-for-testnets) it for the testnet.

At this point, we want to learn how to work with the **TzKT API**. Therefore, we will work with a [public endpoint](https://api.tzkt.io/#section/Introduction).

