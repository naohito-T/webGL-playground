# 環境構築

[参考URL](https://ics.media/entry/16329/#webpack-ts-three)

package.json作成
`$ npm init -y`
モジュールインストール
`$ npm i -D webpack webpack-cli typescript ts-loader`
threeインストール(-Sについてはあとで調べる)
`$ npm i -S three @types/three`
tsconfig.json作成
`$ touch tsconfig.json`
tsconfig記入
```json
{
  "compilerOptions": {
    // Three.jsがES5未サポートなので、割り切って比較的新しい仕様でビルドする
    "target": "ES2015",
    // TSのモジュールはES Modulesとして出力
    "module": "ES2015",
    // node_modules からライブラリを読み込む
    "moduleResolution": "node",
    // 厳密モード
    "strict": true,
    "lib": [
      "ES2020",
      "DOM"
    ]
  }
}
```
webpack.config.jsを作成
`$ touch webpack.config.js`
webpack.config.js記入
```js
module.exports = {
  // モード値を production に設定すると最適化された状態で、
  // development に設定するとソースマップ有効でJSファイルが出力される
  mode: "development",

  // メインとなるJavaScriptファイル（エントリーポイント）
  entry: "./src/index.ts",
  // ファイルの出力設定
  output: {
    //  出力ファイルのディレクトリ名
    path: `${__dirname}/dist`,
    // 出力ファイル名
    filename: "main.js"
  },
  module: {
    rules: [
      {
        // 拡張子 .ts の場合
        test: /\.ts$/,
        // TypeScript をコンパイルする
        use: "ts-loader"
      }
    ]
  },
  // import 文で .ts ファイルを解決するため
  resolve: {
    extensions: [".ts", ".js"]
  }
};
```

以上
