---
title: "GPU利用ガイド"
weight: 20
bookFlatSection: true
---

# GPU利用ガイド

以下の手順に沿って利用してください。

## 利用状況の確認

使用したいリソースを誰も使用していないか確認してください。

- Slackの [#use_computer](https://omuiserver.slack.com/archives/C07CEM8HT1D) チャンネルをチェック
- サーバー上で `nvidia-smi` コマンドを実行し、利用状況をチェック
- [GPUモニタリングツール](/docs/cluster/monitoring) をチェック

## 利用宣言

Slackの [#use_computer](https://omuiserver.slack.com/archives/C07CEM8HT1D) チャンネルで利用する旨を投稿してください。
    
{{< hint info >}}
**フォーマット**

using `[ノード名] (device: [デバイスID])` for `[期間]`

**投稿例**

using `igpu01 (device: 0)` for a while
{{</ hint >}}

## 使い終わったら

処理が終わったら上で投稿したメッセージに *released* スタンプを押してください。