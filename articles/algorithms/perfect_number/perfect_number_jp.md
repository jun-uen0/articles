## 完全数（Perfect Number）

### 完全数とは？
完全数とは、自分自身を除く正の約数の総和が元の数と等しくなる自然数のことです。
数学的には次のように表されます。

\[
\sigma(n) - n = n
\]

ここで \( \sigma(n) \) は数 \( n \) の全ての正の約数の総和を表します。

例えば：
- **6** の約数は \( 1, 2, 3, 6 \) であり、\( 1 + 2 + 3 = 6 \) となるため、6 は完全数。
- **28** の約数は \( 1, 2, 4, 7, 14, 28 \) であり、\( 1 + 2 + 4 + 7 + 14 = 28 \) となるため、28 も完全数。


### 最初のいくつかの完全数
最も小さい完全数のリスト：

\[
6, 28, 496, 8128, 33550336, ...
\]

完全数は無限に存在すると考えられていますが、それを証明することはまだできていません。

---

## 完全数の性質
1. **偶数の完全数**
   - すべての既知の完全数は **偶数** です。
   - メルセンヌ素数（\( M_p = 2^p - 1 \) で素数となるもの）を使って、偶数の完全数を生成できます。
   - 公式：\( 2^{p-1} \times (2^p - 1) \)  （ここで \( p \) は素数）

2. **奇数の完全数は存在するか？**
   - まだ奇数の完全数は見つかっていません。
   - もし存在するとしたら、非常に大きな数であることが分かっています。

---

## **Pythonで完全数を求める**
以下のコードを使用すると、与えられた範囲内の完全数を見つけることができます。

```py
def is_perfect(n):
    divisors = [i for i in range(1, n) if n % i == 0]
    return sum(divisors) == n

# 1から10000までの完全数を探す
for num in range(1, 10001):
    if is_perfect(num):
        print(num)
```

このコードを実行すると、6、28、496、8128 という完全数が出力されます。

---

## メルセンヌ素数を使用した完全数の判定
メルセンヌ素数を使用して、より効率的に完全数を判定することができます。以下のPythonコードは、与えられた数が完全数であるかを確認します。

```py
def is_mersenne_prime(num):
    if num <= 1:
        return False
    if num == 2:
        return True
    if num % 2 == 0:
        return False
    
    for i in range(3, int(num ** 0.5) + 1, 2):
        if num % i == 0:
            return False
    return True

def check_perfect_number(num):
    if num % 2 != 0:
        return False
    
    n = 1
    while (1 << n) - 1 <= num:
        if (1 << (n - 1)) * ((1 << n) - 1) == num:
            if is_mersenne_prime((1 << n) - 1):
                return True
        n += 1
    
    return False

# 1から10000までの完全数を探す
for num in range(1, 10001):
    if check_perfect_number(num):
        print(num)
```

このコードはメルセンヌ素数を活用し、完全数の計算を最適化しています。

---

## 参考リンク

- [完全数 - Wikipedia](https://ja.wikipedia.org/wiki/%E5%AE%8C%E5%85%A8%E6%95%B0)