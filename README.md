## 1.React

#### 1.Reactとは

- ユーザーインターフェース構築のためのJavaScriptライブラリ
- SNSで有名なFacebook社が開発
- フロントエンドで今一番勢いのあるJavaScriptライブラリ

#### 1-1.Reactでできること

- Webアプリケーション開発 - React
- モバイルアプリ開発 - ReactNative(IOS, Android, マルチプラットフォーム)
- VR開発 - React360

#### 1-2.Reactを採用したサービスの例

- facebook, Instagram, 現地の人から借りる家、体験＆すぽっと - Airbnb, プロゲート...etc

#### 1-3.なぜReactが採用されるのか

- Webページの表示速度がはやい
  - レンダリングするために必要最低限の処理
  - SPA(Single Page Application)
    - 一番最初の通信でHTMLをうけとって、そのあとはAjax通信で必要なデータのみ変更できるため表示速度がはやい。（いままでは毎回HTMLを生成していた。Googleマップなど）
  - 仮想DOM
    - DOM: JavaScriptからHTMLを自由に操作することが出来る仕組み。レンダリングする際に必ず作成される。
    - 従来はDOMを毎回破棄して作成しなおすため時間かかる。Reactの場合は仮想DOMを一旦つくり、過去の仮想DOM都の差分だけを本物のDOMに差分更新する。一から本物のDOMを作り直すよりレンダリング早い。
- UX(ユーザ体験)に非常に重要
  - ユーザの50%が3秒以内にページ表示を期待する
  - 表示速度が2秒変わるとコンバージョン率が40%も変わることが判明

#### 1-4.環境構築

```
yarn add typescript --dev
yarn install
yarn tsc --init
```

#### 1-5.Reactプロジェクトの作成

```
mkdir React
cd React
npx create-react-app hello-react
```

#### 1-6.Reactプロジェクトの開始

```
cd /React/hello-react
yarn start
```

## 2.JSX

#### 2.JSXとは

- Facebook社が開発したJavaScriptの拡張構文
- jsファイル上で、ほぼHTMLと同じ記述が出来る
- Reactを使う上で必須ではないが、ReactでSPAつくるなら使うと便利（直感的にも理解しやすい。jsでもできるが非推奨）
- jsでも同様の機能実装ができるが見にくい

  - JSXの場合

  ```
    <div className="App">
      <p>helloworld</p>
    </div>
  ```

  - JSの場合

  ```
    React.createElement(
      'div',
      {
        className: 'App',
      },
      React.createElement('p', null, 'helloworld'),
    )
  ```

## 3.Component

#### 3.Componentとは

- 再利用可能なUI部品
  - UI(User Interface)
    - ユーザとサービスの接触面
    - Webサービスにおいてユーザの目に触れる部分
    - 具体例
      - ボタン
      - 入力フォーム
      - 検索結果一覧
- メリット
  - 部品化することで様々なところで再利用できる
- Class Component
- state
- props
- lifecycle
- などの状態を付加できる
- Functional Component
  - props
  - 余計な情報を付加させない
  - Hooks
    - state
    - lifecycle
    - 最近はHooksをつかったFunctional Componentsが主流
- 実際にコーディングしてみよう！
  - hello-reactプロジェクトを開く
  - セットアップ
    - デフォルトのファイルを削除
    - index.jsの作成
    - App.jsの作成
  - semantic-uiの導入
    - CSSフレームワーク
    - 指定されたクラス名を記述
    - CSSを記述せずに綺麗なUIを作成できる
    - semantic ui cdn
  - Button.jsの作成
