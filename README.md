# Reactとは

- ユーザーインターフェース構築のためのJavaScriptライブラリ
- SNSで有名なFacebook社が開発
- フロントエンドで今一番勢いのあるJavaScriptライブラリ

# Reactでできること

- Webアプリケーション開発 - React
- モバイルアプリ開発 - ReactNative(IOS, Android, マルチプラットフォーム)
- VR開発 - React360

# Reactを採用したサービスの例

- facebook, Instagram, 現地の人から借りる家、体験＆すぽっと - Airbnb, プロゲート...etc

# なぜReactが採用されるのか

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

# 環境構築

'''
mkdir React
yarn add typescript --dev
yarn install
yarn tsc --init
'''

# プロジェクトの作成

'''
npx create-react-app hello-react
'''
