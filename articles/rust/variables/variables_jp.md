# 変数
変数宣言はletで行う。
letは変数を束縛する。
束縛とは、変数名と値の対応付けを行うことである。
変数は、束縛された値を参照することができる。
変数は、束縛された値が変更されると、変更後の値を参照することができる。
他の言語で言うところの代入に近い。ただし、Rustでは束縛と代入はそれぞれ異なる概念として切り分けられている。

## 不変変数
束縛された値は変更できない。(=再代入できない)

letを使った一般的な変数宣言の例
```rust
fn main() {
  let x = 5; // xは5を参照する
  println!("x is {}", x);　// x is 5
  x = 6; // エラー、再代入はできない
}
```

## 可変変数
変数が不変であると、予期せぬバグなどが発生しにくく、可読性も高まる。
ただ、変数が不変であると、変数を使い回すことができない。
変数宣言の際にmutというキーワードを使うことで、変数を可変にすることができる。

let mut 変数名 = 値;

mutを使用して変数を可変にする例
```rust
fn main() {
  let mut x = 5; // xは5を参照する
  println!("x is {}", x);　// x is 5
  x = 6; // xは6を参照する
  println!("x is {}", x);　// x is 6
}
```

## シャドーイング
同じ名前の変数を宣言することで、変数を再定義することができる。
変数の再定義は、変数のスコープが異なる場合に限られる。
変数のスコープとは、変数が有効な範囲のことである。
実質mutを使用せずに、変数の値を変更することができる。(※ 可変になったわけではない)
```rust
fn main() {
  let x = 5; // xは5を参照する
  println!("x is {}", x);　// x is 5
  let x = 6; // 同じ名前で宣言し変数xを再定義
  println!("x is {}", x);　// x is 6
}
```

# 定数
定数は、変数と同様に束縛する。
定数の宣言は、constを使用する。
定数の宣言時には型アノテーションを行う必要がある。
定数は、変数と異なり、束縛された値を変更することができない。(mutを使用することはできない)
```rust
const MAX_POINTS: i32 = 100000;
```