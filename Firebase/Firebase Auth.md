# Firebase Authentication 関連の関数とオブジェクト

## getAuth()

### 概要

`getAuth()`は Firebase Authentication のインスタンスを作成するための関数です。

### 使い方

```javascript
const { getAuth } = require("firebase/auth");

const auth = getAuth();
```

## signInWithRedirect()

### 概要

`signInWithRedirect()`は、リダイレクトを使って Firebase Authentication のログインフローを開始するための関数です。

### 使い方

```javascript
// Googleアカウントでログインする場合の例
const provider = new GoogleAuthProvider();
const auth = getAuth();

signInWithRedirect(auth, provider);
```

## signInWithPopup()

### 概要

`signInWithPopup()`は、ポップアップを使って Firebase Authentication のログインフローを開始するための関数です。

### 使い方

```javascript
// Googleアカウントでログインする場合の例
const provider = new GoogleAuthProvider();
const auth = getAuth();

signInWithPopup(auth, provider)
  .then((result) => {
    // ログイン成功時の処理
  })
  .catch((error) => {
    // エラー時の処理
  });
```

## GoogleAuthProvider

### 概要

`GoogleAuthProvider`は、Google アカウントを使った Firebase Authentication へのログインに必要なオブジェクトです。

### 使い方

```javascript
const provider = new GoogleAuthProvider();
```

## createUserWithEmailAndPassword()

### 概要

`createUserWithEmailAndPassword()`は、email と password を使用して新しいユーザーアカウントを作成するための関数です。

### 使い方

```javascript
const auth = getAuth();

createUserWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // アカウント作成成功時の処理
  })
  .catch((error) => {
    // エラー時の処理
  });
```

## signInWithEmailAndPassword()

### 概要

`signInWithEmailAndPassword()`は、email と password を使用して Firebase Authentication にログインするための関数です。

### 使い方

```javascript
const auth = getAuth();

signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // ログイン成功時の処理
  })
  .catch((error) => {
    // エラー時の処理
  });
```
