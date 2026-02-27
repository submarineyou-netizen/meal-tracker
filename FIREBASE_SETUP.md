# Firebaseプロジェクト作成手順

## ステップ1: Firebaseコンソールにアクセス

1. https://console.firebase.google.com/ を開く
2. Googleアカウントでログイン

## ステップ2: プロジェクトを作成

1. 「プロジェクトを追加」をクリック
2. プロジェクト名を入力
   - 例: `meal-tracker` または好きな名前
3. 「続行」をクリック
4. Google アナリティクス: 「今は必要ない」でOK
5. 「プロジェクトを作成」をクリック
6. 作成完了まで待つ（30秒ほど）
7. 「続行」をクリック

## ステップ3: Webアプリを登録

1. プロジェクトのホーム画面で「</>」（Webアイコン）をクリック
2. アプリのニックネーム: `meal-tracker-web` など
3. 「このアプリのFirebase Hostingも設定します」は**チェックしない**
4. 「アプリを登録」をクリック

## ステップ4: 設定情報をコピー

画面に表示される `firebaseConfig` の中身をコピーしてください。

```javascript
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "meal-tracker-xxxxx.firebaseapp.com",
  projectId: "meal-tracker-xxxxx",
  storageBucket: "meal-tracker-xxxxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:xxxxx"
};
```

この6つの値をメモしておいてください。

  apiKey: "AIzaSyB0wsz1J6oSZrh3THblauHQ0SO0EwDMqFk",
  authDomain: "meal-tracker-5e09f.firebaseapp.com",
  projectId: "meal-tracker-5e09f",
  storageBucket: "meal-tracker-5e09f.firebasestorage.app",
  messagingSenderId: "840097719622",
  appId: "1:840097719622:web:3241d850d96c4e87773147"

## ステップ5: Authentication（認証）を有効化

1. 左メニューの「構築」→「Authentication」をクリック
2. 「始める」をクリック
3. 「Google」を選択
4. 「有効にする」をON
5. 「プロジェクトのサポートメール」: 自分のメールアドレスを選択
6. 「保存」をクリック

## ステップ6: Firestore Database を有効化

1. 左メニューの「構築」→「Firestore Database」をクリック
2. 「データベースを作成」をクリック
3. 「本番環境モードで開始」を選択
4. 「次へ」をクリック
5. ロケーション: 「asia-northeast1（東京）」を選択
6. 「有効にする」をクリック
7. 作成完了まで待つ（1-2分）

## ステップ7: Firestore のセキュリティルールを設定

1. Firestore Database 画面で「ルール」タブをクリック
2. 以下のルールをコピーして貼り付け:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // ユーザーは自分のデータのみ読み書き可能
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

3. 「公開」をクリック

## 完了！

これで Firebase の設定は完了です。
ステップ4でコピーした設定情報を使ってアプリに組み込みます。
