# Firestore オブジェクトを作成する

Firestore のデータベースへの接続を確立するためには、Firestore オブジェクトを作成する必要があります。

```javascript
const firebaseConfig = {
  // Firebase configuration object
};

firebase.initializeApp(firebaseConfig);

const db = firebase.firestore();
```

## コレクションへの参照を取得する

コレクションを作成することは Firestore の基本です。一連のドキュメントを格納する場所としてコレクションを作成することで、Firestore はその集合の役割を果たし、クエリを実行できます。

```javascript
const usersCollectionRef = db.collection("users");
```

## ドキュメント参照を取得する

現在のドキュメントに対してデータを操作するには、ドキュメント参照を取得します。

```javascript
const userDocumentRef = usersCollectionRef.doc("user_id");
```

## ドキュメントを取得する

```javascript
try {
  const userDocumentSnapshot = await userDocumentRef.get();

  if (userDocumentSnapshot.exists) {
    console.log(userDocumentSnapshot.data());
  } else {
    console.log("No such document!");
  }
} catch (error) {
  console.error(error);
}
```

## コレクションまたはクエリから複数のドキュメントを取得する

```javascript
try {
  const usersCollectionSnapshot = await usersCollectionRef.get();

  usersCollectionSnapshot.forEach((doc) => {
    console.log(doc.id, "=>", doc.data());
  });
} catch (error) {
  console.error(error);
}
```

## フィルタリング、ソート及び制限

```javascript
const filteredQueryResult = await usersCollectionRef
  .where("age", ">", 18)
  .orderBy("age")
  .limit(5)
  .get();
```

## Firestore にデータを書き込む

```javascript
try {
  const addedUserDocumentRef = await usersCollectionRef.add({
    name: "John",
    age: 24,
    isOnline: false,
  });

  console.log(addedUserDocumentRef.id);
} catch (error) {
  console.error(error);
}
```

## Firestore の既存のドキュメントを更新する

```javascript
try {
  await userDocumentRef.update({
    name: "John",
    age: 25,
    isOnline: true,
  });
} catch (error) {
  console.error(error);
}
```

## Firestore からドキュメントを削除する

```javascript
try {
  await userDocumentRef.delete();
} catch (error) {
  console.error(error);
}
```

## Realtime Update

Firestore は、Realtime Database 同様に、Realtime updates をサポートしています。これにより、ドキュメントまたはクエリの内容が自動的に更新されることが保証されます。

```javascript
usersCollectionRef.onSnapshot((querySnapshot) => {
  const data = [];

  querySnapshot.forEach((doc) => {
    data.push({ id: doc.id, ...doc.data() });
  });

  console.log(data);
});
```

---

## `setDoc()`

ドキュメントを作成または上書きするために使用されます。

```javascript
const userDocumentRef = usersCollectionRef.doc("user_id");

try {
  const data = { name: "John", age: 30 };
  await userDocumentRef.set(data);
} catch (error) {
  console.error(error);
}
```

このコードでは、 'users'という名前のコレクションがあるものと推定しています。ここで'doc（'user_id')'メソッドを呼び出すことで、特定のドキュメントを参照します。`setDoc()`メソッドは、データオブジェクトを含む引数を取り、ドキュメントが存在しない場合は新しいドキュメントを作成し、存在する場合はデータを更新します。

## `getDoc()`

ドキュメントの内容を取得するために使用されます。

```javascript
const userDocumentRef = usersCollectionRef.doc("user_id");

try {
  const doc = await userDocumentRef.get();

  if (doc.exists()) {
    console.log("Document data:", doc.data());
  } else {
    console.log("No such document!");
  }
} catch (error) {
  console.error(error);
}
```

このコードでは、'users'コレクション内の'user_id'ドキュメントを参照しています。`getDoc()`メソッドは、指定されたドキュメントの内容を取得します。 このメソッドは非同期であり、`await`キーワードを使用して値を取得します。 取得した結果には`exists()`メソッドが含まれます。それにより、取得されたデータに何らかの情報が含まれているかどうかを確認することができます。存在しない場合は、エラーが出力されます。

## `updateDoc()`

既存のドキュメントを更新するために使用されます。

```javascript
const userDocumentRef = usersCollectionRef.doc("user_id");

try {
  const dataToUpdate = { age: 31 };
  await userDocumentRef.update(dataToUpdate);
} catch (error) {
  console.error(error);
}
```

このコードでは、'users'コレクション内の'user_id'ドキュメントを参照しています。`updateDoc()`メソッドは、更新したいフィールドを含むオブジェクトを引数として取ります。これにより、指定されたドキュメントが更新されます。

以上が Firestore でよく使用される`setDoc()`、`getDoc()`、`updateDoc()`の例です。これらの関数を使用することで、Firestore へのアクセスやドキュメントの管理、読み書き、削除などが可能になります。
