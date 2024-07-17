---
title: "ストレージ管理"
weight: 32
bookFlatSection: true
---

# ストレージ管理

## ストレージの使用状況 (ユーザごと)

特定のユーザのストレージの使用状況を調べるには、以下のコマンドを実行してください。
指定したディレクトリの合計容量を調べることができます。

```bash
sudo du -sh /home/[username]
```

## ストレージの使用状況 (システム全体)

システム全体のストレージの使用状況を調べるには以下のコマンドを実行してください。

```bash
df -h
```