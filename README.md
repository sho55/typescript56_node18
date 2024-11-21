# TypeScript Docker Sample

このリポジトリは、Dockerを使用してTypeScriptプロジェクトをセットアップするサンプルプロジェクトです。以下の手順に従って環境を構築し、TypeScriptコードを実行することができます。

## ファイル構成

```
.
├── docker-compose.yaml
├── docker-config
│   └── typescript
│       └── Dockerfile
├── package.json
├── src
│   ├── js
│   │   └── index.js
│   └── ts
│       └── index.ts
└── tsconfig.json
```

### 主なディレクトリ

- **docker-config/typescript/**: Dockerfileを含む、Docker設定用ディレクトリ。
- **src/ts/**: TypeScriptファイルを格納するディレクトリ。
- **src/js/**: コンパイル後のJavaScriptファイルが格納されるディレクトリ。

---

## セットアップ

1. **リポジトリのクローン**
   ```bash
   git clone https://github.com/your-repo/typescript-docker-sample.git
   cd typescript-docker-sample
   ```

2. **Dockerコンテナのビルドと起動**
   ```bash
   docker-compose up --build
   ```

3. **TypeScriptコードの編集**
   `src/ts/index.ts` を編集してTypeScriptコードを追加します。

4. **コードのビルド**
   コンテナ内で自動的に `npm run build` が実行され、`src/js/` にJavaScriptファイルが生成されます。

---

## 動作確認

1. コンテナが正しく起動しているか確認：
   ```bash
   docker-compose ps
   ```

2. TypeScriptファイルを編集して保存すると、対応するJavaScriptが自動生成されます。生成されたファイルを確認：
   ```bash
   ls src/js
   ```

---

## トラブルシューティング

### エラー: `No inputs were found in config file`
- 原因: `tsconfig.json` の `include` または `exclude` が誤って設定されている可能性があります。
- 解決策: `tsconfig.json` を以下のように修正してください。
  ```json
  "include": ["src/ts/**/*.ts"],
  "exclude": ["src/js/**/*"]
  ```

### エラー: `failed to compute cache key`
- 原因: `Dockerfile` の `COPY` ステートメントでファイルが見つからない。
- 解決策: `Dockerfile` に正しいパスを指定してください。
  ```dockerfile
  COPY ./src ./src
  ```

### コンテナ内のファイルが正しくマウントされない
- 解決策: `docker-compose.yaml` の `volumes` を以下のように確認してください。
  ```yaml
  volumes:
    - ./src:/app/src
  ```

---

## 使用技術

- **Docker**: コンテナ化ツール。
- **Node.js**: JavaScriptランタイム環境。
- **TypeScript**: JavaScriptのスーパーセット。

---

## ライセンス

このプロジェクトは [MITライセンス](LICENSE) のもとで公開されています。