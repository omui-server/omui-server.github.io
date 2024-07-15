---
title: "use_computer"
weight: 37
bookFlatSection: true
---

# use_computer

## 利用状況の確認

使用したいリソースを誰も使用していないか確認してください。

- Slackの `#use_computer` チャンネルをチェック
- `nvidia-smi` コマンドで利用状況をチェック

## 利用宣言

Slackの `#use_computer` チャンネルで利用する旨を投稿してください。
    
{{< hint info >}}
**フォーマット**

using `[ノード名] (device: [デバイスID])` for `[期間]`

**投稿例**

using `igpu01 (device: 0)` for a while
{{</ hint >}}

## 使い終わったら

処理が終わったら上で投稿したメッセージに *released* スタンプを押してください。