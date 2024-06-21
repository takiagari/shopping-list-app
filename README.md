# ショッピングリストアプリ

## アプリ概要
Vue.jsとローカルストレージを使用して作成されたシンプルなショッピングリストアプリです。  
購入するアイテムとその個数をリストに追加し、リストからアイテムを削除することができます。  
リストはブラウザのローカルストレージに保存されるため、ページをリロードしてもデータは保持されます。

## アプリ機能
- **アイテムの追加**:
  - アイテム名と個数を入力し、リストに追加することができます。
  - 個数のデフォルト値は1に設定されています。
  - エンターキーを押すか、"Add Item"ボタンをクリックしてアイテムを追加します。
- **アイテムの削除**:
  - 各アイテムの横にある"Delete"ボタンをクリックして、リストからアイテムを削除することができます。
- **データの永続化**:
  - リストはローカルストレージに保存され、ページをリロードしてもリストの内容が保持されます。

## 使用技術
- **Vue.js**:
  - フロントエンドフレームワーク
- **ローカルストレージ**:
  - ブラウザのローカルストレージ
- **Bootstrap**:
  - CSSフレームワーク
- **HTML/CSS**:
  - シンプルなスタイルとレイアウト

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
