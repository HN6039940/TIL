# Typescript ジェネリックスとは？

Typescript のジェネリックは、クラス、インターフェース、およびメソッドを作成するための強力な機能です
ジェネリックを使用することで、型を抽象化して再利用可能にし、一般的なアルゴリズムを書くことができます。

## ジェネリックの使い方

### クラスの例

以下は、ジェネリックを使用してクラスを作成する例です。

```typescript
class MyClass<T> {
  value: T;
  constructor(val: T) {
    this.value = val;
  }
}

const instance1 = new MyClass<string>("Hello");
const instance2 = new MyClass<number>(123);

console.log(instance1.value); // Output: "Hello"
console.log(instance2.value); // Output: 123
```

### 関数の例

ジェネリックを使用して関数を定義することもできます。以下は、配列内の最初の要素を返す汎用関数の例です。

```typescript
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

const arr1 = [10, 20, 30];
const arr2 = ["hello", "world"];

console.log(getFirst<number>(arr1)); // Output: 10
console.log(getFirst<string>(arr2)); // Output: "hello"
```

## まとめ

ジェネリックは、Typescript で強力な抽象化手段です。クラスや関数を汎用的に作成して、再利用可能なコードを書くことができます。ジェネリックを使用することで、より堅牢で拡張性のあるプログラムを構築することができます
