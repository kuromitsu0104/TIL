# TOC<!-- omit in toc -->

- [概要](#概要)
- [関連記事](#関連記事)
- [トランザクション分離レベル](#トランザクション分離レベル)
  - [READ UNCOMMITTED](#read-uncommitted)
  - [READ COMMITTED](#read-committed)
    - [READ\_COMMITTED\_SNAPSHOTオプションによる挙動の違い](#read_committed_snapshotオプションによる挙動の違い)
      - [OFFの場合（デフォルト）](#offの場合デフォルト)
      - [ONの場合](#onの場合)
  - [SERIALIZABLE](#serializable)
  - [SNAPSHOT](#snapshot)
- [各事象について](#各事象について)
  - [ダーティリード](#ダーティリード)
  - [ファジーリード](#ファジーリード)
  - [ファントムリード](#ファントムリード)

# 概要

SQL Serverのトランザクション分離レベルについて調べる

# 関連記事

- [SQL Serverのスナップショット分離レベル導入によるデータ基盤連携の課題解決](https://techblog.zozo.com/entry/sqlserver-transaction-isolation-level-snapshot)
- [SQL Server の読み取り一貫性とロック](https://bellsoft.jp/blog/system/detail_586)

# トランザクション分離レベル

| 分離レベル | ダーティリード | ファジーリード | ファントムリード |
| --- | --- | --- | --- |
| READ UNCOMMITTED | 発生する | 発生する | 発生する |
| READ COMMITTED（READ_COMMITTED_SNAPSHOT OFF） | 発生しない | 発生する | 発生する |
| READ COMMITTED（READ_COMMITTED_SNAPSHOT ON） | 発生しない | 発生する | 発生する |
| REPEATABLE READ | 発生しない | 発生しない | 発生する |
| SNAPSHOT | 発生しない | 発生しない | 発生しない |
| SERIALIZABLE | 発生しない | 発生しない | 発生しない |

デフォルトは`READ COMMITTED`である。（※変更不可）

ヒントによってトランザクション分離レベルを変更できる

- `WITH(NOLOCK)`あり
  - 「READ UNCOMMITTED」分離レベルでクエリを実行
- `WITH(NOLOCK)`なし
  - 「READ COMMITTED」分離レベルでクエリを実行

## READ UNCOMMITTED

ダーティリードを許容してしまう。

## READ COMMITTED

### READ_COMMITTED_SNAPSHOTオプションによる挙動の違い

トランザクション分離レベルは同じだが、共有ロックの取得有無に違いがある。

#### OFFの場合（デフォルト）

共有ロックを取得するため、排他ロックされたデータは解除されるまで読み出しできない。（SQL Serverでデッドロックは発生しやすい要因の一つ）

#### ONの場合

OracleのMVCCに近い挙動になる。

tempdbで行のバージョン管理を行うようになり、共有ロックを取得することなくデータを読み出しできるようになる。

## SERIALIZABLE

同時実行性のない分離レベルのため、多重でクエリが発行されるような状況下では利用するべきでない。

## SNAPSHOT

SQL Server独自の分離レベル。

SERIALIZABLEと同じ分離レベルでありながら同時実行性を担保する。

トランザクションの開始後、他のクエリによって変更されたデータに対して変更をコミットしようとすると、ロールバックされエラーとなる。

# 各事象について

## ダーティリード

あるトランザクションが更新されている最中に、他のトランザクションからデータを読み出すことができてしまう現象のこと

## ファジーリード

読み出した行がほかのトランザクションにより更新または削除され、同じトランザクションで再度同じ行を読み込んだときに、その行が更新または削除されていること

## ファントムリード

読み出した行がほかのトランザクションにより更新または削除され、同じトランザクションで再度同じ行を読み込んだときに、その行が更新または削除されていること
