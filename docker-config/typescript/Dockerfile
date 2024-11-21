FROM node:18

# 作業ディレクトリを設定
WORKDIR /app

# パッケージマネージャを最新化
RUN npm install -g npm

# 必要なファイルをコピー（package.json, tsconfig.json）
COPY package.json tsconfig.json ./

# パッケージをインストール
RUN npm install

# ソースコードをコピー
COPY ./src ./src

# TypeScriptをコンパイル
RUN npm run build


# デフォルトコマンドを設定
CMD ["npm", "run", "dev"]