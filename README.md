# 情報学研究科共有GPUサーバ ユーザガイド

## Getting Started

> [!CAUTION]
> 認証情報を載せないでください。本ドキュメントはリポジトリ、デプロイ先ともに公開されています。

### インストール

1.  以下のパッケージをインストールしてください。

    1. [Hugo](https://gohugo.io/installation/) (extended edition, v0.112.0 or later)
    1. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

1.  Hugo v0.112.0以降をインストールしたことを確認してください。

    ```bash
    hugo version
    ```

1.  本リポジトリをcloneしてください

    ```bash
    git clone git@github.com:omui-server/guidelines.git
    ```

### 開発サーバー

1.  本プロジェクトのディレクトリに移動してください
    ```bash
    cd [Path to the project directory]
    ```

1.  Hugoの開発サーバーを起動してください
    ```bash
    hugo server
    ```
    `Ctrl + C` を押すとサーバーが停止します。

### コンテンツ

コンテンツファイルは `/content` 以下に保存されています。
本ドキュメントは多言語対応しており、 `/content/ja` 以下は日本語、 `/content/en` は英語のコンテンツとなっています。

コンテンツはマークダウンで記述されており、新規のコンテンツを配置する場合は以下のように `index.md` を配置してください。
また、画像を配置したいときは `index.md` と同じディレクトリに `img` ディレクトリを作成し、その中に画像を配置してください。
`[page id]`はURL上のディレクトリ名を表します。
```
.
└── content
   └── [lang]
      └── docs
         └── [section]
            └── [page id]
               ├── img
               └── index.md
```

### デプロイ

`main` ブランチにコミットすると、GitHub Actionsが自動で https://omui-server.github.io/guidelines/ にデプロイします。