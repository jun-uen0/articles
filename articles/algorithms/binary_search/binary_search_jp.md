## 二分探索法 (Binary Search)
二分探索法はターゲットの数字がリスト内にあるかを調べるアルゴリズムです。
処理の時間計算量は O(log N) です。

```py
# 数字「5」はリスト内にある？
trgt = 5
lst = [1, 2, 5, 8, 12, 19, 34]
```

## 前提
- リスト内の要素は数値型
- リストはソート済み

## 手順
1. リストの中央の値を取得する。
2. ターゲットの数字と取得した数字を比較する。
3. 以下のいずれかの処理を行う。
   - 一致すれば要素のインデックスを返す。
   - ターゲットの数字が大きければ、中央の値より右側の部分で検索を続ける。
   - ターゲットの数字が小さければ、中央の値より左側の部分で検索を続ける。
4. リスト内にターゲットの数字がない場合は None を返す。

## 例: 手動計算
```py
trgt = 5
lst = [1, 2, 5, 8, 12, 19, 34]

# リストの中央の値を取得
mid = len(lst) // 2  # 3
mid_n = lst[mid]  # 8
```
ターゲットの値は 5 であり、中央の値 8 より小さいため、
リストの左半分で検索を続ける。

```py
lst = lst[:mid]  # [1, 2, 5]
```

次のステップでは、新しいリスト `[1, 2, 5]` の中央の値を取得。
```py
mid = len(lst) // 2  # 1
mid_n = lst[mid]  # 2
```
ターゲット 5 は 2 より大きいため、右側のリスト `[5]` で検索を続ける。

```py
lst = lst[mid+1:]  # [5]
```

最後に、中央の値が 5 となり、一致するのでインデックスを返す。

## 計算量について
リストのサイズが 10,000,000 でも、二分探索を使えば 24 回の比較で判定可能。

```py
(1回) 10000000
(2回) 5000000
(3回) 2500000
(4回) 1250000
...
(24回) 1
```

処理のたびに検索範囲が半分に狭まるため、計算量は O(log N) となる。

## コード実装（反復処理）
```py
def binary_search_itr(lst, target):
    start = 0
    end = len(lst) - 1

    while start <= end:
        mid = (start + end) // 2
        if lst[mid] == target:
            return mid
        if lst[mid] > target:
            end = mid - 1  # 左側を検索
        else:
            start = mid + 1  # 右側を検索
    
    return None

my_list = [1, 3, 5, 7, 9]
print(binary_search_itr(my_list, 3))  # 1
print(binary_search_itr(my_list, -1)) # None
```

## コード実装（再帰処理）
```py
def binary_search_rcr(lst, target, start, end):
    if start > end:
        return None
    
    mid = (start + end) // 2
    if lst[mid] == target:
        return mid
    elif lst[mid] > target:
        return binary_search_rcr(lst, target, start, mid - 1)  # 左側を検索
    else:
        return binary_search_rcr(lst, target, mid + 1, end)  # 右側を検索

my_list = [1, 3, 5, 7, 9]
print(binary_search_rcr(my_list, 9, 0, len(my_list)-1))  # 4
print(binary_search_rcr(my_list, 10, 0, len(my_list)-1)) # None
```