# Typescript 関数のオーバーロードとは？

TypeScript では、同じ関数名で異なるパラメーターを持つ複数の関数を定義することができます。これらの関数の組み合わせを関数のオーバーロードと呼びます。関数のオーバーロードを使用すると、関数のパラメーターと返り値に正しい型を強制できます。

## 関数のオーバーロードを使う

以下は、関数`calculateSum`の引数に応じて異なるタイプの計算を行う 3 つのオーバーロードの例です。最後に、未定義の場合は 0 を返すデフォルトの実装があります。

```typescript
function calculateSum(a: number, b: number): number;
function calculateSum(a: number, b: number, c: number): number;
function calculateSum(a: string, b: string): string;
function calculateSum(...args: any[]): any {
  if (typeof args[0] === "number" && typeof args[1] === "number") {
    let sum = args[0] + args[1];

    if (typeof args[2] === "number") {
      sum += args[2];
    }

    return sum;
  } else if (typeof args[0] === "string" && typeof args[1] === "string") {
    return args[0] + args[1];
  }

  return 0;
}

console.log(calculateSum(1, 2)); // Output: 3
console.log(calculateSum(1, 2, 3)); // Output: 6
console.log(calculateSum("Hello", "World")); // Output: "HelloWorld"
```

## まとめ

関数のオーバーロードは、TypeScript で異なるパラメーターを持つ複数の関数を定義することができます。これにより、パラメーターと返り値に正しい型を強制できます。オーバーロードを使用すると、コードの柔軟性を高め、コードの品質も向上します。
